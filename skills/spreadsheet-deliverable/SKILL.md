---
name: spreadsheet-deliverable
description: Deliver analysis results as an editable .xlsx workbook whose numbers are live formulas tied to clearly marked inputs, not pasted values. Use when the user asks for Excel or spreadsheet output, a scoring or financial model, or a file other people will keep editing. Covers input/calculation/output separation, recalculating and scanning for error values before delivery, reading formulas versus cached values, version compatibility, and built-in checks. Not for plain CSV/JSON exports or markdown tables.
---

# Spreadsheet Deliverable(xlsx 交付纪律)

本 skill 由 EveryInfra 依据公开的电子表格建模规范(ICAEW《Financial Modelling Code》)和 openpyxl、Microsoft 的公开文档独立编写,适配本仓库的分析场景。与 [analysis-foundation](../analysis-foundation/SKILL.md) 配合:数字先由代码算出并核对,工作簿是把这些数字交给别人继续用的可编辑载体。

## 一、结构:输入 → 计算 → 输出

- 输入(假设)、计算、输出分开放:分不同工作表,或在同一表内划清区块;逻辑从上到下、从左到右流动,时间序列横向排列。
- 每个输入值只在一个位置出现,所有用到它的公式都引用这一格,不在多处重复录入同一个假设。
- 输出区(结论、看板)只放公式结果;确需放在看板上的关键输入要明确标出。
- 第一个工作表做封面:用途、目录、口径与单位、数据来源与取数时间、生成时间、方法附注(见 foundation 第五节)。

## 二、公式与取值

1. **结果写成公式,不写死数字**:合计、比率、加权分都用公式引用上游单元格,改一个输入,下游全部跟着变。代码算出的结果只拿来核对公式,不粘贴进计算区。
2. **公式里不夹常数**:税率、权重、换算系数放进输入区再引用;确需常数(如一年 12 个月)时在旁边注明。
3. **同一行或同一列的公式保持一致**:中途换写法最容易藏错,确有例外要单独标注。
4. **不藏东西**:不隐藏工作表和行列,不用白字或不显示的数字格式;需要收起的内容用分组。
5. **尽量不跨工作簿链接**;必须用时集中放在一个链接页。

## 三、交付前:重算与错误扫描

- openpyxl 这类库只把公式文本写进文件,不负责计算。文件里没有计算结果时,很多预览器和按缓存值读取都会看到空值,所以交付前要用真正的电子表格软件(Excel,或无界面模式的 LibreOffice)打开、重算并保存。
- 重算后逐格扫描错误值(`#REF!`、`#DIV/0!`、`#VALUE!`、`#NAME?`、`#N/A`、`#NUM!`、`#NULL!`),数量为零才交付;扫描结果(公式数、错误数、错误位置)留档。
- 零错误只说明公式算得出来,不说明算得对:抽查几个合计和比率,和代码算出的数对一遍。
- 读别人的工作簿分两遍:openpyxl 默认读到公式文本,`data_only=True` 读到上次保存时的计算结果;审公式用前者,对数用后者。以 `data_only=True` 打开的工作簿不要存回原文件,否则公式会被结果值覆盖。

## 四、兼容性

- 先问清接收方用什么打开(Excel 哪个版本、WPS、LibreOffice、Google 表格)。较新的函数在文件里带 `_xlfn.` 前缀存储(如 XLOOKUP),不认识它的软件会显示这个前缀并返回 `#NAME?`;没有把握时换成老版本也支持的写法,例如用 INDEX/MATCH 代替 XLOOKUP。
- 日期存成日期类型,不存成文本;百分比存小数(0.15)再设百分比格式,不要存成 15。
- 交付前在接收方会用的软件里实际打开一次,确认函数、条件格式和字体都正常。

## 五、格式与标注

- 输入单元格用统一的填充色和/或边框标出,不要只靠字体颜色区分;封面放一份样式图例(输入、计算、链接、待使用者填写)。
- 每个数字都有单位(元、%、件、天),标签写清口径;正负号约定统一(例如成本记正还是记负),写在封面。
- 假设旁边注明来源(报告名和页码或链接、取数日期);暂时没有来源的标「待补来源」,与 foundation 的 [要追加] 协议一致。
- 示例数据、预测数据和实际数据分区存放,示例数据醒目标出,避免误留在交付件里。

## 六、内置检查

- 关键勾稽写成检查公式:分项合计等于总计、权重之和为 1、行数等于源数据条数等,结果为 TRUE 或差额为 0。
- 所有检查汇总到封面的一个总检查格;交付时总检查必须通过。

## 七、分析场景的表格模式

- **评分卡**:准则 × 权重(输入,和为 1)× 打分(输入,带依据列)× 加权结果(公式);权重可调,旁边放敏感性小表(权重各 ±10% 时名次是否翻转)。
- **对比矩阵**:行是候选项,列是带阈值判定的指标(条件格式标 Good/NI/Poor),Evidence 列写数据来源。
- **趋势 + 异常**:时间序列加异常值行,用标注列区分「剔除异常」和「含异常」两版,判定标准写进方法附注。
- **CSV → xlsx**:先按 foundation 四步流水把数算好,再落表;**不在单元格里做本该由代码完成的清洗**。

## 八、交付前检查清单

- [ ] 输入、计算、输出分区;每个输入只出现一次
- [ ] 计算区没有写死的结果,也没有夹在公式里的常数
- [ ] 已用电子表格软件重算并保存;错误值扫描为零,扫描记录留档
- [ ] 抽查的合计和比率与代码结果一致
- [ ] 总检查通过
- [ ] 封面写明输入样式、单位和正负号约定;假设都带来源
- [ ] 百分比存小数、日期为日期类型;没有隐藏的工作表或行列
- [ ] 在接收方使用的软件里打开确认过

## 来源

- ICAEW, *Financial Modelling Code*(2024):输入、计算、输出分离,每个输入只有一个位置,输入用填充色或边框标出,避免写死,检查与总检查,单位和正负号约定。<https://www.icaew.com/technical/technology/excel-community/improve-your-financial-modelling-practice>
- openpyxl 文档,`load_workbook` 的 `data_only` 参数:<https://openpyxl.readthedocs.io/en/stable/tutorial.html>
- Microsoft [MS-XLSX] 规范,带 `_xlfn.` 前缀的 future functions 列表:<https://learn.microsoft.com/en-us/openspecs/office_standards/ms-xlsx/5d1b6d44-6fc1-4ecd-8fef-0b27406cc2bf>
- 本文件由 EveryInfra 编写。
