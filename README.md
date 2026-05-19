# Phytomet-Pharma-Eval

**植物次生代谢物药用价值评估流程 (Agent Skill)**

A standardized research workflow Agent Skill for evaluating the pharmaceutical potential of plant secondary metabolites, covering structure identification, *in vitro* bioactivity screening (anti-tumor / anti-inflammatory / anti-oxidant), molecular docking-based target prediction, and *in vivo* pharmacokinetics analysis.

> 一套面向科研人员的标准化工作流，把"一个分子从结构到 PK"的路径模板化、可重复化。

## 概览 / Overview

本 skill 把植物次生代谢物 (Plant Secondary Metabolite) 的药用价值评估拆解为四个串行漏斗阶段，每阶段都有明确的 **Go / No-Go 决策标准**：

```
阶段 1: 结构鉴定与表征 (Structure ID & Characterization)
   ↓
阶段 2: 体外药效活性初筛 (In vitro Bioactivity: Anti-tumor / Anti-inflammation / Anti-oxidant)
   ↓
阶段 3: 靶点预测与分子对接 (Target Fishing & Molecular Docking)
   ↓
阶段 4: ADMET 与体内药代动力学 (ADMET & In vivo PK)
```

## 何时使用 / When to Use

当用户对一个或多个植物次生代谢物（生物碱、黄酮、萜类、酚酸、皂苷、香豆素等）开展系统性评估时，例如：

- 从天然产物粗提物到候选化合物的研究路径设计
- 单一代谢物的成药性 (drug-likeness) 评估
- 靶点反向预测 (target fishing) 与机制假说生成
- 抗肿瘤 / 抗炎 / 抗氧化方向的体外活性筛选 SOP
- ADMET 预测与体内 PK 实验方案设计
- 多化合物横向比较与立项优先级排序

## 输出形态

- **评估报告** (Markdown / PDF)：单一化合物全流程评估
- **SOP 工作流**：可执行的实验标准操作流程
- **决策矩阵**：多候选化合物横向比较表

## 文件结构

```
phytomet-pharma-eval/
├── SKILL.md                            # 主入口：四阶段框架 + Go/No-Go 决策
└── references/
    ├── in_vitro_assays.md              # 体外活性筛选详细 SOP
    ├── docking_md_protocol.md          # 分子对接 / MD / FEP 参数
    ├── in_vivo_pk_sop.md               # 体内 PK 实验 + LC-MS/MS 方法学验证
    └── tools_databases.md              # 工具与数据库速查表
```

## 安装与使用

### 在 Perplexity Computer 中加载

1. 下载本仓库为 zip 或克隆：
   ```bash
   git clone https://github.com/<your-user>/phytomet-pharma-eval.git
   ```
2. 打包 skill 目录为 `phytomet-pharma-eval.zip`
3. 在 [Perplexity Computer Skills](https://www.perplexity.ai/computer/skills) 上传

### 触发关键词

skill 会在用户提到以下关键词时被自动调用：

> 植物代谢物、天然产物药用评估、phytochemical screening、natural product drug discovery、靶点预测、ADMET、分子对接、药代动力学、抗肿瘤/抗炎/抗氧化初筛、活性评价 SOP

## 核心特色

- **四阶段漏斗 + 明确决策标准**：避免在低质量化合物上浪费资源
- **覆盖湿干结合**：实验 SOP + 计算化学参数都给到可复用粒度
- **面向科研工程化**：推荐 Snakemake / Nextflow / Docker 等自动化管线
- **数据库与工具速查**：30+ 主流工具与数据库的用途与 URL
- **报告模板**：直接产出立项 / 综述章节的可引用素材

## 适用范围

- 适用于小分子代谢物 (MW < 1000 Da)
- 大分子 (多糖、蛋白) 需调整对接 / PK 部分
- 体内实验需符合本地 IACUC 与伦理要求

## License

MIT
