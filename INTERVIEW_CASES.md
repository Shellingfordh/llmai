# LLM / AI 企业面试 Case 手册

## 统一答题框架

面对任何 AI Case，先不要直接给技术方案。

```text
定义问题
→ 明确成功指标
→ 拆解链路
→ 建立 Error Taxonomy
→ 找 Bottleneck
→ 提出 Hypothesis
→ 设计 Experiment
→ Offline Evaluation
→ Online Experiment
→ Observability
→ Regression
```

## Case 1：Function Calling 成功率低

### 先拆指标

```text
E2E Success
├── Tool Selection
├── Argument Accuracy
├── Schema Validity
├── Tool Execution
└── Result Handling
```

### 排查顺序

1. 基座模型 Tool-use 能力 Benchmark
2. 模型版本 / 推理参数
3. Prompt / Context
4. Tool Retrieval
5. Tool Description
6. Schema
7. Structured Output / Constrained Decoding
8. Execution reliability

### 如果是模型能力问题

```text
换更合适的模型
→ 高质量 Tool-use SFT
→ Preference Optimization / RL
```

### 如果是系统问题

```text
Tool Retrieval
→ Schema
→ Validator
→ Retry / Fallback
```

### 关键指标

- Tool Selection Accuracy
- Argument Accuracy
- Schema Validity
- Execution Success
- Task Completion
- Latency
- Cost

---

## Case 2：RAG 答案不准

拆成：

```text
Document Parsing
→ Chunking
→ Embedding
→ Retrieval
→ Reranking
→ Context Construction
→ Generation
```

### 诊断

```text
Ground Truth 不在 Top-K
→ Retrieval Failure

Ground Truth 在 Top-K
但模型没用
→ Context / Generation Failure

Context 正确
答案仍错误
→ Generation / Reasoning Failure
```

### 指标

```text
Recall@K
Precision@K
MRR
NDCG
Faithfulness
Answer Relevance
Correctness
```

---

## Case 3：Agent 成功率低

```text
Intent
→ Planning
→ Tool Selection
→ Tool Execution
→ Observation
→ State
→ Next Action
→ Final Answer
```

分别评估每一步。

不要把所有失败都归因于模型。

---

## Case 4：成本过高

```text
Total Cost
=
Input Tokens
+
Output Tokens
+
Retrieval
+
Tool
+
Model Calls
```

优化顺序：

```text
减少无效 Context
→ Cache
→ Model Routing
→ Smaller Model
→ Prompt Compression
→ Retrieval Optimization
→ Quantization / Serving
```

---

## Case 5：延迟过高

拆：

```text
Network
+
Queue
+
Prefill
+
Decode
+
Tool Latency
+
Retrieval
```

重点指标：

- TTFT
- TPOT
- E2E Latency
- P50
- P95
- P99

不要只看平均延迟。

---

## Case 6：要不要 Fine-tuning？

先判断：

```text
知识缺失？
→ RAG

行为 / 格式 / 特定任务能力不稳定？
→ Fine-tuning

指令表达不清？
→ Prompt / Context

工具选择不稳定？
→ Tool Schema / Retrieval / Model Capability / SFT

```

不是所有问题都应该 Fine-tune。

---

## Case 7：要不要 Agent？

先问：

```text
流程是否固定？
```

如果固定：

```text
Workflow
```

如果需要动态决策：

```text
Agent
```

如果只是一次工具调用：

```text
Function Calling
```

---

## Case 8：向量搜索为什么效果差？

排查：

```text
Embedding Model
→ Query / Document mismatch
→ Chunking
→ Index
→ ANN parameters
→ Top-K
→ Hybrid Search
→ Reranker
```

---

# 面试中常见的技术关联

| 概念 | 主要解决的问题 | 直接关联 |
|---|---|---|
| Transformer | LLM 基础架构 | Attention / GPT |
| Attention | Token 间信息交互 | Transformer |
| RoPE | 位置信息 | Attention / 长上下文 |
| Scaling Law | 模型/数据/计算关系 | Pretraining |
| SFT | 行为和指令遵循 | Instruction Following |
| DPO/RL | Preference / Alignment | SFT / Reasoning |
| Embedding | 语义表示 | Vector Search |
| Vector Search | 语义召回 | RAG |
| BM25 | 关键词召回 | Hybrid Search |
| Reranker | 二阶段精排 | RAG |
| RAG | 外部知识增强生成 | Retrieval + LLM |
| Knowledge Graph | 显式关系 | RAG / Reasoning |
| Function Calling | 结构化调用工具 | Tool Use |
| Agent | 动态任务执行 | Tool + State + Reasoning |
| Workflow | 确定性流程 | Agent |
| Memory | 跨轮次状态/信息 | Agent |
| KV Cache | 加速自回归生成 | Inference |
| FlashAttention | Attention GPU 效率 | Inference |
| PagedAttention | KV Cache 管理 | Serving |
| Quantization | 降低推理成本 | Serving |
| Evaluation | 判断系统是否有效 | 全链路 |

---

# 最重要的实际应用顺序

```text
业务问题
  ↓
Task Definition
  ↓
Evaluation Set
  ↓
Base Model
  ↓
Baseline
  ↓
Prompt / Context
  ↓
是否需要外部知识？
  ├─ No → 继续
  └─ Yes
       ↓
     RAG
       ↓
   Retrieval
       ↓
   Reranking
  ↓
是否需要执行动作？
  ├─ No → Generation
  └─ Yes
       ↓
   Function Calling
       ↓
是否需要动态多步决策？
  ├─ No → Workflow
  └─ Yes → Agent
                    ↓
                  Memory
                    ↓
                State / Tools
  ↓
Evaluation
  ↓
Latency / Cost
  ↓
Observability
  ↓
Regression
  ↓
持续迭代
```
