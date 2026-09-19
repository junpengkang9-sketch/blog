# MCP（Model Context Protocol）

> MCP 是 Agent / AI 应用连接外部工具和数据源的重要协议层。

## 官方入口
- 官网：https://modelcontextprotocol.io/
- GitHub Organization：https://github.com/modelcontextprotocol
- Specification：https://modelcontextprotocol.io/specification/
- Python SDK：https://github.com/modelcontextprotocol/python-sdk
- TypeScript SDK：https://github.com/modelcontextprotocol/typescript-sdk

## 基本架构

```text
Host
↓
MCP Client
↓
Protocol
↓
MCP Server
↓
Tool / Resource / Prompt
↓
External System
```

## 三个核心能力

### Tools
让模型执行动作，例如查询数据库、调用 API、创建任务。

### Resources
向模型暴露可读取的上下文和数据。

### Prompts
服务器提供可复用 Prompt 模板。

## Transport

重点理解：
- stdio
- HTTP / Streamable HTTP

stdio 很适合本地工具；HTTP 更适合远程服务与生产部署。

## MCP 与普通 Function Calling 的区别

Function Calling 更接近“模型如何描述一次工具调用”。

MCP 更接近：

```text
如何发现工具
如何描述能力
如何建立 Client / Server
如何读取 Resource
如何调用 Tool
如何做协议级交互
```

两者不是互相替代。

## 安全必须关注

- Tool 权限最小化
- 输入校验
- 输出过滤
- 用户确认
- 身份认证
- Authorization
- Prompt Injection
- 不可信 Resource
- 日志审计

不要把 MCP Server 当成“模型想调用什么就调用什么”的万能后门。

## 推荐学习顺序

1. Architecture
2. Tool
3. Resource
4. stdio
5. Streamable HTTP
6. Authorization
7. 自己实现一个最小 Server
8. 再接入真实服务

## 我的结论

MCP 的价值不是“又一个 Agent 框架”。

它更接近 AI 世界里的统一连接层：让 Host、Client 和外部能力之间有一套标准协议。
