---
name: phytomet-pharma-eval
description: "植物次生代谢物 (Plant Secondary Metabolite) 药用价值标准化评估流程。覆盖代谢物结构鉴定、体外药效活性初筛（抗肿瘤/抗炎/抗氧化）、基于分子对接的靶点预测、ADMET 与体内药代动力学分析四大阶段，输出可执行的科研工作流。当用户提到植物代谢物、天然产物药用评估、phytochemical screening、natural product drug discovery、靶点预测、ADMET、分子对接、药代动力学、抗肿瘤/抗炎/抗氧化初筛、活性评价 SOP 时使用此技能。"
license: MIT
metadata:
  author: gljx898989
  version: '1.0'
  domain: 'natural-product-drug-discovery'
---

# 植物次生代谢物药用价值评估流程 (Phytomet-Pharma-Eval)

## 何时使用此技能

当用户需要对一个或多个植物次生代谢物（生物碱、黄酮、萜类、酚酸、皂苷、香豆素等）开展系统性药用价值评估时使用，典型场景包括：

- 从天然产物粗提物到候选化合物的研究流程设计
- 单一代谢物的成药性 (drug-likeness) 评估
- 靶点反向预测 (target fishing) 与机制假说生成
- 抗肿瘤 / 抗炎 / 抗氧化等方向的体外活性筛选 SOP
- ADMET 性质预测与体内 PK 实验方案设计
- 撰写候选化合物评估报告 / 立项报告 / 综述

## 输出形态

根据用户需求，技能可输出以下三类交付物中的一种或多种：

1. **评估报告** (Markdown / PDF)：针对特定化合物的全流程评估
2. **SOP 工作流** (Markdown)：可被实验团队执行的标准操作流程
3. **决策矩阵** (表格)：多个候选化合物的横向比较与优先级排序

## 核心评估框架：四阶段漏斗模型

```
阶段 1: 结构鉴定与表征 (Structure ID)
        ↓ 通过 → 化合物明确、纯度 >95%
阶段 2: 体外药效初筛 (In vitro Bioactivity)
        ↓ 通过 → 至少 1 个 model 显示 IC50 < 50 μM
阶段 3: 靶点预测与分子对接 (Target Prediction & Docking)
        ↓ 通过 → 找到合理结合靶点 (docking score < -7 kcal/mol)
阶段 4: ADMET 与体内 PK (ADMET & PK)
        ↓ 通过 → 口服生物利用度可接受、无严重毒性预警
       【进入 lead optimization / 立项】
```

每个阶段都有明确的 **Go / No-Go 决策标准**，避免在低质量化合物上浪费资源。

## 阶段 1：结构鉴定与化学表征

### 1.1 目标

- 确认化合物的 2D/3D 结构
- 评估纯度 (≥95% 用于活性评价)
- 获取关键理化参数 (LogP, MW, pKa, 溶解度)

### 1.2 推荐技术栈

| 技术 | 用途 | 输出 |
|------|------|------|
| **HRMS (ESI/APCI-Q-TOF)** | 分子式确认 | [M+H]⁺ 精确质量、误差 < 5 ppm |
| **1D NMR (¹H, ¹³C)** | 平面结构 | δ 化学位移、耦合常数 |
| **2D NMR (HSQC, HMBC, COSY, NOESY)** | 连接关系、立体化学 | 关键 HMBC 相关 |
| **UV-Vis、IR** | 官能团辅助 | 特征吸收 |
| **X-ray / ECD** | 绝对构型 | CD 曲线、Flack 参数 |
| **HPLC-DAD / HPLC-MS** | 纯度评估 | 主峰面积 % |

### 1.3 数字化与数据库检索

