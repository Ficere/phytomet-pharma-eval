# 工具与数据库速查表

> 各阶段推荐的工具、数据库与代表性文献。

## 1. 化合物数据库

| 名称 | 内容 | URL |
|------|------|-----|
| PubChem | 通用化学数据库，1.1 亿+ 化合物 | https://pubchem.ncbi.nlm.nih.gov/ |
| ChEMBL | 含生物活性数据，220 万+ 化合物，1500 万 activity | https://www.ebi.ac.uk/chembl/ |
| ZINC22 | 商业可购化合物，37 亿+ | https://zinc22.docking.org/ |
| **COCONUT** | 天然产物专属，70 万+ | https://coconut.naturalproducts.net/ |
| **LOTUS** | 天然产物 + 来源生物，36 万+ | https://lotus.naturalproducts.net/ |
| **TCMSP** | 中药系统药理学 | https://old.tcmsp-e.com/ |
| **TCMID** | 中药成分 - 靶点 - 疾病 | http://www.megabionet.org/tcmid/ |
| **HERB / SymMap** | 中药本草数据库 | http://herb.ac.cn/ |
| Dictionary of Natural Products | 商业，全面 | https://dnp.chemnetbase.com/ |
| NPASS | 天然产物活性 & 物种 | http://bidd.group/NPASS/ |
| SuperNatural 3.0 | 50 万+ 天然产物 | https://bioinf-applied.charite.de/supernatural_3/ |

## 2. 靶点 / 通路数据库

| 名称 | 用途 |
|------|------|
| UniProt | 蛋白注释 |
| PDB / PDBe | 晶体结构 |
| AlphaFold DB | 预测结构，2 亿+ |
| DrugBank | 已上市药物-靶点 |
| TTD (Therapeutic Target Database) | 治疗靶点 |
| OMIM | 疾病-基因 |
| KEGG / Reactome / WikiPathways | 通路 |
| STRING | 蛋白-蛋白互作 |
| BindingDB | 结合亲和力 |
| GtoPdb (Guide to Pharmacology) | 配体-受体药理 |

## 3. 靶点预测工具 (web)

| 工具 | 算法 | 输入 | URL |
|------|------|------|-----|
| SwissTargetPrediction | 2D/3D 相似性 | SMILES | http://www.swisstargetprediction.ch/ |
| SEA | 相似性集成 | SMILES | https://sea.bkslab.org/ |
| PharmMapper | 反向药效团 | SDF | http://www.lilab-ecust.cn/pharmmapper/ |
| TargetNet | 多任务 ML | SMILES | http://targetnet.scbdd.com/ |
| SuperPred | 相似性 + ATC | SMILES | https://prediction.charite.de/ |
| ChEMBL Target Prediction | RF 模型 | SMILES | https://www.ebi.ac.uk/chembl/ |
| HitPick | 相似性 | SMILES | http://mips.helmholtz-muenchen.de/proj/hitpick/ |
| PASS Online | QSAR | SMILES | http://www.way2drug.com/passonline/ |

## 4. 计算化学软件

### 开源

| 软件 | 用途 |
|------|------|
| RDKit | 化学信息学库 (Python) |
| Open Babel | 格式转换、力场 |
| AutoDock Vina / Smina / GNINA | 对接 |
| AutoDockFR (ADFR) | 柔性对接 |
| DiffDock / EquiBind | 扩散模型盲对接 |
| Rosetta | 蛋白-配体、ddG |
| GROMACS / AMBER / OpenMM | MD |
| PLUMED | 增强采样 |
| PyMOL | 可视化 |
| ChimeraX | 可视化 |
| Avogadro | 分子构建 |
| Psi4 / NWChem / ORCA | 量子化学 |

### 商业

| 软件 | 公司 |
|------|------|
| Schrödinger Suite (Maestro, Glide, FEP+, Desmond) | Schrödinger |
| MOE | CCG |
| Discovery Studio | BIOVIA |
| ICM | Molsoft |
| Cresset Flare | Cresset |
| SeeSAR | BioSolveIT |

## 5. ADMET 工具

| 工具 | 类型 |
|------|------|
| SwissADME | 免费 web |
| ADMETlab 3.0 | 免费 web，70+ 端点 |
| pkCSM | 免费 web |
| ProTox 3.0 | 毒性预测 |
| StarDrop (Optibrium) | 商业 |
| ADMET Predictor (Simulations Plus) | 商业，工业标准 |
| Volsurf+ | 商业 |
| QikProp (Schrödinger) | 商业 |
| admetSAR | 免费 web |
| Vienna LiverTox | 肝毒性 |

