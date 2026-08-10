---
name: elliott-wave-biga
description: 按 Elliott Wave（艾略特波浪理论）分析市场或图表：声明分析级别、数浪、按 Rule 与 Guideline 校验、给出主备方案与独立失效价位、概率排序、输出报告与交易计划。A 股行情可用 a-stock-data 获取，其他市场需用户提供数据或图表。
---

# Elliott Wave 分析（Elliott Wave Analysis）

按 Frost & Prechter《Elliott Wave Principle》的框架分析市场。先声明级别，再数浪、校验、排序、输出；禁止在正文重新定义术语或规则，唯一权威见 `references/`。

## 1. 输入准备与数据获取

- 分析 A 股：先调用 `a-stock-data` skill 获取指定级别与时间范围的行情（日 K/周 K/月 K 均可），再开始数浪；其他市场：以用户提供的数据或图表为准。
- 无论数据来源，先提取**极端价位（含影线）序列**：所有摆动点、失效价位、边界与比率计算一律以含影线的最高/最低价为准，不以收盘价替代（见 references/rules.md R20）。
- 数据不足或无法确认内部子浪时，如实说明并保守处理（见 references/guidelines.md G12），不得编造后续行情。

## 2. 核心约定（必须遵守）

- **分析级别（Degree）优先**：数浪前必须声明分析级别；不谈级别的数浪无效（见 references/rules.md R22；references/terminology.md 1.2.1）。
- **Rule 与 Guideline 严格区分**：Rule 违反即数法无效；Guideline 违反只降概率并说明理由（见 references/rules.md 与 references/guidelines.md 前言）。
- **主备方案**：任何分析必须给出主方案 + 至少一个替代方案，每个方案独立标注失效价位（见 references/rules.md R24）。
- **概率排序有依据**：按 Guideline 命中数、结构完整度、斐波那契共振、失效价位距离评分（见 references/guidelines.md G21），不空谈概率。
- **术语统一**：使用「中文（English）」格式，例如 推动浪（Impulse）、替代方案（Alternate Count）。

## 3. 分析流程（5 步，对应 `references/workflow.md`）

### 第 1 步 分析市场

读取数据 → 判定趋势方向 → 选择并声明分析级别（见 `references/workflow.md` 第 1 步）。

### 第 2 步 数浪

找主要摆动 → 枚举主备数法 → 逐条执行 Rule Check → 执行 Guideline Check → 标注失效价位 → 概率排序（见 `references/workflow.md` 第 2 步；检查表见 `references/checklists.md`）。

### 第 3 步 验证数浪

结构自洽 → Rule 复核 → Guideline 复核 → 失效价位验证 → 输出完整性检查；**只验证，不修改数法**（见 `references/workflow.md` 第 3 步）。

### 第 4 步 生成报告

按 8 章节结构输出分析报告，复制 `assets/分析报告_report.md` 填写（见 `references/workflow.md` 第 4 步）。
报告与网页归档到 `<项目根目录>/分析输出/<标的名称_代码_YYYYMMDD_HHMM>/`（归档规范见本文第 5 节「输出归档」）。
生成后运行 `scripts/embed_report_images.py <归档文件夹>`，自动把 `图表/` 下 PNG 转 base64 内嵌进 .md 与 .html（md 在查看器不支持 data URI 时可用 `--md-keep-absolute` 回退绝对路径并注明），校验通过才交付（见 `references/workflow.md` 第 4 步第 2.3 节）。

**K 线图 + 浪型标注**：获取行情数据后、报告定稿前，用 `scripts/ew_chart.py` 为每个合法候选数法绘制**两张图——全景图 + 放大图**（图片数量 = 候选方案数 × 2；禁止主备混叠，见 `references/rules.md` R23）：全景图覆盖完整数据范围（数据起点不得擅自截断，图注标注"起点至最新"），只标注大级别结构（1-2-3-4-5 / A-B-C / W-X-Y）与大级别失效价位；放大图用 `--last N` 截取尾部区间（默认最近 250 根，或按用户指定），标注子浪编号（①②③ 或 i-iii）、支撑/阻力、失效价位与当前价格，建议 `--font-scale 1.2–1.4` 保证子浪标注清晰。图标题含分析级别与时间范围（`references/rules.md` R22）；浪段标注按 R23；失效价位红色虚线并注明规则编号（R19、R20）。图表用高清输出（dpi ≥ 150）。PNG 只用于嵌入交付物，保存后必须验证文件存在且可渲染（自检清单见 `references/workflow.md` 第 4 步第 2.1 节）。

