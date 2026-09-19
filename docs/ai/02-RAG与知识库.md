# RAG 与知识库

> RAG 的核心不是“接一个向量数据库”，而是如何把正确上下文稳定地找出来。

## 完整链路

```text
Document
↓
Parsing
↓
Chunking
↓
Metadata
↓
Embedding
↓
Index
↓
Retrieval
↓
Hybrid Search
↓
Rerank
↓
Context
↓
LLM
↓
Evaluation
```

## Embedding

### Sentence Transformers
- 官网：https://www.sbert.net/
- GitHub：https://github.com/huggingface/sentence-transformers

核心模型：

Text → Embedding → Similarity → Retrieval

## LlamaIndex
- 官网：https://docs.llamaindex.ai/
- GitHub：https://github.com/run-llama/llama_index

值得学习：
- Document / Node
- Node Parser
- Index
- Retriever
- Query Engine
- Router
- Metadata

## Qdrant
- 官网：https://qdrant.tech/
- Docs：https://qdrant.tech/documentation/
- GitHub：https://github.com/qdrant/qdrant
- Hybrid Search：https://qdrant.tech/documentation/search/text-search/hybrid-search/

## Retrieval

不要只学 Dense Search。

成熟一些的检索体系通常包含：

```text
Dense Retrieval
+
Sparse / Lexical Retrieval
+
Metadata Filter
+
Fusion
+
Reranking
```

## Chunking

重点问题：
- chunk 多大
- overlap 多大
- 是否按标题 / 段落切
- 表格怎么处理
- 代码怎么处理
- metadata 怎么保留
- Parent / Child retrieval 是否需要

没有统一的“最佳 chunk size”。

## Reranking

第一阶段召回追求 Recall，第二阶段 rerank 再提升 Precision。

典型：

```text
Top 50 Retrieval
↓
Reranker
↓
Top 5 Context
```

## RAG Evaluation

### Ragas
- 官网：https://docs.ragas.io/
- GitHub：https://github.com/explodinggradients/ragas

关注：
- Context Precision
- Context Recall
- Faithfulness
- Response Relevancy

## 我的结论

RAG 的工程价值主要来自四件事：

1. 数据解析质量
2. Retrieval
3. Reranking
4. Evaluation

Vector DB 只是其中一个组件。
