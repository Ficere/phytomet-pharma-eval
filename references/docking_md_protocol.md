# 分子对接与 MD 模拟详细参数

> 在阶段 3 需要具体计算细节时加载本文件。

## 1. 配体准备

### 1.1 从 SMILES 到 3D 构象

```python
from rdkit import Chem
from rdkit.Chem import AllChem

mol = Chem.MolFromSmiles("SMILES_HERE")
mol = Chem.AddHs(mol)
AllChem.EmbedMultipleConfs(mol, numConfs=50, randomSeed=42, pruneRmsThresh=0.5)
AllChem.MMFFOptimizeMoleculeConfs(mol, mmffVariant='MMFF94s')
# 选能量最低的 10 个用于 docking
```

### 1.2 质子化状态

- 用 [Dimorphite-DL](https://github.com/durrantlab/dimorphite_dl) 或 ChemAxon Marvin 生成 pH 7.4 的占优形式
- 对于含咪唑、胍基、羧酸的化合物，必须明确电荷态
- 重要：互变异构 (tautomer) 也需考虑，用 [Open Babel](http://openbabel.org/) 或 RDKit `EnumerateStereoisomers`

### 1.3 部分电荷

- AutoDock 系列：Gasteiger 电荷 (默认)
- MD：RESP/AM1-BCC 电荷 (用 antechamber 或 OpenFF)

## 2. 受体准备

### 2.1 PDB 选择原则

按优先级：

1. 与化合物结构相似的配体共晶 (resolution < 2.5 Å)
2. 同源蛋白共晶 (序列相似性 > 70%)
3. apo 结构 (无配体)
4. AlphaFold / RoseTTAFold 预测结构 (pLDDT > 80)

### 2.2 结构清理

工具：PDBFixer / PyMOL / Schrödinger Protein Preparation Wizard / Maestro

步骤：

1. 删除水分子 (除非已知结合口袋有保守水)
2. 补全缺失残基 (Modeller / loop modeling)
3. 添加氢原子
4. 优化质子化 (PROPKA, pH 7.4)
5. 修复键级、电荷
6. 限制能量最小化 (重原子约束 25 kcal/mol/Å²，OPLS/AMBER 力场)

### 2.3 结合口袋识别

| 工具 | 特点 |
|------|------|
| [fpocket](http://fpocket.sourceforge.net/) | 几何法，命令行，快 |
| [CASTp 3.0](http://sts.bioe.uic.edu/castp/) | 在线，含口袋体积/面积 |
| [SiteMap (Schrödinger)](https://www.schrodinger.com/products/sitemap) | 含 druggability 评分 |
| [P2Rank](https://prankweb.cz/) | ML 预测，准确率高 |
| 共晶配体定义 | grid box 围绕配体 ± 10 Å |

## 3. 分子对接

### 3.1 AutoDock Vina 标准流程

```bash
# 配体准备
mk_prepare_ligand.py -i ligand.sdf -o ligand.pdbqt

# 受体准备
prepare_receptor -r protein.pdb -o protein.pdbqt -A hydrogens

# 配置文件 config.txt
receptor = protein.pdbqt
ligand = ligand.pdbqt
center_x = 25.5
center_y = 18.3
center_z = -10.2
size_x = 22
size_y = 22
size_z = 22
exhaustiveness = 32       # 默认 8，提高到 32 以增加可重复性
num_modes = 20
energy_range = 4
seed = 42

# 运行
vina --config config.txt --out docked.pdbqt --log vina.log
```

### 3.2 Re-docking 验证

- 取共晶配体 → 用 OpenBabel 去氢 → 重新 docking → RMSD < 2 Å 才视为对接参数可靠
- 如果 RMSD > 2 Å：扩大 exhaustiveness、调整 grid box、检查质子化

### 3.3 GNINA (推荐用于天然产物)

```bash
gnina -r protein.pdb -l ligand.sdf \
  --autobox_ligand ref_ligand.sdf \
  -o gnina_out.sdf.gz \
  --num_modes 20 \
  --cnn_scoring rescore     # 用 CNN 模型重打分
```

GNINA 优势：集成 CNN 评分函数，对未见过的化合物泛化性优于 Vina。

### 3.4 DiffDock (盲对接)

无需指定口袋，适合未知靶点结合位点：

```bash
python -m inference --protein_path protein.pdb \
  --ligand "SMILES" \
  --out_dir results/ \
  --inference_steps 20 \
  --samples_per_complex 40 \
  --no_final_step_noise
```

### 3.5 结果分析

- 报告 top 5 pose 的对接分
- 用 PLIP / Schrödinger Ligand Interaction Diagram 分析关键相互作用：氢键、π-π、π-阳离子、盐桥、卤键、疏水接触
- 截 2D / 3D 相互作用图

## 4. MM-GBSA / MM-PBSA 重打分

### 4.1 工具

- AMBER `MMPBSA.py`
- Schrödinger Prime MM-GBSA
- gmx_MMPBSA (GROMACS)

### 4.2 简化流程 (AMBER)

```bash
# 1. 从对接结果生成 complex.pdb
# 2. tleap 加力场 (ff14SB + GAFF2)
# 3. 短时 MD (5–10 ns) 平衡
# 4. 抽 100 帧
MMPBSA.py -O -i mmpbsa.in -cp complex.prmtop \
  -rp receptor.prmtop -lp ligand.prmtop \
  -y md.nc -o results.dat
```

`mmpbsa.in` 关键设置：

```
&general
  startframe=1, endframe=100, interval=1, verbose=2,
/
&gb
  igb=5, saltcon=0.150,
/
```

- 报告 ΔG_bind = ΔE_MM + ΔG_solv - TΔS
- 仅作 ranking，绝对值勿过度解读

## 5. MD 模拟 (50–200 ns)

### 5.1 GROMACS 推荐工作流

```bash
# 力场
gmx pdb2gmx -f protein.pdb -o processed.gro -ff amber99sb-ildn -water tip3p

# 配体力场 (acpype 或 CGenFF)
acpype -i ligand.mol2 -n 0 -a gaff2

# 体系
gmx editconf -f complex.gro -o box.gro -bt dodecahedron -d 1.2
gmx solvate -cp box.gro -cs spc216.gro -p topol.top -o solv.gro
gmx grompp -f ions.mdp -c solv.gro -p topol.top -o ions.tpr
gmx genion -s ions.tpr -o solv_ions.gro -p topol.top -pname NA -nname CL -neutral -conc 0.15

# EM → NVT (100 ps) → NPT (100 ps) → Production
gmx mdrun -deffnm em
gmx mdrun -deffnm nvt
gmx mdrun -deffnm npt
gmx grompp -f md.mdp -c npt.gro -t npt.cpt -p topol.top -o md.tpr
gmx mdrun -deffnm md -nb gpu -bonded gpu -pme gpu
```

### 5.2 关键参数 (md.mdp)

- 时间步长 2 fs，LINCS 约束 H 键
- T = 310 K (Berendsen → V-rescale)
- P = 1 atm (Parrinello-Rahman)
- PME 长程静电，cutoff 1.0 nm
- 输出：每 10 ps 一帧

### 5.3 分析

| 指标 | 工具 | 含义 |
|------|------|------|
| RMSD (配体重原子) | `gmx rms` | < 3 Å 视为稳定 |
| RMSF (蛋白残基) | `gmx rmsf` | 识别柔性区 |
| 氢键占有率 | `gmx hbond` | > 50% 为关键氢键 |
| 接触面积 / SASA | `gmx sasa` | 结合紧密度 |
| 主成分分析 (PCA) | `gmx covar` + `gmx anaeig` | 构象变化模式 |
| 自由能景观 | gmx WHAM | umbrella sampling |

### 5.4 增强采样

- **Metadynamics** (PLUMED)：探索结合/解离路径
- **Umbrella Sampling**：精确 PMF
- **REMD**：克服能垒

## 6. FEP / Alchemical Free Energy (高精度)

适用于 lead optimization 阶段的 ΔΔG 计算：

- **FEP+** (Schrödinger，商业，工业首选)
- **PMX / GROMACS alchemical** (开源)
- **AMBER TI**

典型工作流：

1. 设计配体对 (R 基团变换，ΔLogP < 1)
2. 构建 λ 路径 (16–24 windows)
3. 每个 window 跑 5–10 ns
4. BAR / MBAR 估计 ΔG
5. 与实验 IC50 ΔΔG 比较，验证模型

## 7. 报告对接结果的模板

```
靶点: EGFR (PDB: 1M17, 2.6 Å)
方法: AutoDock Vina 1.2.5, exhaustiveness=32, GNINA rescore
Re-docking RMSD (共晶配体 ERL): 1.2 Å ✓
Top pose:
  Vina score: -9.4 kcal/mol
  GNINA CNN score: 0.78
  MM-GBSA: -52.3 kcal/mol
  关键相互作用:
    - H-bond: Met793 (backbone NH) - 配体酚羟基 (2.1 Å)
    - π-π stacking: Phe699 - 配体苯环
    - 疏水接触: Leu718, Val726, Leu844
MD (100 ns):
  Ligand RMSD: 1.8 ± 0.4 Å (稳定)
  Met793 H-bond 占有率: 87%
  结论: 结合模式合理，建议湿实验验证 (SPR / BLI Kd 测定)
```
