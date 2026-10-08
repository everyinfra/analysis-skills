# 选品加权评分与价格分析

> 建立于 2026-10-09。纪律基线见 [analysis-foundation](../../analysis-foundation/SKILL.md)。

## 一、加权评分选品(MCDA 四步)

1. **定准则**:利润率/需求信号/竞争度/供应商可靠性/物流成本(或按任务声明的准则);
2. **定权重**:简单分配(权重和=1)或 AHP 两两比较;**权重可调、输出附敏感性说明**(权重±10% 时名次是否翻转);
3. 各品按准则 **1–10 打分**(每分带依据,可回溯到源数据字段);
4. 加权求和排名。

**量纲陷阱**:WSM(加权和)对量纲敏感——跨品类对比先归一化(min-max 或 z-score),或改用加权积模型(WPM)。**每个入选理由必须带可复算数字**(verified/refuted 短名单机制)。

## 二、dropshipping 可行性五维(直接可用的准则集)

margin(利润率)/重量(物流)/易碎(退货风险)/退货风险/营销可行性——各 1–10,nexscope 模式。

## 三、价格分布分析(三段模板)

按 **budget/mid/premium** 三段输出:

| 段 | 市场占比 | 竞争密度 | 价差倍数 |
|---|---|---|---|

再做:**价格缺口(price gap)** 定位(哪些价位段供给稀疏)与 **feature-price 错配**分析(某功能只出现在高价段但成本低)。

## 四、价格历史指标(Keepa 数据模型为事实标准)

| 指标 | 定义 |
|---|---|
| 价格波动率 | 价格的 CV(标准差/均值) |
| 折扣深度 | 现价 vs 12 个月高点 |
| Buy Box 占比 | 时间窗口内持有 Buy Box 的比例 |
| 促销周期性 | 折扣事件的时间聚集(如 Prime Day/黑五) |

(Keepa 官方称覆盖 70 亿+ 商品——数据源事实;无权威免费数值基准,不输出"行业平均"。)

## 五、变体分组与类目归一

- 变体分组(颜色/容量/套装)不混合比价;分组键显式声明;
- 类目归一可挂 **Google Product Taxonomy**(官方公开 5,000+ 类目树)——google-taxonomy-matcher(63★)模式;
- 缺失价格/库存 **≠ 0**:缺失标 gap。

## 来源

- MCDA/WSM/WPM 与 AHP:多准则决策标准方法
- 三段定价模板/五维可行性:nexscope-ai/eCommerce-Skills(1,098★)
- Keepa 指标定义:Keepa 数据模型(价格/sales rank/Buy Box 三时间线)
- 类目归一:BernhardWenzel/google-taxonomy-matcher(63★);Google Product Taxonomy 官方
- 本文件由 EveryInfra 编写,仅收录要点与链接
