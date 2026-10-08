# Taxonomy 设计与打标质量

> 建立于 2026-10-09。校准协议基线见 [analysis-foundation](../../analysis-foundation/SKILL.md) 第六节。

## 一、Taxonomy 设计原则(MECE)

- **封闭词表 + 层级结构**;同层互斥(一条内容在同一 term set 只归一个标签)+ 整体穷尽(设"其他"兜底标签,并监控其占比——兜底>20% 说明词表该重设计);
- "one product, one place"(Earley);
- **每层标签数 ≤15–20**,超了就再分层或改 faceted(多维度正交标签,如 主题×情感×产品线 三个独立 facet);
- 兜底"其他"里聚集的内容要定期人工审,提炼新标签候补。

## 二、标签质量四指标(每次打标输出)

| 指标 | 定义 | 行动阈值 |
|---|---|---|
| 覆盖率 | 被打标内容 ÷ 总内容 | <90% 查规则 |
| 标签分布 | 各标签频次 | 超低频标签(<1%)合并;头部垄断(>60%)拆分 |
| 层间一致性 | 层级违反(子标签内容不在父标签内) | 零容忍 |
| 双遍一致性 | 同批打两遍的 agreement(kappa) | kappa<0.6 修词表或示例 |

## 三、LLM 打标校准协议

1. **gold set ≥50–100 条人工精标**(label-studio 模式,28,419★);
2. LLM 全量前先跑 gold:**一致性 >80% 才放开**;
3. **5–10% 抽样人工抽检**(行业惯例,非正式标准);
4. 一致性算 **Cohen's/Fleiss' kappa**(校正随机一致),不只看准确率;
5. **低置信标签路由人工**(置信度阈值可调,autolabel 的 confidence_threshold 机制);
6. 标签错误检测:cleanlab 思路(label quality score,11,690★)——低质量标签优先复核;
7. 规模化后续:标注 50–100 条即可用 setfit(2,836★)微调小分类器替代 LLM 全量。

## 四、打标输出纪律

- 每条标签带**证据(原文引句或字段引用)**——无证据不打标;
- 主题计数报分母(有效记录数)与各标签 n;
- 词表变更须重打全量或声明新旧不可比(口径锁定,同 foundation 第三节);
- 中文/多语言内容:先声明工作语言;跨语言标签做映射表(不是重翻)。

## 来源

- MECE/taxonomy 设计:NN/g Taxonomy 101、Earley "one product one place"
- gold set/kappa/disagreement:HumanSignal/label-studio(28,419★)、argilla(5,142★)
- 置信度路由:refuel-ai/autolabel(2,330★);标签噪声:cleanlab(11,690★);少样本微调:huggingface/setfit(2,836★)
- 本文件由 EveryInfra 编写,仅收录要点与链接
