---
aliases:
tags:
Description:
Type: project
CreatedTime: "[[2026-03-16]]"
BelongTo: "[[openClaw]]"
Related:
---
ModifiedTime: `= this.file.mtime`

---

## 课程目标

面向设计学本科生和研究生，从交互设计视角理解 AI Agent 的技术本质，启发学生思考如何利用 Agent 技术进行设计创新。

---

## Part 1: 从大模型到 Agent — 技术演进与本质

> 核心叙事线：LLM → Chatbot → Agent（ReAct）→ OpenClaw（Agent 住进电脑）
> 每一步跨越意味着什么？对我们（设计者）意味着什么？

### 第一层：大模型（LLM）— 会说话的大脑
- LLM 本质上是一个文本生成器，输入 prompt → 输出 text
- 能力：理解语义、生成内容、推理
- 局限：**没有记忆、没有行动力、没有与外部世界的连接**
- 形态：单轮问答，用完即走

### 第二层：Chatbot — 能对话了
- 在 LLM 基础上加入**对话历史（conversation history）**
- 可以多轮对话，有上下文感知
- 但本质仍是**被动应答**：你问它答，你不问它就不动
- 形态：ChatGPT、Claude 对话界面
- **对设计者意味着**：交互从搜索框/表单 → 对话框，但仍然是用户发起

### 第三层：Agent — 会思考、会行动
- 关键跨越：LLM + **Tool Use（工具调用）** + **ReAct 循环**
- **Function Calling / Tool Use**：LLM 不再只生成文字，而是可以决定"我需要调用某个工具来完成任务"
  - 例：用户问"北京天气"→ LLM 决定调用天气 API → 获取结果 → 基于结果回答
  - LLM 的角色从"文本生成器"变成了"决策者 + 协调者"
- **ReAct 循环（Reasoning + Acting）**：
  ```
  Thought（思考）→ Action（行动/调用工具）→ Observation（观察结果）→ 循环...
  ```
  - 模仿人类解决问题的方式：想一想 → 做一做 → 看看结果 → 再想
  - Agent 可以**多步推理**，根据中间结果调整策略
- **对设计者意味着**：AI 从"应答工具"变成了"能执行任务的助手"，交互从"对话"扩展到"委托（delegation）"

### 第四层：OpenClaw — Agent 住进了电脑
- OpenClaw = Agent + **常驻运行** + **通讯连接** + **记忆系统** + **定时心跳**
- 这是一个质的飞跃：Agent 不再是"打开-使用-关闭"，而是**24/7 活着的数字存在**

#### OpenClaw 简介
- 2025年11月发布（前身 Clawdbot / Moltbot），创建者 Peter Steinberger
- 开源、self-hosted、local-first，2026年1月爆发式增长（30-40万用户）

#### 五大核心组件
1. **Gateway（网关）** — 消息路由控制面，连接 20+ 通讯平台（WhatsApp/Slack/Discord/Telegram/iMessage/Signal...）
   - Hub-and-spoke 架构：一个 Gateway 进程接收所有平台消息，路由到统一的 session
   - Channel Adapter 归一化不同平台的消息格式
2. **Brain（大脑）** — 基于 ReAct 循环编排 LLM 调用（支持 Claude、GPT、DeepSeek 等）
3. **Memory（记忆）** — 双层记忆系统：
   - 短期记忆：daily logs + session context，对话中积累
   - 长期记忆：curated Markdown 文件，记录偏好、决策、重要事实，跨会话持久化
   - 刻意简洁：纯 Markdown 文件，无向量数据库
4. **Skills（技能）** — 插件能力系统，SKILL.md + YAML frontmatter 定义，社区通过 ClawHub 共享（1700+技能）
5. **Heartbeat（心跳）** — **Agent 主动性的关键机制**
   - 周期性触发（如每30分钟），无需用户输入
   - 读取上下文 → 检查 HEARTBEAT.md → 判断是否有需要你注意的事
   - 例：每天6am检查邮件、起草回复，你醒来时已经准备好了

