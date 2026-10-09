# Gold-Standard 样例输出:review-insights(合成数据)

> 用途:展示本仓库分析 skill 的**交付标准**——七段式结构(标题=答案/The answer 独立成立/带 n 的数字/不确定度/可推翻因素/方法附注)。数据为合成,仅示范格式与纪律。真实输出按 analysis-foundation 的四步流水与统计纪律生成。

# 配送延迟是最大可修痛点:3 个月 1,204 条评论中占 31%(n=374),修复优先级高于价格抱怨的 4 倍

_For: 电商运营负责人 · Date: 2026-10-09 · Scope: 亚马逊美国站 ASIN B0XXXX,2026-07-01~09-30,3 个月_

## The answer

延迟类抱怨占有效评论 31%(374/1,204),且集中在 8 月后(月环比 +58%)——与切换新承运商的时间点吻合但未证实因果。修复延迟预计影响面是价格类(8%)的约 4 倍。置信度:高(样本量大+aspect 抽取与人工 gold set 一致性 87%)。

## Key numbers

| 指标 | 数值 | 分母/阈值 |
|---|---|---|
| 有效评论 | 1,204 | 原始 1,388,剔除近重复 142+空评 42 |
| 延迟类(aspect=shipping_delay) | 31%(374) | n 充分 |
| 质量缺陷类 | 22%(265) | |
| 客服响应类 | 12%(145) | 8 月后占比翻倍 |
| 价格类 | 8%(96) | |
| 抽取一致性(kappa) | 0.74 | gold set n=120,>80% 准确率门槛通过(kappa 0.6+) |

## Pain points(每条带引文,可回溯)

| Aspect | 极性 | 严重度 | 频次 | 代表引文(合成) |
|---|---|---|---|---|
| shipping_delay | neg | major | 374 | "Two weeks past the delivery window, no update" |
| defect_rate | neg | major | 265 | "Arrived with cracked housing" |
| support_response | neg | minor | 145 | "Took 5 days to reply" |

## Rating-sentiment divergence

4–5 星但负情愫:41 条(3.4%)——多为"产品好但物流糟"结构;**未发现刷单特征**(高分差评占比正常区间)。

## Recommendation(选项表,选择权在 owner)

| Option | Expected gain | Cost/effort | Confidence |
|---|---|---|---|
| 承运商切换回退+滞后补偿券 | 延迟抱怨 −30~50%(区间) | 2 人周+券成本 | 中 |
| 缺陷抽检加严(批次级) | 质量类 −15~25% | 1 人周 | 中 |
| 客服 SLA 改 24h | 该类 −40% | 流程改动 | 低(量小) |

## What could change this conclusion

- 样本为完成购买者(MNAR):沉默不满者未入样——真实不满率可能更高;
- 8 月跳变与承运商切换仅时间相关;定案实验:分仓 A/B 两承运商 4 周对比;
- 近重复剔除阈值若放宽,延迟类频次 ±6%。

## Method Notes

- 数据:CSV 导出 1,388 行(2026-10-08 拉取);去重键=评论文本 simhash;缺失处理=剔除并计数;
- 抽取:聚类→LLM 结构化(aspect/polarity/severity/quote),gold set n=120 人工校验;
- 全部数字由脚本计算;引文可回溯到 review_id。
