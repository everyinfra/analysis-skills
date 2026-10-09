---
name: spreadsheet-deliverable
description: Deliver analysis results as a real .xlsx workbook with formulas, not pasted values. Use when the user asks for Excel/spreadsheet output, a financial or scoring model, or a deliverable others will edit. Enforces formula-first cells, a recalculation gate with zero errors before delivery, input/formula color conventions, percentages stored as decimals, and assumptions with sources. Not for plain CSV/JSON exports or markdown tables.
---

# Spreadsheet Deliverable(xlsx 交付纪律)

吸收 [anthropics/skills](https://github.com/anthropics/skills)(MIT)xlsx 官方技能的纪律,适配本仓库分析场景。与 [analysis-foundation](../analysis-foundation/SKILL.md) 配合:数字先由代码算出,表格是把数字变成他人可编辑模型的载体。

## 一、五条硬规则

1. **公式优先,永不硬编码结果**:汇总=SUM/聚合公式,不用手敲数字;下游单元格引用上游,改输入即全表联动——这是"交付模型"与"交付截图"的区别;
2. **重算门禁(recalc gate)**:交付前用脚本重算整个工作簿(如 LibreOffice headless 或 openpyxl 双 pass),**error_summary 必须为零**才可交付;有错修完再交;
3. **双 pass 读模型**:读他人工作簿时,数据值与公式是两个互斥视图(data_only 与公式)——审计公式逻辑用公式视图,对数用数据视图,不可混;
4. **兼容性清单**:LibreOffice/旧 Excel 兼容——新函数带 `_xlfn.` 前缀风险、慎用 XLOOKUP 等新函数(给替代);日期存真实日期类型非字符串;
5. **假设必须带来源**:每个假设单元格旁注来源(`Source: 10-K FY2024 p45` 式)——与 foundation 的 [要追加] 协议同源。

## 二、视觉约定(财务模型惯例)

| 颜色 | 含义 |
|---|---|
| 蓝 | 输入(硬编码假设,唯一允许手敲的) |
| 黑 | 公式 |
| 绿 | 跨表引用 |
| 黄 | 可填空(交付给使用者的交互区) |

其他:百分比**按小数存储**+百分比格式(不是存 "12%");负数用括号或统一红色;每表一个用途,不放"万能 sheet";首 sheet 为封面(目录+口径说明+方法附注,见 foundation 第五节)。

## 三、分析场景的表格模式

- **评分卡**:准则×权重(蓝,和=1)×打分(蓝,带依据列)×加权结果(黑公式)——权重可调+旁边放敏感性 mini 表(权重 ±10% 名次是否翻转);
- **对比矩阵**:行=候选项,列=带阈值判定的指标(Conditional Formatting 上 Good/NI/Poor),Evidence 列引数据源;
- **趋势+异常**:时间序列+异常值行(黄标注"已剔除/含"两版,判定标准入方法附注);
- **CSV→xlsx 升级路径**:先按 foundation 四步流水算好数,再落表——**禁止在单元格里做本该代码做的清洗**。

## 四、交付前检查清单

- [ ] 重算门禁零错误(error_summary 报告留存)
- [ ] 输入/公式/跨表/可填四色正确
- [ ] 无硬编码结果混入公式区(抽查 5 个聚合)
- [ ] 百分比为小数存储;日期为日期类型
- [ ] 假设全部带来源注
- [ ] 封面含:口径说明、数据新鲜度、生成时间戳、"临时手写口径"标注(如有)
- [ ] 在 LibreOffice 中打开一次确认兼容(字体/函数/条件格式)

## 来源

anthropics/skills(MIT)`skills/xlsx/`:recalc 验证闭环、双 pass、颜色/格式惯例、兼容清单。本文件由 EveryInfra 编写,仅收录要点与链接。
