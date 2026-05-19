# 体内药代动力学 (PK) 实验 SOP

> 在阶段 4 需要 PK 实验细节时加载本文件。

## 1. 实验前准备

### 1.1 动物选择

| 物种 | 适用 | 备注 |
|------|------|------|
| SD 大鼠 (200–250 g) | 常规 PK 首选 | 颈静脉插管可取多点血 |
| C57BL/6 小鼠 (20–25 g) | 与肿瘤模型 / 转基因匹配 | 总血量限制，每只通常只能取 3–4 点 |
| Beagle 犬 | 桥接临床、口服制剂 | 成本高，需 GLP 设施 |
| 食蟹猴 | IND-enabling | 监管必备 |

### 1.2 给药制剂

**IV 给药**

- 溶剂：生理盐水 / 5% 葡萄糖 / 10–20% HP-β-CD / 30% PEG400 + 5% Tween80 + 65% 盐水
- 浓度：通常 0.5–1 mg/mL，给药量 5 mL/kg
- 注射速度：尾静脉慢推 30–60 秒；插管动物可推注

**PO 给药**

- 溶剂：0.5% CMC-Na / 0.5% MC / 10% Solutol HS15 / 5% DMSO + 5% Tween80 + 90% (0.5% CMC)
- 浓度：2–10 mg/mL，给药量 10 mL/kg
- 灌胃针匹配体重 (大鼠 18G，小鼠 22G)

**预实验**：每个制剂用 LC-MS 测溶解度与稳定性，确认实际给药浓度。

### 1.3 剂量选择

- 参考体外 IC50 与计算预测的 Cl/F
- IV：1, 5 mg/kg；PO：10, 30, 100 mg/kg (剂量线性研究)
- MTD (Maximum Tolerated Dose) 通常 ≤ 1/10 LD50

## 2. 采血方案

### 2.1 大鼠 (颈静脉插管)

时间点 (IV, 0.5 mg/kg)：

```
0 (pre-dose), 2 min, 5 min, 15 min, 30 min, 1 h, 2 h, 4 h, 6 h, 8 h, 12 h, 24 h
```

时间点 (PO, 10 mg/kg)：

```
0, 15 min, 30 min, 1 h, 2 h, 4 h, 6 h, 8 h, 12 h, 24 h, 48 h
```

- 每点采血 ~200 μL，肝素钠抗凝 (10 IU/mL)
- 4°C 8000 rpm 离心 5 min 取血浆，-80°C 储存
- 总采血量 ≤ 动物总血量的 10% (大鼠约 1.5 mL/天上限)

### 2.2 小鼠 (sparse sampling)

每个时间点用独立动物 (n = 3)：

- IV：1 min, 5 min, 15 min, 30 min, 1, 2, 4, 8, 24 h
- 眼眶或心脏穿刺末次采血

## 3. 生物分析方法 (LC-MS/MS)

> 这是用户的专长领域，强调方法学验证按 FDA / EMA bioanalytical guideline。

### 3.1 方法开发要点

**色谱**

- 柱：Waters ACQUITY UPLC BEH C18 (2.1 × 50 mm, 1.7 μm) 或 Phenomenex Kinetex
- 流动相 A：0.1% 甲酸水 / 5 mM 乙酸铵 (pH 4–7 视化合物)
- 流动相 B：乙腈 / 甲醇 (0.1% 甲酸)
- 梯度：5% B → 95% B in 3 min，post-run 1 min
- 流速：0.4 mL/min；柱温：40°C
- 进样量：2–5 μL

**质谱**

- ESI+ / ESI- (视分子结构)
- MRM 多反应监测，选择最强 product ion
- 优化 declustering potential、collision energy、entrance potential
- 内标 (IS)：氘代物 (优先) > 结构类似物，注意排除离子抑制

### 3.2 样品前处理

| 方法 | 适用 | 回收率 |
|------|------|--------|
| 蛋白沉淀 (ACN/MeOH 1:3) | 通用、快 | 70–95% |
| 液-液萃取 (EA, MTBE) | 中等极性 | 60–90% |
| SPE (HLB, MCX) | 痕量 / 干扰多 | 80–100% |
| 在线 SPE | 高通量 | 类同 |

通常蛋白沉淀即可，但浓度低 (<1 ng/mL) 或有内源干扰时升级。

### 3.3 方法学验证 (FDA Bioanalytical Guidance 2018)

| 参数 | 要求 |
|------|------|
| **选择性** | 6 批空白血浆，干扰峰 < LLOQ 的 20%，IS 干扰 < 5% |
| **LLOQ** | S/N ≥ 10，准确度 80–120%，精密度 RSD ≤ 20% |
| **线性** | 6–8 浓度点，R² ≥ 0.99，权重 1/x² 常用 |
| **准确度** | LQC, MQC, HQC：85–115% (LLOQ 80–120%) |
| **精密度** | 日内、日间 RSD ≤ 15% (LLOQ ≤ 20%) |
| **基质效应** | IS-normalized MF：变异 ≤ 15% (6 批基质) |
| **回收率** | 一致性 (不要求高，但要稳) |
| **稳定性** | 室温短期 / 冻融 3 次 / 长期 -80°C 30 天 / 处理后自动进样器 |
| **稀释完整性** | 1:10 稀释 QC 准确度 85–115% |