#### Agent Loop（完整循环）
```
接收消息 → 路由到会话 → 加载上下文+Skills → LLM推理(ReAct) → 工具调用 → 流式回复 → 持久化状态
```

- **对设计者意味着**：这不再是一个"工具"，而是一个**有记忆、有行动力、能主动联系你、活在你日常通讯渠道里的数字实体**。交互设计的对象从"界面"变成了"关系"。

---

## Part 2: Agent 架构带来的交互范式变化

> 从 OpenClaw 的架构特性出发，讨论对交互设计的影响和创新空间

### 2.1 主动响应式交互（Proactive Interaction）
- **传统模式**：用户发起 → 系统响应（Request-Response）
- **Agent 模式**：Agent 通过 Heartbeat 主动感知 → 主动联系用户
- OpenClaw 实例：Agent 每天检查邮件/日历，主动推送待办提醒
- **设计启发**：如何设计"不打扰但有用"的主动交互？何时该主动、何时该沉默？
- 参考：Peter Steinberger 将 Heartbeat 描述为"将 Agent 从被动 chatbot 转变为主动自治监控者"的关键特性

### 2.1+ 案例：移动机器人的主动服务方法
> 当 Agent 的"主动性"从数字世界走进物理空间 — 一种基于服务时间轴的机器人主动服务方案

- **核心思路**：给机器人一张"日程表"（服务时间轴），让它像 Agent 的 Heartbeat 一样，主动规划、主动移动、主动发起服务
- **服务时间轴（Service Timeline）**：
  - **预设服务**：用户手动配置（如"每天 7:00 在厨房提醒妈妈吃药"）
  - **预测服务**：LLM 从历史服务数据中学习，自动生成（如"周一早上 9:00 妈妈可能需要穿搭建议"）
  - 预设优先级 > 预测优先级，时间冲突自动检测
- **完整服务循环**：
  ```
  查询日程 → 移动到目标地点 → 预响应（调整位姿/屏幕朝向）→ 判断是否启动 → 执行服务（LLM 驱动的主动响应）→ 记录数据
  ```
- **两种响应模式**：
  - 预启动响应：预设服务 → 机器人就位等待，调整好姿态
  - 建议响应：预测服务 → 屏幕展示个性化建议，引导用户决定是否启动
- **持续学习**：从服务使用数据中学习用户偏好（内容偏好 + 交互方式偏好），预测服务越来越精准
- **与 Heartbeat 的类比**：服务时间轴 ≈ HEARTBEAT.md，预测服务 ≈ Agent 自主判断"该做什么"，预响应 ≈ Agent 的上下文加载
- **设计启发**：机器人的主动服务同样面临"何时该主动、何时该沉默"的问题 — 预测服务的置信度机制是一种解法

### 2.2 连续交互与记忆能力（Continuous Interaction & Memory）
- **传统模式**：每次对话是独立的，关闭窗口 = 遗忘一切
- **Agent 模式**：Agent 常驻运行，对话跨时间、跨会话延续
- OpenClaw 的双层记忆系统：
  - 短期记忆：daily logs + session context，对话中积累
  - 长期记忆：curated Markdown 文件，跨会话持久化偏好、决策、重要事实
  - 选择性记忆：有意识地决定记什么、忘什么（记忆 = Agent 的"人格"基础）
- **设计启发**：如何设计"长期关系型"的交互？记忆如何影响 Agent 的行为和人格？

### 2.3 终端用户编程与软件定制（End-User Development）
> 从"我来编程"到"Agent 自己开发"的递进

- **Level 1：直接编程** — 开发者写代码构建定制系统，门槛最高
- **Level 2：Coding Agent 对话式开发** — 通过与 coding agent 对话（如 Claude Code、Cursor），用自然语言描述需求，Agent 帮你写代码生成软件
  - 降低了开发门槛，但仍需要开发-部署-使用的流程
- **Level 3：OpenClaw Runtime 自适应** — 在运行时直接告诉 Agent 你要什么功能，Agent 自己开发、自己部署、自己运行
  - OpenClaw 的 Skill 系统：用户描述需求 → Agent 编写 Skill → 立即可用
  - 不再有"开发"和"使用"的边界，软件在对话中被创造
