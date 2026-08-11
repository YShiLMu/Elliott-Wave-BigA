> **打包说明**：本文件由 `01_知识库_knowledge/11_规则冲突裁决_rule_conflict_adjudication.md` 转换生成（仅编号与路径口径不同），**禁止直接修改，修改请改源**；维护性章节（转换规则、验收清单）不打包，完整版见 `01_知识库_knowledge/11_规则冲突裁决_rule_conflict_adjudication.md`。
>

# 规则冲突裁决（Rule Conflict Adjudication）——跨步骤知识

> **定位**：本文件是"规则冲突与形态边界归属"的**唯一权威裁决流程**。数浪（`references/workflow.md（第 2 步）`）、验证（`references/workflow.md（第 3 步）`）、更新（`references/workflow.md（第 5 步）`）遇到 Rule 与 Rule、Rule 与 Guideline、Guideline 与 Guideline 的冲突，或形态边界归属不清时，按本文裁决。它不属于任何一个工作流步骤（工作流 01–05 各承载本步骤执行细则），故属跨步骤知识。
>
> **只裁决、不重复条文**：本文只写"冲突怎么裁决、按什么顺序裁决"，不重复展开规则条文。条文唯一权威在 `references/rules.md`（R1–R30）与 `references/guidelines.md`（G1–G25）；形态结构细节见 `references/patterns.md（推动浪）`、`references/patterns.md（楔形）`、`references/patterns.md（调整浪）`、`references/patterns.md（三角形）`；数据问题按 `references/data.md` 处理，不进入本裁决流程。
>

## 1. 裁决总原则

- **Rule 优先于 Guideline**：任一 Rule 违反即数法无效（references/rules.md R19）；Guideline 违反只降低概率，并在输出中说明理由（references/guidelines.md 前言）。Guideline 不得豁免 Rule——references/guidelines.md G20 只说明级别错标的概率影响，不豁免 references/rules.md R4 的嵌套自洽判定。
- **例外条款先验证条件、后适用例外**：例外条款必须先验证其适用条件，满足才可豁免基础规则。典型如重叠例外 references/rules.md R8–R11：先查楔形位置（references/rules.md R9/R10）与子浪结构，并按极端价位（references/rules.md R20）判定，全部满足才豁免 references/rules.md R7；条件不满足仍按 references/rules.md R7 判违反（references/rules.md R11）。
- **本文只写裁决方式**：条文与判定标准以 references/rules.md、references/guidelines.md 为唯一权威；本文不新增、不改写任何 Rule/Guideline，也不重复展开条文内容。

## 2. 冲突类型与处理

| 冲突类型 | 例子 | 裁决方式 |
| --- | --- | --- |
| Rule vs Rule 表面冲突 | references/rules.md R7 重叠 vs references/rules.md R8–R11 楔形例外 | 先验证例外条件：位置（references/rules.md R9/R10）、子浪结构、极端价位（references/rules.md R20）；条件不满足则按 references/rules.md R7 判违反（references/rules.md R11） |
| Rule vs Guideline | references/rules.md R4 嵌套自洽 vs references/guidelines.md G20 级别错标只降概率 | references/guidelines.md G20 不豁免 references/rules.md R4：嵌套自洽按 references/rules.md R4 判定；级别错标是否影响概率按 references/guidelines.md G20 单独说明 |
| Guideline vs Guideline | references/guidelines.md G1 交替 vs references/guidelines.md G23 位置偏好指向不同方案 | 不裁决合法性；按 references/guidelines.md G21 四指标计分排序（Guideline 命中数、结构完整度、斐波那契共振、失效价位距离） |
| 形态边界归属 | 双锯齿形 references/rules.md R13 vs 联合形 references/rules.md R16；三角形 references/rules.md R15/R27 vs 楔形 references/rules.md R9/R10 vs 平台形 references/rules.md R14/R28 | 按第 3 节裁决顺序执行 |

## 3. 形态边界裁决顺序（固定流程）

1. **结构证据优先**：先按子浪计数判定形态身份——锯齿形 5-3-5（references/rules.md R12）、平台形 3-3-5（references/rules.md R14/R28）、三角形 3-3-3-3-3（references/rules.md R15/R27）、楔形（references/rules.md R9/R10）。子浪结构与数量是最高优先级证据；形态细节见 `references/patterns.md（推动浪）`、`references/patterns.md（楔形）`、`references/patterns.md（调整浪）`、`references/patterns.md（三角形）`。
2. **位置约束次之**：三角形不作第 2 浪独立形态（references/rules.md R15）、楔形位置限制（references/rules.md R9/R10）；位置偏好（references/guidelines.md G23）只作参考，不构成合法性判定。
3. **身份约束**：B/X/W/Y/Z 不得标为推动浪（references/rules.md R30）；X 浪必须是调整浪（references/rules.md R3）；方向身份须自洽（references/rules.md R25）。
4. **Guideline 计分**：前三步仍有多解时，按 references/guidelines.md G21 计分排序；排序不裁决合法性，只影响概率与仓位。
5. **仍无法裁决**：输出多重数浪——主备方案 + 各自独立失效价位 + 区分信号（references/rules.md R24）；禁止硬猜唯一解。

## 4. 引用点

- `references/workflow.md（第 2 步）`：枚举候选数法（第 3 节）遇到形态边界时，注明"按 `references/rule_conflicts.md` 第 3 节裁决"。
- `references/workflow.md（第 3 步）`：Rule 复核（第 3 节）发现冲突时，引用本文第 2、3 节。
- `references/workflow.md（第 5 步）`：形态切换决策（5.2 节）引用本文第 3 节。
- `assets/分析报告_report.md`【7. 风险提示】：需要说明歧义裁决依据时引用本文。
