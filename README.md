# Project Task Router

一个面向 Codex 和其他 AI Agent 的任务复杂度路由 Skill。它先判断任务属于简单、聚焦多步、多阶段还是长期任务，再选择合适的规划深度、对话边界、正式产出与交接方式。

它的目标不是让每个任务都先写一大份计划，而是让规划成本与任务风险相匹配：简单任务直接做，复杂任务先理清依赖，长期任务把关键状态落到正式文件中。

## 核心能力

- 将任务分为简单、聚焦多步、多阶段和长期任务四级。
- 在当前对话完成与拆分新对话之间做有依据的选择。
- 为复杂任务明确总目标、阶段、准确输入、正式输出和完成标准。
- 在暂停或换对话前生成精简交接和可直接使用的续接提示。
- 通过权威文件保存稳定事实，降低长对话造成的信息遗漏和返工。
- 控制流程开销，不把清楚的小任务机械复杂化。

## 两部分如何配合

这个仓库包含两个互补部分：

1. `project-task-router/` 是正式 Skill。它提供复杂任务的分级、路由、阶段划分和交接方法。
2. `AGENTS－任务复杂度门检片段.md` 是可选的长期规则片段。把它合并到 Agent 的全局 `AGENTS.md` 或等效规则文件后，Agent 才会在每个新任务开始时主动做轻量门检。

只安装 Skill 时，可以通过 `$project-task-router` 明确调用，也可以在匹配的复杂任务中由运行环境自动触发。若希望“所有任务开始时都先判断，但简单任务不展示多余规划”，建议同时合并长期规则片段。

## 推荐安装方式

下载或克隆本仓库后，把整个仓库交给你的 AI Agent，并发送：

```text
请阅读并执行仓库中的《01－直接交给AI的安装提示词.md》，安装 project-task-router Skill，并把任务复杂度门检片段去重合并到你真实的全局规则文件。不要覆盖已有无关规则。完成后报告实际安装路径、修改的规则文件和验证结果。
```

详细的自动安装提示词见 [`01－直接交给AI的安装提示词.md`](./01－直接交给AI的安装提示词.md)。

## 手动安装

1. 把 `project-task-router` 文件夹复制到 Agent 的个人 Skill 目录。
   - Codex 常见位置：`~/.codex/skills/project-task-router`
   - 其他 Agent：使用该产品实际支持的全局 Skill 目录。
2. 可选：把 `AGENTS－任务复杂度门检片段.md` 中“规则正文”部分合并到全局 `AGENTS.md` 或等效规则文件。
3. 保留原有规则，只做去重合并，不要用示例文件整份覆盖已有配置。
4. 重新启动或让 Agent 重新读取 Skill 与长期规则。
5. 用下面的测试提示验证：

```text
请使用 $project-task-router 判断这个任务应当直接完成、在当前对话列短计划，还是拆成多个阶段：我要制作一个包含调研、脚本、角色设定、分镜和成片验收的短片项目。
```

## 使用示例

明确调用：

```text
请用 $project-task-router 规划这个任务，说明阶段、每阶段的输入输出、完成标准，以及是否值得换对话。
```

恢复长期项目：

```text
请用 $project-task-router 接续这个项目。先判断当前资料是否足够，再给出本阶段唯一产出、需要读取的准确文件和完成后的交接更新。
```

简单任务不应出现额外仪式。安装全局门检后，像“把这句话改得更自然”这样的请求仍应直接完成。

## 仓库结构

```text
.
├── project-task-router/
│   ├── SKILL.md
│   └── agents/openai.yaml
├── AGENTS－任务复杂度门检片段.md
├── 01－直接交给AI的安装提示词.md
├── 02－给朋友的简明使用说明.md
└── README.md
```

`SKILL.md` 是运行时核心；`agents/openai.yaml` 提供 Skill 列表中的显示名称、简介和默认调用提示。仓库根目录的其他文件用于安装和分享，不会增加 Skill 被触发后的上下文负担。

## 适用范围

该 Skill 最适合以下情况：

- 一个请求包含多个成果或生产阶段；
- 后续工作依赖尚未确认的上游决定；
- 不同阶段需要读取不同资料；
- 项目可能跨越多个对话或较长时间；
- 需要可追踪的正式成果、检查点和交接。

对于单一、明确、低风险的任务，不应强制调用或输出复杂规划。

## 兼容性

核心内容是纯 Markdown，没有运行时依赖。它首先按 Codex Skill 结构整理，也可移植到支持 Markdown 指令包、Skill 或长期 Agent 规则的其他环境。不同产品的 Skill 目录和全局规则文件位置可能不同，应以实际环境为准。

## 隐私与安全

仓库不应包含个人项目资料、访问令牌、账号密码、浏览器数据或本机绝对路径。安装时也不要把任何凭据写入 Skill 或长期规则。

## 开源许可

本项目采用 [MIT License](./LICENSE)。你可以使用、修改和分发，但需保留原始版权与许可声明。

## English overview

Project Task Router is a lightweight planning and continuity skill for AI agents. It classifies work as simple, focused multi-step, multi-stage, or long-running; then chooses the smallest reliable planning structure. It helps define dependencies, deliverables, completion criteria, conversation boundaries, and compact file-based handoffs without adding ceremony to simple requests.
