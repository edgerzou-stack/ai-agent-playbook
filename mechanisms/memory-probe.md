# Hierarchical Memory Probe (树状记忆探针 V2)

这套机制是被写入底层系统级 Prompt 的强制拦截器。旨在强行锁定大模型的思维链，防止因上下文过长或多任务并行导致的隐式遗忘。

## 机制原理
在 AI Agent 完成任何一轮对话的最终回复时，必须在文档末尾附带以下格式的记忆快照。通过物理输出的方式，强制大模型将“散落在注意力机制中”的零碎记忆实体化、结构化。

## V2 版本三大核心能力
1. **树状事件归类 (Hierarchical Categorization)**
   不再使用扁平的列表罗列，而是通过 `[主线事件/项目名称] -> [具体子任务/约束]` 的形式组织信息，大幅提高复杂多项目并行的管理能力。
2. **主动记忆熔断与召回 (Interactive Loss Recovery)**
   如果 Agent 判定某些上下文因过长被截断，或者主动丢弃了低优先级任务，**必须**显式在 `Dropped Items` 中列出，并向用户发起提问确认是否彻底丢弃。这赋予了用户管理 AI 生命周期的能力。

## AGENTS.md 最佳实践模板
将以下代码写入项目的 `.agents/AGENTS.md` 即可自动生效：

```markdown
## Universal "Plan-Act-Review" SOP
To ensure maximum efficiency, transparency, and alignment with the user, you MUST adhere to the following strict workflow for any non-trivial codebase modifications or architectural tasks:

1. **Phase 1: Propose & Iterate Plan (No Execution)**
   - Before writing code or modifying files, generate a detailed execution plan.
   - Continuously refine the plan based on user feedback.
   - Wait for explicit user approval before proceeding.

2. **Phase 2: Execution**
   - Execute the approved plan strictly.

3. **Phase 3: Hierarchical Memory Probe & Review**
   - After completing the execution, you MUST output the "Context & Memory State" block at the bottom of your response.
   - **Categorization**: Group active context hierarchically (e.g., Event -> Sub-tasks).
   - **Loss Recovery**: If any memory/context was dropped, explicitly ask the user if it should be retained or permanently discarded.

Format it strictly as follows:

---
**🧠 Context & Memory State:**
*   **✅ Completed Tasks:** [Summary of tasks just completed]
*   **🔄 Active Context (Hierarchical):**
    *   **[Event/Project A]**:
        *   [Sub-task/Constraint 1]
        *   [Sub-task/Constraint 2]
*   **❓ Dropped/Forgotten Items:** [List explicitly dropped items. If not empty, add: "Did you still need me to retain these for later, or can they be permanently discarded?"]
```
