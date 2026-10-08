# 评论挖掘:aspect 优先与混合管线

> 建立于 2026-10-09。纪律基线见 [analysis-foundation](../../analysis-foundation/SKILL.md)(本文件只写领域层)。

## 一、三种主题抽取路线的取舍

| 路线 | 优点 | 缺点 | 适用 |
|---|---|---|---|
| LDA | 便宜、可复现 | bag-of-words 无语义 | 快速粗扫 |
| **BERTopic**(embedding+UMAP/HDBSCAN,7,872★) | coherence/diversity 稳定胜 LDA/NMF;自带层级/动态主题与离群点检测 | 需 embedding 计算 | 需要统计严谨时的默认项 |
| LLM 直接抽取 | 从脏文本直接拿结构化字段(aspect/极性/严重度) | 按条计费;有幻觉风险 | 低量/原型/打标-摘要 |

**混合管线是主流**:聚类(便宜)→ LLM 打标/摘要(准确)→ 主题计数。

## 二、ABSA(aspect-based sentiment)——痛点挖掘的正确抽象

先抽 aspect(电池/物流/尺码)再定极性,比全文情感有用得多。输出 schema(四元组,借 ABSADatasets 任务定义):

```json
{"aspect": "battery", "polarity": "negative", "severity": "major|minor", "quote": "引文原文(必填,防幻觉)"}
```

- 固定 aspect 词表 + few-shot 示例;引文可回溯到原评。
- zero-shot LLM 可做原型,一致性不如微调模型(arXiv 2412.12564 等);商业管线常见"LLM 引导标注→微调小模型"——skill 层(无微调)用 gold set 校准替代(>80% 一致性门槛,见 foundation 第六节)。
- 情感 3 分类 + 置信度输出;短文本可用 VADER 类词典做基线(5,077★)。

## 三、评论数据的统计陷阱(领域特有)

1. **MNAR(因结果而缺失)**:"愤怒者才写评论"——评论样本对总体有系统性偏差,结论必须带"覆盖偏差"声明。
2. **评分-情感背离检测**:高分差评/低分好评是可疑信号(刷单/胁迫好评/答非所问);并排报评分分布与情感分布。
3. **变体/批次特异性问题**必须按 SKU/时间窗切片,不合并下结论。
4. 平台偏差:各平台评论文化不同(日=克制、美=极端化),跨平台对比须声明。

## 四、大规模流程(skill 内可实现)

1. 去重(近重复文本)+ 过滤(空评/机器评);
2. BERTopic 或简单聚类分组;
3. 每组 LLM 结构化抽取(aspect/极性/严重度/引文);
4. 主题计数 + 代表性引文(每主题 2–3 条,选最长/最具体);
5. 输出带 n 与占比(分母=有效评论数);**修建议按 痛点频次×严重度 排序,标注"待验证假设"**。

## 来源

- 路线取舍:2025–26 社区共识 + MaartenGr/BERTopic(7,872★)
- ABSA schema:songyouwei/ABSA-PyTorch(2,115★)、yangheng95/ABSADatasets(246★);中文场景:Meituan-Dianping/asap(359★)
- 词典基线:cjhutto/vaderSentiment(5,077★);方法索引:xiamx/awesome-sentiment-analysis(933★)
- LLM zero-shot 局限:arXiv 2412.12564 等
- 本文件由 EveryInfra 编写,仅收录要点与链接
