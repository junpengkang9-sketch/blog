# Python 工程基础

> 目标：不是把 Python 语法重新学一遍，而是建立能支撑后端与 AI 应用开发的工程能力。

## 核心地图

Python 工程基础包含：

- 语言基础：OOP、Data Model、Type Hints
- 项目结构：module / package / src layout
- 项目配置：pyproject.toml
- 依赖管理：uv
- 环境隔离：virtual environment
- 发布与构建：build / package

## Python 官方文档
- 官网：https://www.python.org/
- Tutorial：https://docs.python.org/3/tutorial/
- Data Model：https://docs.python.org/3/reference/datamodel.html
- GitHub：https://github.com/python/cpython

## OOP 与 Data Model

建议重点理解：
- class / instance
- inheritance
- composition
- dunder methods
- iterator / generator
- context manager
- descriptor
- dataclass

真正重要的是理解 Python 对象模型，而不是只会写 class。

## Type Hints
- 官方：https://docs.python.org/3/library/typing.html
- typing spec：https://typing.python.org/

Type Hints 的价值：
- IDE 补全
- 静态检查
- API Schema
- Pydantic / FastAPI
- Agent Tool 参数约束

## Python Packaging
- Packaging Guide：https://packaging.python.org/
- pyproject.toml：https://packaging.python.org/en/latest/specifications/pyproject-toml/

现代 Python 项目建议把配置中心放到 pyproject.toml。

## uv
- 官网：https://docs.astral.sh/uv/
- GitHub：https://github.com/astral-sh/uv

uv 可以统一处理：
- Python 版本
- 虚拟环境
- 依赖
- lockfile
- scripts
- build
- publish

## 推荐项目结构

```text
project/
├── pyproject.toml
├── uv.lock
├── README.md
├── src/
│   └── app/
└── tests/
```

## 推荐工作流

```text
uv init
→ uv add
→ uv run
→ uv lock
→ uv sync
```

## 我的结论

现代 Python 项目优先理解：

Python → pyproject.toml → uv → type hints → package structure

这比死记 pip / venv / requirements.txt 的各种组合更值得长期投入。
