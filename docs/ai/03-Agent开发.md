# Agent 开发

> 不从框架开始。先理解 Agent Loop，再理解框架帮你解决了什么。

## 最小 Agent

```text
User
 ↓
LLM
 ↓
Decide
 ↓
Tool Call
 ↓
Tool Result
 ↓
LLM
 ↓
Answer
```

如果这个循环自己写不明白，直接上复杂 Agent Framework 很容易只会配置。

## 核心能力

- Tool Calling
- Structured Output
- Context Management
- Memory
- Planning
- Handoff
- Sub-agent
- Guardrail
- Human-in-the-loop
- Retry / Timeout
- Tracing
- Evaluation

## OpenAI Agents SDK
- Python Docs：https://openai.github.io/openai-agents-python/
- GitHub：https://github.com/openai/openai-agents-python

适合理解：
- Agent
- Tool
- Handoff
- Guardrail
- Session
- Tracing

## LangGraph
- Docs：https://docs.langchain.com/oss/python/langgraph/overview
- GitHub：https://github.com/langchain-ai/langgraph

适合：
- 有状态 Workflow
- 持久化
- Human-in-the-loop
- 长任务
- 自定义 Agent Graph

核心概念：State、Node、Edge、Checkpoint。

## LangChain
- Docs：https://docs.langchain.com/
- GitHub：https://github.com/langchain-ai/langchain

建议学习它的 abstractions 和 integrations，不需要背完整 API。

## Deep Agents
- Docs：https://docs.langchain.com/oss/python/deepagents/overview
- GitHub：https://github.com/langchain-ai/deepagents

值得研究：
- planning
- filesystem
- sub-agents
- context management
- long-horizon tasks

## PydanticAI
- 官网：https://ai.pydantic.dev/
- GitHub：https://github.com/pydantic/pydantic-ai

对于 Python 开发者很值得看：类型安全、依赖注入、Tool schema 与 Pydantic 生态结合得自然。

## Dify
- 官网：https://dify.ai/
- Docs：https://docs.dify.ai/
- GitHub：https://github.com/langgenius/dify

适合快速理解 Workflow、Knowledge、Tool、Agent，并快速验证业务。

## 框架怎么选

简单 Tool Agent → 先原生 SDK / OpenAI Agents SDK / PydanticAI

复杂状态流程 → LangGraph

低代码验证业务 → Dify

复杂长任务 / Sub-agent → Deep Agents 等更高层 harness

## 我的结论

框架不是能力本身。

真正应该掌握的是：

```text
Model
+
Context
+
Tool
+
State
+
Control Flow
+
Observability
+
Evaluation
```

只要这些理解清楚，框架换掉也不会重新学一遍。