### 第 5 步 更新数浪

失效优先 → 触发条件判定（H1–H4 硬性触发 / S1–S3 软性触发）→ 主备方案状态维护 → 概率重排 → 写入变更日志（见 `references/workflow.md` 第 5 步）。

### 最小可执行示例（假设数据）

场景：上升趋势第 4 浪位置（假设数据），当前价格 197。

1. 声明级别：日线中浪 Intermediate，第 (4) 浪回调中（见 `references/terminology.md`；references/rules.md R22）；
2. 枚举：主方案"平台形（Flat）"A-B-C 3-3-5 vs 替代"三角形（Triangle）"A-B-C-D-E（见 `references/patterns.md`）；
3. Rule Check：逐条检查 R14（3-3-5）、R28（三变体分类）与 R15/R27（三角形结构与子浪），任一违反即方案失效（见 `references/rules.md`；`references/checklists.md`）；
4. Guideline Check：检查 G1 交替（第 2 浪陡直、第 4 浪横向），命中 +1，只参与排序不裁决合法性（见 `references/guidelines.md`）；
5. 标注失效价位：主方案跌破 C 浪终点后连续 2 根收盘未收回即失效；替代跌破三角形下边界（趋势线）且不回抽即失效——价位按极端价位精确标注（见 references/rules.md R20）；
6. 概率排序：按 Guideline 得分、结构完整度、共振、失效距离计算加权总分，输出主备排序与升级条件（见 `references/workflow.md` 第 2 步；references/guidelines.md G21）。

## 4. 参考资料导航（按需加载，禁止一次全读）

| 场景 | 读取文件 |
| --- | --- |
| 术语/标注/级别含义 | `references/terminology.md` |
| 合法性判断（Rule） | `references/rules.md` |
| 概率性规律（Guideline） | `references/guidelines.md` |
| 形态识别与常见错误 | `references/patterns.md` |
| 比率目标与共振 | `references/fibonacci.md` |
| 逐条校验清单 | `references/checklists.md` |
| 工作流细节与交接格式 | `references/workflow.md` |
| 项目默认口径（须披露的量化约定） | `references/defaults.md` |

## 5. 模板与输出（assets）

**交付物规范（每次分析只交付两个文档）**：

- 归档位置：`<项目根目录>/分析输出/<标的名称_代码_YYYYMMDD_HHMM>/`（归档规范见本文第 5 节「输出归档」）；
- **分析报告_<标的>_<代码>_<时间>.md**：按 `assets/分析报告_report.md` 模板输出；交易计划（第 6 章）、失效价位（第 5 章）、更新与跟踪（第 8 章）内容完整并入，不再单独成文件；浪型图以 Markdown 图片语法嵌入，**必须使用绝对路径**引用 `分析输出/<文件夹名>/图表/<PNG>`，保证可渲染；
- **网页报告_<标的>_<代码>_<时间>.html**：复制 `assets/网页报告_web_report.html` **直接填充**生成（所有 `{{字段名}}` 替换为本次分析数据，图区填入 PNG 相对路径，如 `图表/主方案_全景.png`），禁止从零重写 HTML 结构；
- 两份文档中主备方案、失效价位、概率排序、简洁总结、关键价位表必须一致。

**不再生成**：独立交易计划.md、失效追踪.md、变更日志.md、日线 CSV、独立 PNG——浪型图仅作内嵌素材存于该文件夹 `图表/` 子目录。

- `assets/分析报告_report.md`：第 4 步报告输出时复制填写（**交付文档**）；
- `assets/网页报告_web_report.html`：生成分析报告时，复制该模板，填入数据、浪型图与简洁总结后交付网页（**交付文档**，含主备方案标签页与末尾总结，见 `references/workflow.md` 第 4 步输出结构）；
- `assets/每日复盘_daily_review.md`、`assets/失效追踪_invalidation.md`、`assets/交易计划_trade_plan.md`：**仅作内部工作底稿**（盘中草稿、跨周期失效跟踪、仓位草稿），产出**不进入 `分析输出/` 归档、不作为交付物**；需要交付的内容分别并入分析报告.md 对应章节（交易计划→第 6 章、失效价位与更新跟踪→第 5/8 章、复盘更新→第 8 章）。

模板不加载进上下文；交付文档复制到归档文件夹填写，工作底稿复制到临时/工作目录填写、不进入 `分析输出/`。

