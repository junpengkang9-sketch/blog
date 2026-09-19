# Python Web 后端与 API

> 目标：搭出可上线的 AI / Agent 后端，而不是只写一个本地脚本。

## 推荐技术栈

```text
FastAPI
↓
Pydantic
↓
SQLAlchemy
↓
PostgreSQL
```

## FastAPI
- 官网：https://fastapi.tiangolo.com/
- Tutorial：https://fastapi.tiangolo.com/tutorial/
- GitHub：https://github.com/fastapi/fastapi

重点理解：
- Path / Query / Body
- Dependency Injection
- Middleware
- Exception Handling
- Background Tasks
- StreamingResponse
- WebSocket
- OpenAPI
- lifespan

## Pydantic
- 官网：https://docs.pydantic.dev/
- GitHub：https://github.com/pydantic/pydantic

核心模型：

```text
External JSON
↓
Validation
↓
Python Object
↓
Serialization
↓
JSON / JSON Schema
```

它和 FastAPI、Structured Output、Tool Calling、MCP Schema 都关系很深。

## SQLAlchemy
- 官网：https://www.sqlalchemy.org/
- Tutorial：https://docs.sqlalchemy.org/en/20/tutorial/
- GitHub：https://github.com/sqlalchemy/sqlalchemy

直接学习 SQLAlchemy 2.x 思维。

重点：
- Engine
- Connection
- Session
- ORM
- select
- transaction
- relationship
- async engine

## PostgreSQL
- 官网：https://www.postgresql.org/
- Docs：https://www.postgresql.org/docs/

AI 应用里通常会存：
- user
- conversation
- message
- agent run
- tool call
- config
- evaluation result

## API 设计建议

优先做到：
- 输入输出有 Schema
- 错误结构统一
- Request ID
- Logging
- Timeout
- Rate Limit
- Auth
- Observability

## 一个基础 Agent API

```text
POST /chat
   ↓
Pydantic validate
   ↓
Agent service
   ↓
Tool / LLM
   ↓
Streaming response
   ↓
Tracing + persistence
```

## 我的结论

FastAPI 的价值不仅是“快速写 API”。

真正要掌握的是：

HTTP API + Schema + Async + Persistence + Error Handling + Observability