- **对设计者意味着**：
  - End-User Development（EUD）的终极形态：用户不再定制界面，而是通过对话定制能力
  - 传统 EUD 方法对比：自定义配置 → 可视化编程 → 对话式编程 → Agent 自主开发
  - 设计挑战：如何让用户有效表达需求？如何让用户验证 Agent 开发的功能是否正确？

### 2.4 多端交互能力（Multi-Channel Interaction）
- **传统模式**：一个应用 = 一个入口
- **Agent 模式**：同一个 Agent，通过 WhatsApp/Slack/Telegram/Web 任意渠道访问
- OpenClaw 实例：在 WhatsApp 开始对话 → Telegram 继续 → Web 管理，会话状态统一
- **设计启发**：
  - 用户不再需要"打开某个 App"，Agent 在你已有的通讯工具里
  - 交互设计从"设计界面"变成"设计跨渠道体验"
  - UX 从 interaction design → **delegation design**：用户不再执行任务，而是委托任务

### 交互范式总结对比

| 维度 | Chatbot | Agent (OpenClaw) |
|------|---------|-----------------|
| 发起方 | 用户发起 | 双向（用户+Agent主动） |
| 时间性 | 用完即走 | 24/7 常驻 |
| 记忆 | 无/短期 | 长期自适应 |
| 入口 | 单一App | 多渠道统一 |
| 用户角色 | 操作者 | 委托者 |
| 定制方式 | 编程/配置 | 对话即定制 |
| 设计重心 | 界面 | 关系+信任 |

---

### Agent 时代的设计挑战

> 以上是 Agent 架构带来的创新机会，以下是设计者需要解决的问题

#### 挑战 1：透明性与控制权（Transparency & Control）
- **现状问题**：OpenClaw 实际上是个**黑盒**
  - 权限极高，能访问邮件、文件、通讯等
  - 消耗大量 token，后台做了很多事情用户看不到
  - 高度自主，用户缺乏控制感
- **设计问题**：
  - Agent 在做什么？做了多少？做对了没有？
  - 如何让用户"知情但不被打扰"？
  - 如何设计 Agent 行为的可审计性（auditability）？

#### 挑战 2：信任校准（Trust Calibration）
- 用户如何建立对 Agent 的**合理信任**？
  - 过度信任 → 依赖 Agent，不检查结果，出错不自知
  - 过度怀疑 → 反复确认，效率低，Agent 形同虚设
- **设计问题**：如何帮助用户形成准确的心智模型 — 知道 Agent 擅长什么、不擅长什么？

#### 挑战 3：错误恢复与问责（Error Recovery & Accountability）
- Agent 自主执行了错误操作怎么办？
  - 发错邮件、删错文件、回复不当
  - Agent 的行为链条长且复杂，难以回溯
- **设计问题**：如何设计撤销/回滚机制？出了问题"谁负责"？

#### 挑战 4：隐私与记忆边界（Privacy & Memory Boundaries）
- Agent 记住了太多个人信息怎么办？
- 记忆有时效性，过时的记忆可能导致错误判断
- **设计问题**：
  - 用户如何查看、编辑、删除 Agent 的记忆？
  - 如何设计记忆衰减机制？
  - 在多用户/群组场景中，记忆的边界在哪里？

#### 挑战 5：社交场景中的 Agent 角色（Agent in Social Context）
- Agent 出现在群聊中时，它是什么角色？
  - 是某人的私人助手？还是群组的公共助手？
  - Agent 发言会影响群组社交动态
- **设计问题**：Agent 在多人交互中的身份、权限、发言时机如何设计？

---

## Part 3: 实例 — OpenClaw 连接 Tami 机器人

### OpenClaw + 机器人的技术基础
- OpenClaw 已有机器人集成案例：
  - Unitree G1 人形机器人
  - Aero Hand Open（3D打印机械手，16关节，USB摄像头视觉验证）
  - Raspberry Pi 集成
