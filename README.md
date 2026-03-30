# E-commerce Recommendation System Strategy & A/B Testing Simulation

[![Product Strategy](https://img.shields.io/badge/Product-PRD-blue.svg)]()
[![Data Analysis](https://img.shields.io/badge/Data-A/B%20Testing-brightgreen.svg)]()
[![Python](https://img.shields.io/badge/Python-Jupyter-orange.svg)]()

> 一个全链路 (End-to-End) 的电商推荐系统产品策略项目，包含完整的 PRD (产品需求文档) 以及基于 Python 的 Monte Carlo A/B 测试模拟 (A/B Testing Simulation)。

## 项目概述 (Project Overview)
本项目展示了针对电商平台推荐系统优化的核心产品策略。从用户场景拆解开始，设计了包含**冷启动 (Cold Start)** 和 **协同过滤 (Collaborative Filtering)** 的推荐分发逻辑，并最终通过统计学严谨的 A/B 测试数据模拟，验证了核心产品策略的有效性。

项目的终极目标是驱动核心业务指标的增长：
- **点击率 (Click-Through Rate, CTR)**
- **转化率 (Conversion Rate, CVR)**
- **平均客单价 (Average Order Value, AOV)**

同时，探讨在不同**样本量 (Sample Size)** 与**最小可检测效应 (Minimum Detectable Effect, MDE)** 的夹击下，如何制定科学的 Product Rollout (发版推全) 策略。

---

## 核心交付物 (Repository Structure)
- `PRD_Recommendation_System.md`: 完整的**产品需求文档 (PRD)**。详细定义了冷启动流量分发机制、基于 Item-CF 的算法推荐业务规则，以及诸如 Fatigue Control（疲劳度控制）的防护性业务边界场景。
- `ab_test_simulation.ipynb`: 一个交互式的 **Jupyter Notebook**。利用 Python 模拟用户全链路转化漏斗（曝光 -> 点击 -> 下单 -> 支付 GMV），并对不同的灰度测试流量场景进行了严格的假设检验（Chi-Square 独立性检验、独立样本 T-Test）。

---

## 核心产品策略 (Key Product Strategies)

### 1. 新客冷启动策略 (Cold Start for New Users)
* **Global Popularity & Category Diversity (全局热度与品类打散)**: 利用销量排行兜底池，并在前置展示位强制打散品类 (例如：3C、美妆、服饰混排)，有效避免算法 Filter Bubble (信息茧房) 带来的新客直接流失。

### 2. 基于用户行为的算法原型 (Behavior-based Item-CF)
* **“看了又看” (View-to-View)**: 面向用户决策比价链路。通过计算商品余弦相似度，推荐同叶子类目、价格带 (Price Band) 接近的商品。
* **“买了又买” (Buy-to-Buy)**: 面向提升客单价与连带率。基于历史同现订单 (Co-occurrence in orders) 计算概率，优先推荐能够跨品类产生购买欲的强互补品 (如：iPhone + 磁吸充电宝)。

---

## A/B 测试与数据模拟 (A/B Testing & Data Simulation)
在 Jupyter Notebook 中，使用了 `numpy` 和 `scipy.stats` 构建基于二项分布 (Binomial) 和对数正态分布 (Log-normal) 的流量漏斗，进而推算每一次改变变量后的 P-Value ($\alpha = 0.05$)。

本模拟深入刻画了推灰度实验时面临的 **三大典型业务场景 (3 Critical Business Scenarios)**：
1. **场景一 (小流量但微弱提升)**：转化率虽然微升，但在统计上 P-Value > 0.05。揭露了小样本下“伪增长”的危害，警示避免凭借随机波动噪音 (Random Noise) 草率发版。
2. **场景二 (大盘流量加持下的微弱提升)**：在 10 倍用户流量的长期累积支持下，证明了哪怕是极微弱的真实转化提升，也完全可以达到统计显著。这体现了一线大厂用大流量和时间对抗波动性的最真实业务场景。
3. **场景三 (算法代差的降维打击)**：模拟一次革命性的 Transformer 大模型迭代，产生极其夸张的 30%+ 真实转化跃升，证明了技术突破带来的断崖式效应可以无视长周期的流量积累，光速斩获显著性置信度。

---
## 总结 (Conclusion)

本项目的核心并不在于构建一个“更准的推荐算法”，而在于从产品视角出发，设计一个**可落地、可验证、可决策的推荐系统策略**。

在**产品层面**，本项目将推荐系统拆解为多个用户决策场景（如冷启动、比价阶段、连带购买阶段），并针对不同阶段设计差异化推荐逻辑，而非单一模型统一处理。这一设计强调：推荐系统的本质并不是算法优化问题，而是围绕用户行为路径的策略设计问题 (Strategy Design Problem)。

在**策略层面**，冷启动阶段优先采用 Global Popularity 与 Category Diversity 进行风险控制，而非过早引入个性化推荐，从而避免因模型不稳定导致用户流失。这体现了推荐系统在实际业务中的核心权衡：相关性 (Relevance) 与稳定性 (Stability) 的平衡。

在**数据层面**，本项目通过 Monte Carlo 模拟构建完整 A/B 测试框架，重点不在于单次显著性检验，而在于刻画不同样本量 (Sample Size) 与最小可检测效应 (MDE) 下的决策边界。实验结果表明：统计显著性不仅取决于效果大小，还高度依赖流量规模与实验周期，这也是实际业务中灰度发布策略设计的关键依据。

**整体而言，本项目强调：**

推荐系统的核心不只是提升预测准确率，而是在不确定性环境下，通过数据驱动的方法做出稳定且可扩展的产品决策 (Data-driven Product Decisions under Uncertainty)。

---
## 技能树 (Tech Stack & Skills)
- **Product Management (产品管理)**: PRD Writing, Scenario Design, Funnel Optimization, Agile Rollout Strategy
- **Data & Statistics (数据分析与统计)**: Hypothesis Testing (卡方检验, T-Test), Monte Carlo Simulation (蒙特卡洛模拟), MDE (最小可检测效应分析)
- **Tools**: Python 3.x, `Pandas`, `Numpy`, `scipy.stats`, Jupyter Notebook