1. 用 **ChemDraw / RDKit** 绘制结构 → 生成 SMILES、InChI、InChIKey
2. 在以下数据库进行去重 (是否为已知化合物)：
   - [PubChem](https://pubchem.ncbi.nlm.nih.gov/)
   - [ChEMBL](https://www.ebi.ac.uk/chembl/)
   - [Dictionary of Natural Products (DNP)](https://dnp.chemnetbase.com/)
   - [COCONUT (天然产物专属)](https://coconut.naturalproducts.net/)
   - [TCMSP (中药系统药理)](https://old.tcmsp-e.com/tcmsp.php)
3. 用 **SciFinder / Reaxys** 检索结构相似化合物 (Tanimoto > 0.7) 的已报道活性，作为先验

### 1.4 Go / No-Go 决策

- ✅ Go：结构明确、纯度 >95%、无已报道严重毒性
- ❌ No-Go：结构不确定（异构体未分开）、纯度 <80%、已知为通用 PAINS / 弗朗克 (Frequent Hitter) 化合物
  - 用 [FAF-Drugs4](https://fafdrugs4.rpbs.univ-paris-diderot.fr/) 或 RDKit 的 PAINS filter 检查

## 阶段 2：体外药效活性初筛

### 2.1 三大方向的初筛模型矩阵

| 方向 | 一级筛选 (生化/简单细胞) | 二级筛选 (机制) | 关键指标 |
|------|--------------------------|-----------------|----------|
| **抗肿瘤** | MTT/CCK-8 (HepG2, MCF-7, A549, HCT-116, A375 多细胞系) | 克隆形成、细胞周期 (PI)、凋亡 (Annexin V/PI) | IC50 (24/48/72 h)、SI = IC50(正常)/IC50(肿瘤) ≥ 3 |
| **抗炎** | LPS 诱导 RAW264.7，ELISA 测 TNF-α / IL-6 / NO (Griess) | NF-κB 报告基因、Western blot (p-p65, p-IκBα) | NO 抑制率、IC50 (cytokine)、正常细胞毒性 (CC50) |
| **抗氧化** | DPPH、ABTS、FRAP、ORAC | 细胞内 ROS (DCFH-DA)、Nrf2/HO-1 通路、MDA / SOD / GSH | EC50 (μM)、与 Trolox/VC 比较 |

### 2.2 实验设计要点

1. **剂量梯度**：至少 5–7 个浓度点 (典型 0.1, 0.3, 1, 3, 10, 30, 100 μM)，跨 3 个数量级
2. **重复**：每个浓度至少 3 个生物学重复 + 3 个技术重复
3. **对照**：
   - 阴性对照（溶剂，DMSO 终浓度 ≤ 0.1%）
   - 阳性对照（如阿霉素 / 顺铂 / 地塞米松 / Trolox）
   - 空白对照
4. **数据分析**：GraphPad Prism 非线性回归拟合，报告 IC50 ± 95% CI 和 Hill slope
5. **筛除假阳性**：
   - 荧光化合物干扰 → 改用比色 / 同位素法
   - 聚集 (aggregation) → 加 0.01% Triton X-100 复测
   - 与 luciferase 直接结合 → 用 nano-luciferase 复检

### 2.3 Go / No-Go 决策

- ✅ Go：至少 1 个 model 中 IC50 < 50 μM 且 SI ≥ 3，剂量-反应曲线光滑 (Hill slope ≈ 1)
- ⚠️ 待定：IC50 50–100 μM，可考虑结构衍生 (SAR) 后再评
- ❌ No-Go：IC50 > 100 μM 在所有模型，或显示明显细胞毒性导致假信号

## 阶段 3：靶点预测与分子对接

> 此阶段是用户专业领域 (蛋白工程 + 计算化学) 的优势环节，强调先反向预测再正向验证。

### 3.1 靶点反向预测 (Target Fishing)

| 工具 | 算法 | 适用 |
|------|------|------|
| [SwissTargetPrediction](http://www.swisstargetprediction.ch/) | 2D/3D 相似性 | 人源蛋白，快速 |
| [SEA (Similarity Ensemble Approach)](https://sea.bkslab.org/) | 配体相似性 + 统计 | 大规模筛选 |
| [PharmMapper](http://www.lilab-ecust.cn/pharmmapper/) | 反向药效团映射 | 结构多样化合物 |
| [TargetNet](http://targetnet.scbdd.com/) | 多任务 ML | 623 个人源靶点 |
| [SuperPred](https://prediction.charite.de/) | 相似性 + ATC | 含药物-靶点关系 |
| **AlphaFold + 反向 Docking** | 全蛋白组扫描 | 新靶点发现，需算力 |

**实践建议**：至少用 3 个工具取交集，输出靶点优先级表（带通路注释，KEGG / Reactome）。

### 3.2 通路富集与机制假说

1. 将候选靶点列表上传 [DAVID](https://david.ncifcrf.gov/) / [Metascape](https://metascape.org/) / [Enrichr](https://maayanlab.cloud/Enrichr/)
2. 富集 KEGG pathway、GO term、Reactome
3. 构建 "化合物 - 靶点 - 通路 - 表型" 网络 (Cytoscape)
4. 形成可证伪的机制假说，连接到阶段 2 观察到的表型

### 3.3 分子对接验证

#### 准备

- **配体**：用 RDKit / OpenBabel 加氢、能量最小化 (MMFF94)，生成多个构象
- **受体**：从 PDB 下载共晶结构 (优先) 或 AlphaFold 模型，用 PDBFixer / Schrödinger Protein Prep 处理
- **结合口袋**：用 fpocket / CASTp / SiteMap 识别，或基于已知配体定义 grid box

#### 对接工具

| 工具 | 特点 | 速度 |
|------|------|------|
| **AutoDock Vina / Vina-GPU** | 免费、广泛使用、基线方法 | 快 |
| **Smina / GNINA** | Vina 改进，GNINA 集成 CNN 打分 | 中 |
| **Glide (SP/XP)** | Schrödinger 商业、精度高 | 中-慢 |
| **DiffDock** | 扩散模型，盲对接 SOTA | 中 (需 GPU) |
| **GOLD** | 灵活、口袋柔性 | 慢 |

#### 评分与验证

1. **Re-docking**：先对共晶配体重对接，RMSD < 2 Å 才信任评分
2. **打分**：报告对接分 (kcal/mol)、关键氢键、π-π 堆积、盐桥
3. **MM-GBSA / MM-PBSA**：对 top hits 重新计算结合自由能
4. **MD 模拟** (推荐，用户优势)：50–200 ns，看 RMSD/RMSF/H-bond 占有率稳定性
5. **FEP / TI** (高精度)：用于 lead optimization 阶段的 ΔΔG 预测

### 3.4 Go / No-Go 决策

- ✅ Go：≥ 1 个生物学合理的靶点，docking score ≤ -7 kcal/mol，MD 稳定 (RMSD < 3 Å)，且靶点-表型一致
- ❌ No-Go：所有预测靶点都打分弱 (> -5)、MD 中迅速解离、靶点无法解释体外表型

## 阶段 4：ADMET 预测与体内药代动力学

### 4.1 计算 ADMET 预筛

| 工具 | 输出 |
|------|------|
| [SwissADME](http://www.swissadme.ch/) | Lipinski/Veber/Egan、BBB、GI 吸收、CYP 抑制 |
| [ADMETlab 3.0](https://admetlab3.scbdd.com/) | 70+ 端点（吸收、分布、代谢、排泄、毒性） |
| [pkCSM](https://biosig.lab.uq.edu.au/pkcsm/) | PK 参数预测 (Caco-2, VDss, t1/2, CL) |
| [ProTox-3.0](https://tox.charite.de/protox3/) | LD50、肝毒性、致癌性、心脏毒性 (hERG) |
| [DeepTox / Tox21](https://tox21.gov/) | 12 类毒性端点 |

**关键过滤**：

- Lipinski / Veber 规则（柔性）
- PAINS / Brenk / NIH alerts
- hERG IC50 > 10 μM (预测)
- 肝毒性、致突变性预警

### 4.2 体外 ADME 实验 (送 CRO 或自建)

| 项目 | 方法 | 关键阈值 |
|------|------|---------|
| 溶解度 | Shake-flask / kinetic (PBS pH 7.4, FaSSIF) | > 10 μg/mL 较好 |
| 渗透性 | Caco-2 / PAMPA | Papp > 1×10⁻⁶ cm/s |
| 血浆蛋白结合 | 平衡透析 | 通常 < 99% |
| 微粒体稳定性 | 人/大鼠肝微粒体，孵育 60 min | t1/2 > 30 min，CLint 低 |
| CYP 抑制 | 探针底物 + LC-MS/MS (1A2/2C9/2C19/2D6/3A4) | IC50 > 10 μM |
| 血脑屏障 | MDCK-MDR1 / 小鼠脑/血浓度比 | 视靶点需求 |

### 4.3 体内 PK 实验设计

**典型方案 (大鼠 / 小鼠)**：

- **给药途径**：IV (1–5 mg/kg) + PO (10–50 mg/kg)，平行组比较口服生物利用度
- **采血点**：5 min, 15 min, 30 min, 1, 2, 4, 6, 8, 12, 24 h (IV)；15 min, 30 min, 1, 2, 4, 6, 8, 12, 24, 48 h (PO)
- **生物分析**：HPLC-MS/MS (用户专长)，建立 LLOQ ≤ 1 ng/mL 的方法，内标用结构类似物或氘代物
- **PK 参数 (WinNonlin / Phoenix / NCA)**：
  - Cmax, Tmax, t1/2, AUC0-t, AUC0-∞, CL, Vss, MRT
  - F (生物利用度) = (AUC_PO × Dose_IV) / (AUC_IV × Dose_PO)
- **组织分布** (PD/PK 关联)：测肝、肾、脑、肿瘤组织浓度
- **代谢物鉴定**：胆汁/尿液/血浆中用 Q-TOF 寻找 M+16, M+14, M+2, M-2 等代谢路径

### 4.4 Go / No-Go 决策

- ✅ Go：F% > 10% (口服小分子)、t1/2 > 1 h、无严重毒性、暴露量与体外 IC50 匹配
- ⚠️ 待定：F% 较低但可通过制剂改善 (前药、纳米载体)
- ❌ No-Go：F% < 2%、t1/2 < 15 min、hERG 强阻断、肝毒性确证

## 横向决策矩阵 (多化合物比较)

当需要在 N 个候选物中选择优先推进对象，输出如下表格：

| 化合物 | 阶段1纯度 | 阶段2 best IC50 | 阶段3 top 靶点 / docking | 阶段4 F% | LE | LipE | 综合优先级 |
|--------|-----------|-----------------|---------------------------|----------|-----|------|-------------|
| Cpd-A | 98% | 5 μM (HepG2) | EGFR / -9.2 | 12% | 0.35 | 5.1 | ⭐⭐⭐ |
| Cpd-B | 95% | 18 μM (RAW) | COX-2 / -7.8 | 28% | 0.30 | 4.2 | ⭐⭐ |
| ... | | | | | | | |

- **LE (Ligand Efficiency)** = -ΔG / 重原子数；目标 ≥ 0.3
- **LipE (Lipophilic Efficiency)** = pIC50 - LogP；目标 ≥ 3

## 报告模板

输出报告时遵循以下章节顺序：

1. **摘要**：化合物名称、来源植物、最有潜力的方向 (1 句话)
2. **结构与表征**：SMILES、关键 NMR/MS 数据、纯度
3. **活性初筛**：剂量-反应曲线截图、IC50 表、SI
4. **靶点与机制假说**：top 3 靶点、关键残基、富集通路、机制图
5. **ADMET & PK**：计算预测 + 体内数据
6. **综合评估**：SWOT 分析、Go/No-Go 建议、下一步实验
7. **参考文献**：Vancouver 格式，含 DOI

## 工作流执行步骤

当被调用时：

1. **询问输入**（如果用户未提供）：
   - 化合物名称 / SMILES / 来源植物
   - 主攻方向（抗肿瘤 / 抗炎 / 抗氧化 / 其他）
   - 当前已有数据（结构、活性、PK）
   - 评估深度：快速 (just 阶段1-2) / 完整四阶段 / 多化合物比较

2. **检索先验**：用 web 检索化合物在 PubChem / ChEMBL / 文献中的已知信息（IC50、靶点、PK）

3. **生成评估**：按四阶段框架填充，区分 "已有数据"、"文献推断"、"建议补做"

4. **决策建议**：明确 Go/No-Go 与下一步实验设计

5. **加载详细参考** (按需)：
   - 实验操作细节 → `references/in_vitro_assays.md`
   - 对接 / MD 详细参数 → `references/docking_md_protocol.md`
   - PK 实验 SOP → `references/in_vivo_pk_sop.md`
   - 推荐工具与数据库清单 → `references/tools_databases.md`

## 引用规范

- 所有活性数据、靶点信息须注明来源（PMID / DOI / 数据库 ID）
- 计算预测须注明工具版本和参数
- 区分 "实验测得" (有 reference) vs "AI 预测" (注明模型)

## 兼容性说明

- 本流程适用于小分子代谢物 (MW < 1000 Da)。大分子 (多糖、蛋白类) 需调整
- 体内实验需符合本地 IACUC 与伦理要求
- 计算工具中的免费 web 服务对商业用途可能有限制，请遵守 license
