# 体外药效活性筛选详细 SOP

> 在阶段 2 需要具体实验细节时加载本文件。

## 1. 抗肿瘤活性筛选

### 1.1 MTT / CCK-8 增殖抑制实验

**细胞系推荐组合 (NCI-60 简化版)**

| 类型 | 细胞系 | ATCC 编号 | 培养基 |
|------|--------|-----------|--------|
| 肝癌 | HepG2 | HB-8065 | DMEM + 10% FBS |
| 乳腺癌 | MCF-7 | HTB-22 | DMEM + 10% FBS |
| 肺癌 | A549 | CCL-185 | F-12K + 10% FBS |
| 结肠癌 | HCT-116 | CCL-247 | McCoy's 5A + 10% FBS |
| 黑色素瘤 | A375 | CRL-1619 | DMEM + 10% FBS |
| 白血病 | HL-60 | CCL-240 | IMDM + 20% FBS |
| **正常对照** | LO2 / HEK293 / WI-38 | — | 同源对照 |

**操作流程 (CCK-8 为例)**

1. 对数生长期细胞，胰酶消化、计数
2. 96 孔板接种 5×10³–1×10⁴ 细胞/孔，100 μL，过夜贴壁
3. 弃旧液，加含化合物的新鲜培养基 100 μL (5–7 个浓度 + 阴阳对照 + 空白)
4. 培养 48 h (或 24/72 h，看研究目的)
5. 每孔加 10 μL CCK-8 试剂，37°C 孵育 1–4 h
6. 酶标仪 450 nm 测 OD，参考波长 600 nm
7. 抑制率 = (OD_对照 - OD_样品) / (OD_对照 - OD_空白) × 100%
8. GraphPad Prism: log(inhibitor) vs. normalized response - Variable slope 拟合 IC50

**质量控制**

- Z' factor ≥ 0.5
- 阳性对照 IC50 与文献一致 (±2 倍以内)
- DMSO 终浓度 ≤ 0.1%，且空白组与对照组无显著差异

### 1.2 凋亡检测 (Annexin V-FITC/PI 双染)

- 处理浓度：通常选 IC30, IC50, 2×IC50 三个浓度
- 处理时间：24–48 h
- 流式：Annexin V+/PI- 为早凋；Annexin V+/PI+ 为晚凋/坏死
- 分析至少 10,000 个事件

### 1.3 细胞周期 (PI 单染)

- 70% 冷乙醇固定过夜
- RNase A 处理 30 min
- PI 染色，流式 488 nm 激发
- ModFit / FlowJo 分析 G1/S/G2-M 百分比

### 1.4 克隆形成 (Long-term)

- 6 孔板每孔接种 500–1000 细胞
- 含药培养基处理 24 h 后换正常培养基
- 培养 10–14 天至形成肉眼可见克隆
- 4% PFA 固定、结晶紫染色、计数 (≥50 细胞为一个克隆)

## 2. 抗炎活性筛选

### 2.1 LPS / RAW264.7 经典模型

**步骤**

1. RAW264.7 接种 24 孔板，5×10⁵/孔
2. 化合物预孵育 1 h
3. 加 LPS (终浓度 100 ng/mL 或 1 μg/mL，Sigma L2630 来源 E. coli O111:B4)
4. 培养 24 h
5. 收上清测 NO (Griess 法) / TNF-α / IL-6 / IL-1β / PGE2 (ELISA)
6. 收细胞做 Western blot (iNOS, COX-2, p-p65, p-IκBα) 或 qPCR

**关键控制**

- 排除细胞毒性：用 MTT 在相同浓度下测 RAW264.7 存活率 (CC50 应 ≥ 10×IC50)
- 阳性对照：地塞米松 (1 μM) 或 L-NAME (NO 抑制)

### 2.2 进阶机制实验

- **NF-κB 报告基因**：HEK293-NF-κB-Luc 稳转株 + TNF-α / IL-1β 激活
- **MAPK 通路**：Western blot p-ERK, p-JNK, p-p38
- **NLRP3 炎症小体**：BMDM + LPS priming + ATP / nigericin → 测 IL-1β、Caspase-1 p20

## 3. 抗氧化活性筛选

### 3.1 化学法 (无细胞)

**DPPH 自由基清除**

- 100 μM DPPH 甲醇溶液 100 μL + 样品 100 μL，避光反应 30 min
- 517 nm 测吸光度
- 清除率 = (1 - A样品/A对照) × 100%
- EC50 与 Vc / Trolox 比较

**ABTS·⁺**

- ABTS 7 mM + K₂S₂O₈ 2.45 mM 暗处过夜生成 ABTS·⁺
- 稀释至 OD734 ≈ 0.70
- 加样品 30 min 后测 734 nm

**FRAP (铁还原力)**

- TPTZ + FeCl₃ + 醋酸缓冲液 (pH 3.6)
- 37°C 反应，测 593 nm

**ORAC**

- AAPH 产生过氧自由基，荧光素探针
- 报告 Trolox 等效值 (μmol TE/g)

### 3.2 细胞法

**H₂O₂ 诱导 HepG2 / HUVEC 氧化损伤**

1. 预处理化合物 24 h
2. 加 H₂O₂ (200–500 μM) 处理 2–4 h
3. 测 CCK-8 看保护率
4. DCFH-DA (10 μM, 30 min) 染色 → 流式或共聚焦测胞内 ROS
5. 试剂盒测 MDA、SOD、CAT、GSH/GSSG

### 3.3 Nrf2/ARE 通路验证

- ARE-Luc 报告基因
- 核蛋白 Nrf2 (Western)
- 下游 HO-1, NQO1, GCLC 的 qPCR / WB

## 4. 数据处理与统计

- 至少 3 次独立实验 (n ≥ 3)，每次 3 复孔
- 正态性检验 (Shapiro-Wilk) → 两组 t 检验 / 多组 one-way ANOVA + Tukey
- 非正态用 Mann-Whitney / Kruskal-Wallis
- IC50 报告 95% CI 和 Hill slope
- 图表用 GraphPad Prism 或 R (ggplot2)，注明误差类型 (SD/SEM)

## 5. 常见陷阱

| 现象 | 可能原因 | 解决 |
|------|----------|------|
| IC50 极低 (<0.1 μM) 但无明显机制 | 化合物聚集 / 荧光干扰 | 加 0.01% Triton X-100 复测；换比色法 |
| 不同细胞系 IC50 完全相同 | 通用毒性 (membrane lytic) | 加 LDH 释放、膜完整性检测 |
| 浓度-反应曲线陡 (Hill > 2) | 协同 / 聚集 | DLS 测粒径；稀释血清 |
| 阳性对照失效 | 试剂降解 / 细胞污染 | 重做 STR 鉴定、支原体检测 |
| 抗炎组 NO 抑制但 cell viability 也降 | 细胞毒性假象 | 用 IC10 浓度重测 cytokine |
