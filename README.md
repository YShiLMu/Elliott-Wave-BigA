# 波浪理论在大A（Elliott Wave Analysis）

一个用于分析 A 股市场的 Codex Skill：声明分析级别、数浪、按 Rule 与 Guideline 校验、给出主备方案与独立失效价位、概率排序，并输出分析报告与交易计划。

## 安装

方式一：通过 Codex 技能安装器安装本仓库：

```
https://github.com/YShiLMu/elliott-wave-a-shares
```

方式二：手动安装

1. 下载本仓库 zip 并解压；
2. 将解压出的目录改名为 `elliott-wave-analysis`；
3. 放到 `~/.codex/skills/` 下，重启 Codex；
4. 在对话中使用 `$elliott-wave-analysis` 调用。

## 用法

```
使用 $elliott-wave-analysis 分析沪深300 日线走势，给出主备数浪、校验结果、失效价位与概率排序。
```

分析 A 股行情时会调用 `a-stock-data` skill 获取真实数据；其他市场需用户提供数据或图表。

## 结构

- `SKILL.md`：技能入口与核心流程
- `references/`：规则、指南、工作流、斐波那契、形态与术语
- `assets/`：分析报告、交易计划、每日复盘、失效追踪、网页报告模板
- `scripts/ew_chart.py`：K 线图 + 浪型标注绘图脚本
