---
name: analysis-foundation
description: Shared analysis discipline layer for all EveryInfra analysis skills. Use before or alongside any data analysis task: numbers must come from executed code, denominators must be named, uncertainty must be reported, correlation must not be worded as causation. Provides the data-profiling step, statistics checklist, metric-definition rules, chart-choice table, and the method-notes template that every analysis output must carry. Read this when analyzing CSV/JSON with an LLM, when results will be reported to stakeholders, or when numbers look surprising.
---

# Analysis Foundation(分析纪律层)

所有分析 skill 的公共地基。核心立场:**LLM 只做叙述,数字必须由代码算出**——实证:RAG 场景下 LLM 数值抽取召回可低至 25.7%(ACM 2026);450+ 真实分析任务基准 DABstep 上最强 agent 准确率仅 ~16%,首要失败模式就是"一步作答而不先看 schema"。

## 一、四步流水(强制顺序,禁一步出数)

1. **画像(profiling)**:先跑数据画像——行数/列类型/缺失分布/重复键/数值范围(30 秒内,代码完成)。画像改变后续一切假设。
2. **过滤**:精确条件(字段/运算符/值)+ 去重键;**缺失 ≠ 0**(缺失是缺失,零是零)。
3. **聚合**:分组键+聚合函数+时间粒度与时区写明;聚合后做**二次校验**(sum of parts = total)。
4. **验证**:关键数字用第二种独立方法重算一致才可入报告;代码执行失败即停,不得脑补结果。

## 二、数字与统计纪律(每条输出前过一遍)

- 叙述中出现的每个数字,必须能在工具输出中找到出处;心算/目测数字=最严重失败。
- **每个 % 同时报绝对数与分母 n**;点名分母(事故案例:同一数据 2% vs 32%,差异全在分母口径)。
- **n<30 只报计数不报率**;组间比较两组 n 都要达标。
- 报**不确定度**:置信区间或误差范围+置信水平(n=200→±7.1%,n=4,000→±1.6%,Pew 模式);**差异小于误差范围时禁止说"更高/更低"**。
- 偏态数据(收入/时长)均值**并报中位数**。
- 时间序列:YoY 优先于 MoM;强季节性须季调或同比;异常值剔除必须说明标准。
- **措辞纪律**:观察数据只配 "is associated with",只有实验/准实验设计(RCT/DID/IV)才配 "causes";摘要句只许用链条中最弱的因果词。
- Simpson 检查:分层后关系是否反转;多重比较:报告找到该结果前看了多少个检验;回归均值:对"最差/最优"组的前后对比天然可疑。
- 幸存者偏差:完成者指标并排报"of all who started / of those who reached";入口过滤器会静默丢掉最弱用户(事故:≥10min 活跃阈值排除 43% 弱用户)。
- 缺失机制三问:不存在/没记录/因结果而缺失(MNAR——"愤怒者才写评论"即 MNAR);处理方式(删行/插补/缺失指示)写明并给理由。
- 基准先行:92% 准确率在多数类占 90% 时无意义。
- 效果量门槛事先声明并全程一致(小样本收紧):|d|≳0.2、RR≳1.5、|r|≳0.1。
- 零结果是真实结果,不许隐藏;被驳倒的假设记入 ledger(refuted)。

## 三、指标定义纪律

- **派生指标必须给公式**:分子+分母+时间窗+纳入/排除。例:engagement rate 无全球标准——分母可以是 followers/reach/impressions,**结果差数倍**;不写公式=不可比。
- **口径锁定**:同一份分析内不得静默换分母;换口径须重算全部历史。
- 同行基准必须带:来源+发布日期+平台/行业分段+样本说明;无来源的"行业平均"禁止输出。
- **口径溯源脚注**(每个交付数字可附):口径层级(metric store>固化 SQL>周报>临时手写——最底层必须显式标"请复核")、数据新鲜度、源表、校验人。

## 四、图表决策表(常见错配即失败)

| 分析意图 | 推荐 | 禁用 |
|---|---|---|
| 对比 | 条形/分组条形 | 类别过多用折线 |
| 趋势 | 折线/面积(x=时间,≥3 点) | **截断 y 轴**;类目轴用折线 |
| 分布 | 直方图/箱线 | 条形图冒充分布(丢形状) |
| 构成 | 饼图 ≤5 块、堆叠条;超 5 块改 100% 堆叠/树图 | 饼图>5 块;3D 饼 |
| 关系 | 散点(+拟合线);双类目用热力 | 点数<10 画趋势线 |

条形图 y 轴从 0 开始;双轴图默认禁用;截断轴与失真纵横比同样骗过视觉模型(arXiv 2508.09716)。

## 五、方法附注模板(每次分析输出必须携带)

```
数据: 来源文件+版本/哈希; 过滤前 N0 → 过滤后 N1
过滤: 精确条件、去重键、缺失值处理
聚合: 分组键、函数、时间粒度与时区
指标: 派生指标公式(分子/分母)
异常: 被剔除的异常值及判定标准
环境: 生成时间戳、模型/工具及版本
局限: 覆盖偏差、不可外推的场景
```

(结构对齐 REFORMS 32 项清单与 AAAI 可复现清单的适用子集。)

## 六、LLM 打标/抽取的校准协议(供 content-analysis-tagging 与 review-insights 共用)

- 建 **gold set**(人工精标 50–100 条);LLM 与 gold 一致性 **>80%** 才放开全量。
- **5–10% 抽样人工抽检**(行业惯例,非正式标准);一致性用 Cohen's/Fleiss' kappa,不只看准确率。
- 低置信标签路由人工(置信度阈值);标签错误检测可借 cleanlab 思路(label quality score)。
- LLM 输出结构化 JSON 时**必须带引文原文**(可回溯=防幻觉)。

## 七、数据合理性速查(空结果/异常的根因清单)

- SQL/聚合空结果根因:ID 类型不匹配、日期格式、JOIN 键错、时区错位;
- JOIN 膨胀:`COUNT(DISTINCT) ≠ COUNT` 必查;
- CSV/JSON 常见:表头重复、BOM、数字带千分位存成字符串、布尔的多种写法、嵌套数组摊平后行数暴涨。

## 来源

- 数值幻觉召回 25.7%:ACM 3805712.3809882(2026);多步分析失败:DABstep arXiv:2506.23719;因果措辞:CORR2CAUSE arXiv:2306.05836;误导图:arXiv:2508.09716
- 统计纪律:BBC 统计报道指南、Pew 误差范围模式、MeasuringU 小样本指引、Journalist's Resource
- 方法附注:REFORMS(reforms.cs.princeton.edu)、AAAI-26 可复现清单
- 结构借鉴:anthropics/skills(xlsx 重算门禁/验证闭环)、tronghieu/agent-skills data-scientist 目录范式、gaasher/Agent-Loop-Skills(ledger/验证门)、retentioneering-tools(事故库)、fafa-ai-data-lab(口径溯源脚注)、TerryFYL(先诊断后分析)
- 本文件由 EveryInfra 编写,仅收录要点与链接