## 6. PK 软件

| 软件 | 用途 |
|------|------|
| Phoenix WinNonlin (Certara) | NCA / 房室分析，工业标准 |
| Monolix / PKanalix (Lixoft) | 群体 PK |
| NONMEM | 群体 PK，监管金标准 |
| GastroPlus (Simulations Plus) | PBPK |
| Simcyp (Certara) | PBPK，工业首选 |
| PK-Sim / MoBi (Open Systems Pharmacology) | 开源 PBPK |
| PKNCA (R 包) | 开源 NCA |
| nlmixr2 / Pumas | 开源群体 PK |

## 7. AI / ML 工具 (用户领域)

| 工具 | 用途 |
|------|------|
| DeepChem | 化学 ML 框架 |
| Chemprop | 分子性质 GNN |
| ChemBERTa / MolBERT / MolFormer | 化学语言模型 |
| Mol2Image / MolDiff | 生成式分子设计 |
| REINVENT 4 | 强化学习分子生成 |
| TamGen / MolGPT | Transformer 生成 |
| AlphaFold 3 / Boltz-1 / Chai-1 | 蛋白-配体复合物预测 |
| RFdiffusion + ProteinMPNN | 蛋白设计 |
| DiffDock-L | SOTA 盲对接 |
| Uni-Mol / Uni-Mol+ | 3D 分子表征 |
| BindingNet / GNINA-CNN | 对接 rescoring |

## 8. 文献检索

| 工具 | 特色 |
|------|------|
| PubMed | 生物医学文献 |
| Google Scholar | 通用 |
| Scopus / Web of Science | 引文分析 |
| Reaxys | 化学反应、合成 |
| SciFinder-n | 化合物检索 |
| Europe PMC | 开源 PMC |
| Semantic Scholar | AI 辅助 |
| **天然产物专属**：Marinlit, NaprAlert, TCMID 文献模块 |  |

## 9. 关键综述与方法学文献

为评估报告建议引用以下基础文献（按主题）：

**天然产物药物发现总论**

- Newman DJ, Cragg GM. *Natural Products as Sources of New Drugs over the Nearly Four Decades from 01/1981 to 09/2019*. J Nat Prod. 2020;83(3):770-803.
- Atanasov AG, et al. *Natural products in drug discovery: advances and opportunities*. Nat Rev Drug Discov. 2021;20(3):200-216.

**结构鉴定**

- Bross-Walch N, et al. *Strategies and tools for structure determination of natural products using modern NMR*. Chem Biodivers. 2005;2(2):147-77.

**体外活性筛选**

- Riss TL, et al. *Cell Viability Assays*. Assay Guidance Manual. 2016.

**靶点预测**

- Sydow D, et al. *Advances and Challenges in Computational Target Prediction*. J Chem Inf Model. 2019;59(5):1728-1742.

**分子对接**

- Pinzi L, Rastelli G. *Molecular Docking: Shifting Paradigms in Drug Discovery*. Int J Mol Sci. 2019;20(18):4331.

**MD 模拟**

- Hollingsworth SA, Dror RO. *Molecular Dynamics Simulation for All*. Neuron. 2018;99(6):1129-1143.

**ADMET**

- Wu F, et al. *Computational Approaches in Preclinical Studies on Drug Discovery and Development*. Front Chem. 2020;8:726.

**PK 分析**

- FDA. *Bioanalytical Method Validation Guidance for Industry*. 2018.

## 10. 工作流自动化建议 (面向用户)

结合用户的 Docker / Python / GitHub 工作流，推荐：

1. **化学数据管线**：RDKit + Pandas + DuckDB 处理化合物库
2. **批量对接**：Snakemake / Nextflow + Vina/GNINA + slurm
3. **MD 自动化**：BioBB (Biomolecular Building Blocks) + GROMACS
4. **ADMET 批量预测**：调用 ADMETlab API / 本地 chemprop 模型
5. **结果聚合**：MLflow / Weights & Biases 追踪实验
6. **报告生成**：Jupyter + Quarto / nbdev → PDF / HTML
7. **数据库**：MongoDB / DuckDB 存化合物 + 活性 + 预测结果
8. **可视化**：Streamlit / Dash 仪表板供团队查看
