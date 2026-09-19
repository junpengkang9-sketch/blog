# LLM 基础

> 目标：理解大模型运行的关键机制，够支撑 RAG、Agent 和推理优化，不要求走算法研究路线。

## 学习主线

```text
神经网络
↓
Forward
↓
Loss
↓
Backpropagation
↓
Gradient Descent
↓
Transformer
↓
Attention
↓
Token
↓
Context
↓
KV Cache
↓
Inference
```

## PyTorch
- 官网：https://pytorch.org/
- Learn the Basics：https://docs.pytorch.org/tutorials/beginner/basics/
- GitHub：https://github.com/pytorch/pytorch

重点：Tensor、Model、Autograd、Optimization。

## Dive into Deep Learning
- 官网：https://d2l.ai/
- 中文：https://zh.d2l.ai/
- GitHub：https://github.com/d2l-ai/d2l-en

适合用来补深度学习基础，不需要每章都学。

## Transformer
- 原论文：https://arxiv.org/abs/1706.03762
- Annotated Transformer：https://nlp.seas.harvard.edu/annotated-transformer/

核心概念：
- Self-Attention
- Multi-Head Attention
- Positional Information
- Feed Forward
- Residual
- LayerNorm

## Hugging Face
- LLM Course：https://huggingface.co/learn/llm-course/
- Transformers Docs：https://huggingface.co/docs/transformers/
- GitHub：https://github.com/huggingface/transformers

## Token 与 Context

需要理解：
- tokenizer
- token budget
- context window
- prompt / completion
- truncation
- context management

Agent 设计里，Context 往往比 Prompt 技巧更重要。

## KV Cache
- 官方文档：https://huggingface.co/docs/transformers/en/kv_cache

一句话：缓存历史 token 的 Key / Value，避免生成每个新 token 时重复计算整个历史。

它直接影响：
- decoding latency
- memory
- long context
- prefix reuse

## 推理时值得关注

- TTFT：Time To First Token
- Tokens / second
- Context length
- Batch
- Quantization
- Cache
- Streaming

## 我的结论

Agent 应用开发不需要先成为算法工程师。

至少要真正搞懂：Token、Transformer、Attention、Context、KV Cache、Inference。否则后面很多“优化”只能靠猜。
