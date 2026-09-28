# 我的阅读清单：面向游戏 AI NPC 方向

> 本仓库 Fork 自 [youngyangyang04/llm-master](https://github.com/youngyangyang04/llm-master)，文章版权归原作者。
> 这份清单是我按「做一个有记忆、会行动的 NPC」这个目标，从 170 多篇文章里挑出来重新排的顺序。
> 读完一篇就把 `[ ]` 改成 `[x]`。

**核心思路**：游戏 NPC 本质上就是一个 Agent。它要有性格设定（Prompt），能记住玩家（记忆），能做事（工具调用），还要稳定不出戏（失败处理与评估）。所以阅读重点放在 Agent 和记忆上，RAG、部署、原理按需补。

---

## 第 1 步：先搞懂基本概念（约 3 天）

- [ ] [大模型关键词全解：13 个核心概念](docs/llm/intro/llm_keywords.md)：先把 Prompt、Token、Agent、MCP 这些词对上号
- [ ] [大模型是怎么训练出来的](docs/llm/intro/how_llm_trained.md)：预训练、SFT、RLHF 是什么，一篇讲完
- [ ] [大模型应用开发到底在做什么](docs/llm/intro/app_dev_overview.md)：应用开发和算法岗的区别
- [ ] [Token、成本与延迟：三个硬约束](docs/llm/app/token_cost_latency.md)：NPC 要实时对话，延迟尤其重要

## 第 2 步：调 API 的基本功（约 1 周）

- [ ] [Prompt Engineering：结构化 Prompt 与角色设计](docs/llm/app/prompt_engineering.md)：NPC 的人设就写在 System Prompt 里
- [ ] [Few-shot、CoT 与自我反思](docs/llm/app/prompt_fewshot_cot_reflection.md)
- [ ] [结构化输出与 JSON Schema](docs/llm/app/structured_output.md)：让 NPC 输出「台词 + 动作 + 情绪」这类游戏能直接解析的格式
- [ ] [同步、异步、流式输出怎么选](docs/llm/app/streaming_output.md)：对话要逐字出来，就得用流式
- [ ] [Function Calling 详解](docs/llm/app/function_calling.md)：NPC 能「做事」（给道具、开门、战斗）靠的就是它

> 小练习：写一个脚本，让大模型扮演一个铁匠 NPC，每次都以 JSON 格式返回 `{台词, 情绪, 动作}`。

## 第 3 步：Agent 核心（重点，约 2 周）

- [ ] [Agent 到底是什么](docs/llm/app/agent_intro.md)：规划、工具、执行、反馈四个能力
- [ ] [Agent vs Workflow：什么时候根本不需要 Agent](docs/llm/app/agent_vs_workflow.md)：大部分 NPC 用固定流程就够了，要知道什么时候才值得上 Agent
- [ ] [工具设计决定 Agent 上限](docs/llm/app/agent_tool_design.md)：设计 NPC 能调用的「游戏动作」
- [ ] [ReAct、Reflection、规划执行三种思路](docs/llm/app/react_reflection_planning.md)
- [ ] [Plan-and-Execute 落地成 DAG 执行器](docs/llm/app/plan_execute_dag.md)：NPC 执行多步骤任务（比如先去市场、再买东西、再回家）
- [ ] [MCP 协议](docs/llm/app/mcp_protocol.md)：了解即可，是工具接入的新标准

## 第 4 步：记忆与上下文（NPC 的灵魂，约 1 周）

- [ ] [Agent 的记忆：短期、长期、RAG 什么关系](docs/llm/app/agent_memory.md)：**必读**。讲了四类记忆、写入要过筛、记忆也要会忘，这些正是 NPC 记住玩家的关键
- [ ] [Context Engineering 入门](docs/llm/app/context_engineering.md)：长对话怎么不爆上下文，滑动窗口、摘要压缩、分层记忆
- [ ] [为什么需要 RAG](docs/llm/app/why_rag.md)：游戏世界观、剧情设定可以做成知识库
- [ ] [RAG 完整链路拆解](docs/llm/app/chain_of_rag.md)
- [ ] [Embedding 是什么](docs/llm/app/embedding.md)
- [ ] [向量数据库解决了什么问题](docs/llm/app/vector_database.md)
- [ ] [Agentic RAG：RAG 怎么长出 Agent 能力](docs/llm/intro/agentic_rag.md)

## 第 5 步：让 NPC 稳定、不出戏（约 1 周）

- [ ] [Agent 为什么容易翻车](docs/llm/app/agent_failure_modes.md)
- [ ] [Agent 系统如何约束幻觉](docs/interview/llm/agent_hallucination_control_interview.md)：NPC 乱编剧情、说出不该知道的事，都是幻觉问题
- [ ] [上下文漂移与工具调用幻觉](docs/interview/llm/agent_drift_hallucination_interview.md)：聊久了人设跑偏，就是上下文漂移
- [ ] [Agent 怎么评估](docs/llm/app/agent_evaluation.md)：怎么证明你的 NPC 做得好，写进简历时要用到

## 第 6 步：多个 NPC 一起工作（进阶）

- [ ] [Planner、Worker、Reviewer 怎么分工](docs/llm/app/multi_agent_roles.md)
- [ ] [多 Agent 上下文、消息和 Token 怎么治理](docs/llm/app/multi_agent_context_governance.md)：一群 NPC 互相对话时的成本控制
- [ ] [多 Agent 通信与编排](docs/interview/llm/multi_agent_communication_interview.md)

## 第 7 步：性能与部署（有外呼机器人和压测经验，可以快速过）

- [ ] [云 API、托管推理还是自部署](docs/llm/app/deployment_options.md)
- [ ] [KV Cache、PagedAttention、Prefix Cache](docs/llm/app/kv_cache_paged_attention.md)
- [ ] [量化怎么选](docs/llm/app/model_quantization.md)：想让 NPC 在玩家本地显卡上跑，就得靠量化
- [ ] [大模型服务怎么压测](docs/llm/app/stress_testing.md)
- [ ] [什么时候微调、什么时候 RAG](docs/llm/app/finetuning_vs_rag.md)
- [ ] [LoRA / QLoRA](docs/llm/app/lora_qlora.md)：用小成本把模型微调成固定的角色口吻

## 第 8 步：补原理（可选，想走得更深再读）

按顺序读，后半部分是手写代码，建议边读边敲：

- [ ] [为什么所有大模型都绕不开 Transformer](docs/llm/transformer/transformer_base_1.md)
- [ ] [Q、K、V 是什么](docs/llm/transformer/qkv.md) → [Attention 计算全过程](docs/llm/transformer/qkv_cal.md) → [多头注意力](docs/llm/transformer/mha.md) → [位置编码](docs/llm/transformer/pos_encode.md)
- [ ] [手撕 Attention](docs/llm/transformer/attention_code.md) → [手撕多头](docs/llm/transformer/mha_code.md) → [手撕 Transformer Block](docs/llm/transformer/transformer_block_code.md) → [手撕 Tiny Transformer](docs/llm/transformer/tiny_transformer_code.md)

## 求职阶段再看（大三开始）

- [Agent 大厂面试题汇总](docs/interview/llm/agent_interview.md)
- [字节 Agent 开发四面面经](docs/interview/llm/20260506bytedance.md)
- [字节 Agent 应用开发实习一面](docs/interview/llm/bytedance_fanqie_agent_intern_interview.md)：项目被连续深挖时怎么答
- [RAG 面试题汇总](docs/interview/llm/rag_interview.md)
- [Transformer 面试题汇总](docs/interview/llm/transformer_interview.md)
- [大模型学习路线总览](docs/llm/README.md)、[求职与面试路线](docs/roadmap/interview.md)

## 暂时可以跳过

- `docs/llm/news/`：行业新闻，时效性强，有空刷刷就行
- `docs/llm/claude/`：Claude Code 使用技巧，属于提升写代码效率的工具，和 NPC 主线无关
- `docs/llm/intro/` 里标着「本文已迁移」的几篇：只剩一个跳转链接
- `docs/qita/`：会员充值相关

---

## 配套项目：有记忆的 NPC Agent

读完第 1～5 步后做这个项目，完成标准参考原仓库的 [Agent 阶段项目](docs/roadmap/agent.md)：

1. **人设**：System Prompt 定义性格、说话风格、知道和不知道的事
2. **结构化输出**：每轮返回 `{台词, 情绪, 动作}`，能被游戏逻辑直接解析
3. **工具**：至少 3 个游戏动作，比如给物品、查询背包、改变好感度
4. **记忆**：短期记忆（最近对话）+ 长期记忆（玩家名字、做过的事、好感度），有写入规则和遗忘规则
5. **世界观知识库**：用 RAG 回答游戏设定问题，查不到就不乱编
6. **评估**：准备 30 条固定测试对话，统计人设一致率、工具调用正确率、幻觉次数

> 这个仓库没怎么讲、需要另外补的 NPC 专属内容：长期人设一致性、情绪状态机、和游戏引擎（Unity / Unreal）对接、实时语音对话（可以参考自己做过的 ASR + LLM + TTS 外呼链路）。
