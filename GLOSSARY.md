# LLM / AI 设计知识词典

## Model

### Base Model
经过大规模预训练、主要具备通用语言建模能力的模型。它是应用层能力的基础。

### SFT
Supervised Fine-Tuning。通过高质量监督数据改变模型行为、格式遵循和特定任务能力。

### Preference Optimization
利用偏好数据优化模型输出，典型方法包括 DPO 等。

### Reasoning
让模型在复杂任务中进行更长或更结构化的推理。

---

## Retrieval

### Embedding
将文本、图片等对象映射到向量空间中的表示。

### Vector Search
基于向量相似度进行近邻检索。

### ANN
Approximate Nearest Neighbor。用索引结构加速大规模近邻搜索。

### HNSW
一种常见的图结构 ANN 索引。

### BM25
经典的词法检索方法，适合精确关键词匹配。

### Hybrid Search
通常将词法搜索和向量搜索结合。

### Reranker
对初步召回的候选进行二阶段精排。

### RAG
Retrieval-Augmented Generation。先检索外部信息，再将相关信息提供给生成模型。

---

## Agent

### Tool / Function Calling
让模型输出结构化调用请求，由系统执行外部函数/API。

### Workflow
预先定义的确定性任务流程。

### Agent
根据当前状态和观察结果动态决定下一步行动的系统。

### Memory
保存跨轮次或跨任务的信息、状态和经验。

---

## Context

### Context Engineering
系统性设计模型实际看到的所有上下文：

```text
System Instruction
+
Conversation
+
Memory
+
Retrieved Documents
+
Tool Results
+
Task State
+
User State
```

### Context Compression
减少无关或重复上下文，降低 token、延迟和噪声。

---

## Inference

### KV Cache
缓存已经计算过的 Attention Key/Value，减少自回归生成中的重复计算。

### FlashAttention
面向 GPU IO 的高效 Attention 实现。

### PagedAttention
改善大规模 LLM Serving 中 KV Cache 内存管理的方法。

### Continuous Batching
在请求不断到达的情况下动态组织推理 batch，提高 GPU 利用率。

### Quantization
用更低精度表示模型参数或激活，以降低内存和计算成本。

---

## Evaluation

### Golden Dataset
人工确认正确答案、工具、参数或轨迹的数据集，用于离线评测。

### Recall@K
正确目标出现在前 K 个召回结果中的比例。

### Precision@K
前 K 个结果中真正相关结果的比例。

### MRR
Mean Reciprocal Rank，用于衡量第一个相关结果的排序位置。

### NDCG
用于评估具有不同相关性等级的排序质量。

### Task Success
最终任务是否完成，比单独 Tool Call Success 更接近真实产品价值。

### Regression Test
防止模型、Prompt、Retrieval、Tool 等更新导致已有能力下降。

---

# 最小关系图

```text
Embedding
   ↓
Vector Search
   ↓
Retrieval
   ↓
Reranker
   ↓
RAG
   ↓
Context
   ↓
LLM

LLM
 ↓
Function Calling
 ↓
Tool
 ↓
Agent
 ↓
Workflow / State / Memory

所有链路
 ↓
Evaluation
 ↓
Observability
 ↓
Optimization
```