- 与 Gemini Robotics-ER、Qwen VLM 等理解物理世界的模型集成
- 支持零代码机器人控制

### OpenClaw + Tami 连接方案（待补充具体细节）
- [ ] Tami 机器人的接口/SDK 信息
- [ ] 连接方式：通过 Skill 还是 Tool？
- [ ] Demo 场景设计：让学生看到从"对话指令"到"机器人动作"的完整链路
- [ ] 录制演示 GIF/视频

### 教学价值
- 展示 Agent 从数字到物理的完整闭环
- 让学生理解 Tool Use 的实际意义：不只是调 API，还能控制硬件
- 激发学生思考：还能连接什么？还能设计什么样的交互？

---

## 参考资料

### OpenClaw 核心
- [OpenClaw 官网](https://openclaw.ai/)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [OpenClaw 官方文档 - 架构](https://docs.openclaw.ai/concepts/architecture)
- [OpenClaw 官方文档 - Tools](https://docs.openclaw.ai/tools)
- [OpenClaw 官方文档 - Heartbeat](https://docs.openclaw.ai/gateway/heartbeat)
- [OpenClaw Architecture, Explained](https://ppaolo.substack.com/p/openclaw-system-architecture-overview)
- [How OpenClaw Works - Medium](https://bibek-poudel.medium.com/how-openclaw-works-understanding-ai-agents-through-a-real-architecture-5d59cc7a4764)
- [OpenClaw: The Open-Source AI Agent That Took the World by Storm](https://www.aibarcelona.org/2026/03/openclaw-open-source-ai-agent-origin-architecture.html)
- [OpenClaw Design Patterns](https://kenhuangus.substack.com/p/openclaw-design-patterns-part-1-of)
- [You Could've Invented OpenClaw](https://nader.substack.com/p/you-couldve-invented-openclaw)
- [OpenClaw: From Chatbot to 24/7 Autonomous AI Teammate](https://aimlapi.com/blog/openclaw-from-chatbot-to-24-7)

### Agent 技术基础
- [What is a ReAct Agent? - IBM](https://www.ibm.com/think/topics/react-agent)
- [Understanding AI Agents: Thought-Action-Observation - Hugging Face](https://huggingface.co/learn/agents-course/unit1/agent-steps-and-structure)
- [LLM Tools: From Chatbot to Real-World Agent](https://www.lorenstew.art/blog/llm-tools-1-chatbot-to-agent)
- [Single LLM to Agentic AI: GenAI's Evolution](https://medium.com/@senthilkumar.m1901/single-llm-to-agentic-ai-genais-evolution-explained-c0670d8325f3)

### 交互设计视角
- [A New HCI Paradigm: Agent Interaction Model Based on Large Models - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S209657962500021X)
- [Five Design Paradigms Reshaping Our Digital Future](https://medium.com/cyberark-engineering/when-the-agents-go-marching-in-five-design-paradigms-reshaping-our-digital-future-a219009db198)
- [The End of the User Interface? How AI Agents Are Rewriting UX](https://raw.studio/blog/the-end-of-the-user-interface-how-ai-agents-are-rewriting-ux/)
- [UI Design for AI Agents - Fuselab](https://fuselabcreative.com/ui-design-for-ai-agents/)

### 机器人集成
- [OpenClaw 机器人编程 - Hackster.io](https://www.hackster.io/psmooij/openclaw-for-robot-programming-pmsg-on-budget-d76a91)
- [AI Agents Meet Robotics](https://www.xiaorgeek.net/blogs/news/openclaw-ai-agents-meet-robotics-turn-ai-into-physical-robots)
- [When AI Gets Physical Hands: OpenClaw on Unitree G1](https://evoailabs.medium.com/when-ai-gets-physical-hands-a-review-of-openclaw-on-the-unitree-g1-and-other-robots-0fbf06a1d4c8)

### 中文资源
- [OpenClaw 中文教程合集](https://github.com/xianyu110/awesome-openclaw-tutorial)
- [OpenClaw 工作原理 - 菜鸟教程](https://www.runoob.com/ai-agent/openclaw-how-it-works.html)