**输出归档（必须遵守）**：所有分析输出统一归档到**当前项目根目录** `分析输出/`（即运行本次分析的工作区根目录，禁止写入技能安装目录或系统目录）。**一次分析 = 一个独立子文件夹**，命名 `标的名称_代码_YYYYMMDD_HHMM`（本地时间 4 位；Windows 文件夹名禁止冒号，如 `科创50_1B0688_20260809_1522`）；文件夹内**只放两个交付文档**（分析报告_*.md 与 网页报告_*.html），浪型图 PNG 仅存于 `图表/` 子目录作内嵌素材；**不生成**原始行情 CSV、独立的失效追踪、交易计划、变更日志文件（内容分别并入报告第 5/6/8 章）。同一标的的后续更新写回原文件夹；确需从头重开时新建带新时间戳的文件夹，并在旧文件夹分析报告.md 第 8 章登记去向。

## 6. 校验与报告规范

- 每个候选数法必须给出 Rule Check 与 Guideline Check 结果表（格式见 `references/checklists.md`）。
- 报告必须声明级别、不混用标注、失效价位精确到具体价位（见 references/rules.md R20、R22、R23）。
- 概率表述用"大概率 / 倾向于 / 通常"，禁止"必然 / 一定 / 绝对"（见 references/guidelines.md 前言）。
- 假设数据必须显著标注；后续走势未发生时如实标注，禁止编造。

## 7. 禁止事项

- 禁止把 Guideline 升格为 Rule，或把 Rule 降格为 Guideline；
- 禁止只给单方案；
- 禁止写模糊失效价位（如"附近""左右"）；
- 禁止在正文重新定义术语或规则（唯一权威在 `references/`）。

## 8. 输出结构（简明分析 → 浪型图 → 简洁总结）

**三份输出物关系**：`分析报告.md` 是完整正文——简明分析说明置于第 1 章之前（开篇摘要），浪型图嵌入【2 主方案】【3 替代方案】章节，简洁总结位于全文末尾；`网页报告.html` 是同一内容的快捷查看版（页头 → 简明分析 → 主备方案图标签页 → 简洁总结），不新增分析结论；简明分析说明与简洁总结在每份交付物中各出现一次。

按以下顺序输出，便于快速查看与决策：

1. **简明分析说明（3–5 段以内，禁止长篇展开）**：
   - 标的、周期与声明的分析级别（见 references/rules.md R22）；
   - 主方案与替代方案各用一句话描述（见 references/rules.md R24）；
   - Rule 校验结论：说明哪条规则决定取舍（例如"第 4 子浪与第 1 子浪重叠，违反 R7，故不标普通推动浪，改用楔形假设"）；
   - Guideline 概率排序依据：主备评分与失效距离（见 references/guidelines.md G21）。
2. **浪型标注图（放在总结之前）**：每个方案两张图（全景 + 放大，图片数量 = 候选方案数 × 2，工作流输出约定，见 references/workflow.md 第 4 步第 2.1 节）；每张图只用 Python（matplotlib）绘制 K 线再叠加浪型标注，保存 PNG 后由 `scripts/embed_report_images.py` 自动转 base64 内嵌进 .md 与 .html（自包含交付；md 在查看器不支持 data URI 时可回退绝对路径；脚本 `scripts/ew_chart.py`；内嵌校验见 references/workflow.md 第 4 步第 2.3 节）；标题含级别与时间范围（见 references/rules.md R22）；浪段标注不混用（见 references/rules.md R23）；每段浪注明形态类型；失效价位红色虚线 + 规则编号（见 references/rules.md R19、R20）；标出支撑/阻力与当前价格。
3. **简洁总结（所有内容最后，≤15 行）**：严格按以下格式，每字段 1–3 句话：

   **标的【代码】（【名称】），截至【日期】收盘【价格】。**

   **核心判断：**【当前处于哪个浪、什么形态、方向倾向】
   **当前关键形态：**【关键结构特征与依据，如子浪重叠、三角形类型】
   **备选方案：**【一句话 + 确认/证伪价位】
   **概率与仓位：**【主备评分与失效距离结论 + 仓位建议，如"轻仓试探（2–3 成）"】
   **关键价位：**【上方突破观察：……；下方防守：……】
   **核心方法论启示：**【本次数浪体现的 Rule/Guideline 设计逻辑，一句话】

总结禁止复述完整分析过程，只给结论、关键价位与仓位；概率表述用"大概率/倾向于/通常"，禁止"必然/一定/绝对"（见 references/guidelines.md 前言）。