### 3.4 ISR (Incurred Sample Reanalysis)

- 至少 10% 真实样品复测
- 67% 复测样品两次结果差异 ≤ 20% (PK 研究) / 30% (毒理研究)

## 4. 数据处理与 PK 参数计算

### 4.1 软件

- **Phoenix WinNonlin** (商业，标准)
- **R 包 PKNCA / NonCompart** (开源)
- **PKanalix** (Lixoft)

### 4.2 非房室分析 (NCA) 关键参数

| 参数 | 定义 | 计算 |
|------|------|------|
| Cmax | 最大血药浓度 | 实测 |
| Tmax | 达峰时间 | 实测 |
| AUC0-t | 0 至最后可测点 | 梯形法 |
| AUC0-∞ | 外推至无穷 | AUC0-t + Ct/λz |
| t1/2 | 末端消除半衰期 | 0.693/λz |
| CL | 清除率 (IV) | Dose / AUC0-∞ |
| Vss | 稳态分布容积 (IV) | CL × MRT |
| MRT | 平均滞留时间 | AUMC/AUC |
| F | 绝对生物利用度 | (AUC_PO × Dose_IV) / (AUC_IV × Dose_PO) × 100% |

### 4.3 房室模型 (Compartmental)

- 用 AIC / BIC 选择 1/2/3 房室
- 估计 ka, k10, k12, k21, V1, V2 等
- 用于剂量推演和靶 PK 建模

## 5. 组织分布 (Tissue Distribution)

### 5.1 设计

- 在 Cmax (如 0.5 h) 和 ~t1/2 (如 4 h) 取材
- 通常采集：肝、脾、肾、肺、心、脑、睾丸/卵巢、肌肉、脂肪、肿瘤 (如有)
- 每个时间点 n ≥ 3

### 5.2 处理

- 组织准确称重，加 PBS / 甲醇匀浆 (1:3 或 1:5 w/v)
- 后续同血浆样品前处理
- 结果以 ng/g 或 ng/mL (匀浆液) 报告
- 计算组织/血浆比 (Kp)

### 5.3 BBB 渗透判定

- 脑/血浆 AUC 比 > 0.3 视为可穿透
- 注意脑组织残血校正 (≈ 2% 血液污染)

## 6. 代谢物鉴定 (Metabolite ID)

### 6.1 实验设计

- 体外：肝微粒体 (HLM, RLM) + NADPH 孵育；或肝细胞 (3D primary)
- 体内：尿液 (0–24 h)、胆汁 (大鼠胆管插管)、粪便、血浆

### 6.2 分析

- 高分辨 Q-TOF / Orbitrap 全扫描 (MS¹)
- 数据依赖性 MS/MS (DDA)
- 软件：Mass-MetaSite / MetWorks / Compound Discoverer
- 推测代谢路径：Phase I (CYP 氧化 +16, +14, +2, -2)、Phase II (葡糖醛酸化 +176, 硫酸化 +80, 谷胱甘肽 +305)

### 6.3 关键代谢物结构确认

- 同位素 (¹³C / D / ¹⁴C / ³H) 标记
- 同位素峰簇辅助
- 合成标品比对
- 含偶氮、亚胺、N-O、CY3A4 介导的活性代谢物需重点关注

## 7. PK / PD 关联

- 同步采血和 PD biomarker (如肿瘤体积、cytokine、磷酸化蛋白)
- 暴露 - 应答 (Cmax/AUC vs. inhibition%) 建模
- Indirect response model (DERSE / Sheiner)
- 用于剂量预测和给药频次设计

## 8. 数据报告模板

```
化合物: NP-001
物种: SD 大鼠 (♂, n=6)
给药: IV 1 mg/kg, PO 10 mg/kg
制剂: IV 5% DMSO + 95% 盐水；PO 0.5% CMC-Na 混悬

主要 PK 参数 (mean ± SD):
              IV              PO
Cmax (ng/mL)  1850 ± 220      245 ± 58
Tmax (h)      0.03            0.5
t1/2 (h)      2.1 ± 0.3       2.4 ± 0.5
AUC0-∞ (h·ng/mL) 1420 ± 180  3650 ± 620
CL (L/h/kg)   0.70 ± 0.09     —
Vss (L/kg)    1.8 ± 0.3       —
F (%)         —               25.7

结论:
- 中等清除率，分布广泛 (Vss > 总体水)
- 口服生物利用度 25.7%，可接受
- t1/2 约 2 h，预计每日 2 次给药
- 与体外 IC50 (5 μM) 对比，10 mg/kg PO 时游离 Cmax (假设 fu = 5%) 可覆盖
```

## 9. 伦理与合规

- 所有动物实验须经 IACUC 批准
- 遵守 3R 原则 (Replacement, Reduction, Refinement)
- 安乐死方法：CO₂ / 戊巴比妥过量 / 颈椎脱臼 (小鼠)
- 数据存档 ≥ 5 年，原始记录可追溯
- 如用于 IND 申报，必须 GLP 设施
