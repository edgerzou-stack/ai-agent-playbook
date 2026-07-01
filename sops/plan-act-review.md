# Universal "Plan-Act-Review" SOP (V2)

本 SOP 旨在定义人类与 AI Agent 进行非琐碎任务协作时的普适性、防失控闭环工作流。通过将“思考”与“执行”强行解耦，极大提升操作的安全边际。

## 核心工作流 (The Workflow)

### Phase 1: Propose & Iterate Plan (事前拟定与多轮迭代)
在执行任何实际的修改之前，AI Agent 必须：
1. 主动输出详尽的 `implementation_plan.md`。
2. 将执行状态挂起（Wait for user approval）。
3. 如果用户不满意，支持进行任意轮次的驳回和修改，直至计划完美。

### Phase 2: Execution (静默精确执行)
在用户明确按下 `Proceed` 批准后，Agent 进入执行期：
1. 严格按照已定计划的每一个步骤进行物理上的文件 I/O、命令行操作。
2. 杜绝自作主张的范围溢出。

### Phase 3: Hierarchical Memory Probe & Review (事后探针与熔断询问)
执行完毕后，Agent 必须通过“记忆探针”汇报状态。
详见 [Hierarchical Memory Probe](../mechanisms/memory-probe.md)。

## 适用边界
对于极度琐碎的操作（如修一个拼写错误），允许跳过 Phase 1 以节省时间，但 **Phase 3 (记忆探针) 是铁律，任何情况都不可省略**。
