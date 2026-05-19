# 🌿 植物次生代谢物药用评估 / Phytomet-Pharma-Eval

植物次生代谢物药用价值标准化评估 Agent Skill —— 输入一个化合物（SMILES 或名称），自动生成四阶段评估流程：结构鉴定 → 体外药效初筛 → 靶点预测与分子对接 → ADMET 与体内 PK。

适用于天然产物药物发现、CRO 立项、SAR 优化、综述撰写等科研场景。

A standardized research-workflow Agent Skill for evaluating the pharmaceutical potential of plant secondary metabolites. Given a compound, it generates a four-stage funnel: structure ID → in vitro bioactivity → target prediction & docking → ADMET & in vivo PK — with explicit Go/No-Go criteria at every stage.

遵循 [Agent Skills 开放标准](https://agentskills.io)，兼容 Claude Code、Cursor、GitHub Copilot、Codex、Windsurf、Gemini CLI、Perplexity Computer 等 30+ AI Agent 平台。

## 安装 / Install

```bash
npx skills add Ficere/phytomet-pharma-eval
```

> 需要 Node.js。安装后 Agent 会自动发现并按需加载该技能。
>
> Requires Node.js. Once installed, your agent will auto-discover and load this skill when relevant.

<details>
<summary>其他安装方式 / Alternative methods</summary>

**手动安装 / Manual install：**

```bash
git clone https://github.com/Ficere/phytomet-pharma-eval.git
# 将整个目录复制到你的 Agent 的 skills 目录下即可
# Copy the directory to your agent's skills folder:
#   Claude Code:  ~/.claude/skills/
#   Cursor:       .cursor/skills/
#   Copilot:      .github/skills/
#   Codex:        ~/.codex/skills/
#   Gemini CLI:   .gemini/skills/
```

**Perplexity Computer：**

下载本仓库 zip → 在 [Skills 管理页面](https://www.perplexity.ai/computer/skills) 上传。

</details>

## 使用 / Usage

安装后直接用自然语言触发，无需任何配置：

```
帮我评估一下姜黄素（curcumin）的抗肿瘤药用潜力，从结构到 PK 完整走一遍
```

```
这是 SMILES：CC(=O)Oc1ccccc1C(=O)O，按四阶段漏斗判断是否值得立项
```

```
我有 5 个黄酮类化合物，做一张横向决策矩阵，告诉我先推哪个
```

```
帮我设计大鼠口服 PK 实验方案，化合物 LogP 3.2、水溶性差
```

```
对这个生物碱做靶点反向预测，给出 top 3 靶点 + 分子对接 + MD 验证方案
```

## 功能 / Features

| 阶段 | 模块 | 说明 |
|------|------|------|
| **阶段 1** | 结构鉴定 | HRMS / 1D & 2D NMR / X-ray / ECD 方案，PubChem · ChEMBL · COCONUT · TCMSP 去重，PAINS 过滤 |
| **阶段 2** | 体外药效初筛 | 抗肿瘤（MTT/凋亡/周期/克隆形成）· 抗炎（LPS·RAW264.7、NF-κB）· 抗氧化（DPPH/ABTS/ORAC、ROS、Nrf2）SOP |
| **阶段 3** | 靶点预测 + 分子对接 | SwissTarget · SEA · PharmMapper 取交集；Vina / GNINA / DiffDock + MM-GBSA + GROMACS MD + FEP |
| **阶段 4** | ADMET + 体内 PK | SwissADME · ADMETlab 3.0 · pkCSM · ProTox；大鼠/小鼠 IV/PO 设计 + LC-MS/MS 方法学验证 + NCA |
| **横向** | 决策矩阵 | 多化合物 IC50 · docking · F% · LE · LipE 综合排序，输出立项优先级 |
| **报告** | 输出模板 | 摘要 · 表征 · 活性 · 机制 · ADMET/PK · SWOT · Go/No-Go · 参考文献 七段式 |

每个阶段都有明确的 **Go / No-Go 决策阈值**，避免在低质量化合物上浪费资源。

<details>
<summary>四阶段漏斗与决策标准 / Four-stage funnel & Go-NoGo criteria</summary>

| 阶段 | 关键产出 | ✅ Go | ⚠️ 待定 | ❌ No-Go |
|------|----------|-------|---------|----------|
| 1. 结构鉴定 | SMILES、纯度、理化参数 | 结构明确，纯度 > 95% | 异构体未分开 | PAINS / Frequent Hitter |
| 2. 体外药效 | IC50 / EC50、SI、剂量-反应曲线 | IC50 < 50 μM 且 SI ≥ 3 | IC50 50–100 μM，可做 SAR | 所有模型 > 100 μM 或通用毒性 |
| 3. 靶点 + 对接 | 靶点列表、docking score、MD 稳定性 | 合理靶点 ≤ -7 kcal/mol，MD 稳定 | 单一弱靶点 | 全部 > -5 或机制无法解释表型 |
| 4. ADMET + PK | F%、t1/2、CL、Vss、毒性预警 | F > 10%、t1/2 > 1 h、无严重毒性 | F 低但可优化制剂 | hERG 强阻断、肝毒性确证 |

</details>

<details>
<summary>决策矩阵示例 / Decision matrix example</summary>

| 化合物 | 纯度 | best IC50 | top 靶点 / docking | F% | LE | LipE | 优先级 |
|--------|------|-----------|---------------------|-----|------|------|--------|
| Cpd-A | 98% | 5 μM (HepG2) | EGFR / -9.2 | 12% | 0.35 | 5.1 | ⭐⭐⭐ |
| Cpd-B | 95% | 18 μM (RAW) | COX-2 / -7.8 | 28% | 0.30 | 4.2 | ⭐⭐ |
| Cpd-C | 92% | 75 μM | — | — | — | — | × |

LE = -ΔG / 重原子数，目标 ≥ 0.3 ; LipE = pIC50 - LogP，目标 ≥ 3。

</details>

## 目录结构 / Structure

```
phytomet-pharma-eval/
├── SKILL.md                          # 技能入口：四阶段框架 + Go/No-Go 决策（Agent 自动读取）
├── references/
│   ├── in_vitro_assays.md            # 抗肿瘤 / 抗炎 / 抗氧化 SOP（细胞系、剂量梯度、QC）
│   ├── docking_md_protocol.md        # Vina · GNINA · DiffDock + GROMACS MD + MM-GBSA + FEP 参数
│   ├── in_vivo_pk_sop.md             # 大鼠/小鼠 PK + LC-MS/MS 方法学验证（FDA 2018）+ NCA
│   └── tools_databases.md            # 30+ 数据库与工具速查（COCONUT · TCMSP · ADMETlab 等）
├── LICENSE
└── README.md
```

## 适用范围 / Scope

- 适用于小分子代谢物（MW < 1000 Da）：生物碱、黄酮、萜类、酚酸、皂苷、香豆素等
- 大分子（多糖、多肽、蛋白）需调整对接与 PK 部分
- 体内实验需符合本地 IACUC 与伦理要求

## 免责声明 / Disclaimer

本技能输出为科研工作流参考，不构成医疗、用药或药物开发的最终决策依据。所有体内实验须经动物伦理委员会（IACUC）批准；任何临床转化须遵守相应监管法规（NMPA / FDA / EMA）。计算预测仅供假设生成，结论必须经实验验证。

This skill outputs a research-workflow reference only and does not constitute medical, pharmaceutical, or drug-development advice. All in vivo experiments must be approved by an animal ethics committee (IACUC); any clinical translation must follow applicable regulatory frameworks (NMPA / FDA / EMA). Computational predictions are for hypothesis generation only — conclusions must be validated experimentally.

## License

MIT
