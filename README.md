# AI Agent Playbook

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](#)

> **开源协议声明 (License & Copyright)**
> 本项目采用 **CC BY 4.0 (知识共享署名 4.0)** 协议开源。
> 允许您自由共享（复制、发行）以及演绎（修改、转换、基于本作品创作），包括商业性使用。**唯一条件是必须给出适当的署名 (Attribution)**，并指出是否作了修改。

**AI Agent Playbook** 是专门为解决人机协作过程中“上下文坍塌”与“不受控乱改”痛点而设计的纯文本级工作流系统。通过将思考与执行强行解耦，极大提升 AI Agent 在代码修改与复杂任务处理时的安全边际与透明度。

---

## 核心特性 (Key Features)

- **先计划后执行 (Plan First, Execute Later)**：彻底杜绝 AI 自作主张。Agent 必须主动输出详尽的 `implementation_plan.md`，并将执行状态挂起，直到人类用户明确按下 `Proceed` 批准。
- **树状事件归类 (Hierarchical Event Categorization)**：抛弃容易遗忘的扁平列表，强制 AI 以 `[主线项目] -> [具体子任务/约束]` 的树状结构组织上下文记忆，从根本上解决复杂多任务并发时的记忆错乱。
- **主动记忆探针与熔断 (Proactive Memory Loss Recovery)**：系统级探针会在每轮执行完毕后自动触发。当发现因为上下文截断导致记忆丢失时，AI 必须显式向用户发起提问，由人类决定是否需要重新拉回记忆。

---

## 架构哲学 (Architecture Philosophy)

- **大道至简 (Absolute Simplicity)**: 拒绝臃肿的抽象概念、复杂的 Python 框架或冗余的文档目录。整套机制被极致压缩成了一份声明式的 Markdown 规则。
- **消除黑盒 (Eliminate Blackbox)**: AI 的状态、执行意图以及记忆结构必须保持 100% 透明，并且在每个回合结束时以物理文本的形式呈现给用户。

---

## 目录结构 (Directory Structure)

```text
ai-agent-playbook/
├── .agents/                 # AI 系统级指令存放处
│   └── AGENTS.md            # 最核心的 "Plan-Act-Review" 与记忆探针指令
├── LICENSE                  # 开源协议文件
└── README.md                # 本说明文档
```

---

## 快速上手 (Quick Start)

由于本项目坚持“大道至简”的设计哲学，没有任何复杂的依赖或安装过程。

### 1. 植入核心指令
只需将本仓库内的 `.agents/AGENTS.md` 文件直接复制到您个人的项目工作区根目录下：

```bash
cp -r /path/to/ai-agent-playbook/.agents /your/project/workspace/
```

### 2. 自动生效
一旦植入完毕，支持该规范的 AI 系统将会在启动或读取工作区时自动加载配置。系统会立刻化身为极其严谨的合作者，开始严格遵守“事前审批 -> 物理执行 -> 输出树状记忆探针”的闭环 SOP 为您工作。
