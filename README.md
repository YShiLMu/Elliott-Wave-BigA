# Elliott-Wave-BigA（波浪理论在大A）

一个用于分析 A 股市场的 Codex Skill：声明分析级别、数浪、按 Rule 与 Guideline 校验、给出主备方案与独立失效价位、概率排序，并输出分析报告与交易计划。

## 前置依赖

**本技能需要先安装前置 skill：`a-stock-data`**（用于获取 A 股行情/K 线等真实数据）。

安装方式：

1. 在 Codex 中通过技能安装器安装 `a-stock-data`；
2. 或将其放入 `~/.codex/skills/` 后重启 Codex。

分析非 A 股市场（如美股、港股）时不需要该前置 skill，由用户直接提供数据或图表。

**`a-stock-data` 作者与致谢：**

- 作者：Simon 林（[@linsizhen](https://x.com/linsizhen)）
- 网址：[https://github.com/simonlin1212/a-stock-data](https://github.com/simonlin1212/a-stock-data)

感谢 Simon 林把 `a-stock-data` 开源出来，A 股的数据获取基本靠它，真的省了不少事。

## 安装

方式一：通过 Codex 技能安装器安装本仓库：

```
https://github.com/YShiLMu/Elliott-Wave-BigA
```

方式二：手动安装

1. 下载本仓库 zip 并解压；
2. 将解压出的目录改名为 `elliott-wave-biga`；
3. 放到 `~/.codex/skills/` 下，重启 Codex；
4. 在对话中使用 `$elliott-wave-biga` 调用。

## 用法

```
使用 $elliott-wave-biga 分析沪深300 日线走势，给出主备数浪、校验结果、失效价位与概率排序。
```

分析 A 股行情时会调用 `a-stock-data` skill 获取真实数据；其他市场需用户提供数据或图表。

## 结构

- `SKILL.md`：技能入口与核心流程
- `references/`：规则、指南、工作流、斐波那契、形态与术语
- `assets/`：分析报告、交易计划、每日复盘、失效追踪、网页报告模板
- `scripts/ew_chart.py`：K 线图 + 浪型标注绘图脚本
