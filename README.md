# LLM / AI 应用开发设计知识体系

这份知识库用于系统理解现代 LLM 应用、RAG、Agent、Tool Calling、Embedding、向量检索、知识库、Memory、模型微调、评测、推理与 AI 应用工程之间的关系。

目标不是背概念，而是建立一张可以用于**技术设计、Case 面试、系统架构和实际落地**的知识地图。

## 一、先建立总图

```text
                           ┌─────────────────────┐
                           │   Foundation Model  │
                           │ Transformer / LLM   │
                           └──────────┬──────────┘
                                      │
                         Pretraining / Alignment
                                      │
                                      ▼
                           ┌─────────────────────┐
                           │   Model Capability  │
                           │ Reasoning / Coding  │
                           │ Instruction Follow  │
                           └──────────┬──────────┘
                                      │
                  ┌───────────────────┼───────────────────┐
                  │                   │                   │
                  ▼                   ▼                   ▼
             Prompt/Context       Fine-tuning         Inference
                  │                   │                   │
                  └───────────────────┼───────────────────┘
                                      ▼
                           ┌─────────────────────┐
                           │   Application Layer │
                           └──────────┬──────────┘
                                      │
             ┌────────────────────────┼────────────────────────┐
             │                        │                        │
             ▼                        ▼                        ▼
           RAG                    Agent / Tool             Workflow
             │                        │                        │
     ┌───────┼────────┐        ┌──────┼────────┐              │
     ▼       ▼        ▼        ▼      ▼        ▼              ▼
  Parsing  Retrieval Rerank  Router Function Memory       Deterministic
             │        │        Call    │                  Pipeline
             ▼        ▼         │      ▼
          Vector /   Cross      │   Short/Long
          Keyword    Encoder    │   Term Memory
          Hybrid     / LLM      │
             │                   │
             └──────────┬────────┘
                        ▼
                 Context Construction
                        │
                        ▼
                  Generation / Action
                        │
                        ▼
                Evaluation / Observability
                        │
                        ▼
             Offline Eval + Online Metrics
                        │
                        ▼
                   Iteration Loop
```

---

# 二、最重要的认知：不要把这些东西当成并列名词

很多初学者会把：

- Embedding
- Vector DB
- RAG
- Agent
- Function Calling
- Prompt
- Fine-tuning
- Memory

理解成“八种 AI 技术”。

实际上它们处在完全不同的层级。

### 模型层

解决：

> 模型本身能不能理解、推理、生成和遵循指令？

包括：

- Transformer
- Attention
- Pretraining
- SFT
- RL / Preference Optimization
- Base Model
- Reasoning Model

### 知识层

解决：

> 模型本身没有的外部知识，怎么提供给它？

包括：

- Document
- Chunking
- Embedding
- Vector Search
- Keyword Search
- Hybrid Search
- Reranker
- RAG
- Knowledge Graph
- LLM Wiki / Structured Knowledge

### 行动层

解决：

> 模型怎么操作外部世界？

包括：

- Tool Calling
- Function Calling
- API
- Agent
- Workflow
- Browser / Computer Use
- MCP 类工具协议

### 记忆层

解决：

> 系统怎么保存跨轮次、跨任务的信息？

包括：

- Conversation History
- Short-term Memory
- Long-term Memory
- User Profile
- Episodic Memory
- Semantic Memory
- State Store

### 系统层

解决：

> 这些东西怎么稳定、低延迟、低成本地运行？

包括：

- Serving
- KV Cache
- Batching
- GPU
- Quantization
- Caching
- Retry
- Rate Limit
- Observability

### 评测层

解决：

> 怎么知道系统真的变好了？

包括：

- Golden Dataset
- Retrieval Recall
- Precision
- Answer Accuracy
- Task Success
- Tool Success
- Latency
- Cost
- Online A/B Test
- Regression Test

---

# 三、实际项目应该按什么顺序做？

一个真实 AI 应用通常不是：

```text
先上向量数据库
→ 再上 Agent
→ 再加 Prompt
```

而应该按照问题倒推。

## Step 1：定义任务

先回答：

```text
用户到底想完成什么？
```

例如：

> 用户希望根据企业内部制度查询请假规则。

定义：

```text
Input
Output
Success Criteria
Failure Criteria
```

如果成功标准都没定义，后面无法评测。

---

# 四、先判断需不需要 RAG

这是非常关键的架构决策。

### 不需要 RAG

如果知识：

- 很稳定
- 很通用
- 已经在模型知识中
- 不需要企业私有数据

直接：

```text
User → LLM → Answer
```

### 需要 RAG

如果：

- 企业私有知识
- 经常更新
- 文档规模较大
- 要求答案有出处
- 模型本身不知道

使用：

```text
User
 ↓
Retriever
 ↓
Relevant Context
 ↓
LLM
```

---

# 五、RAG 的完整链路

```text
                    Offline
                       │
Raw Documents
      ↓
Parsing
      ↓
Cleaning
      ↓
Chunking
      ↓
Metadata
      ↓
Embedding
      ↓
Index
      │
      ▼
                 Vector / Search DB


                    Online
                       │
User Query
      ↓
Query Rewrite / Expansion
      ↓
Retriever
      ↓
Top-K
      ↓
Reranker
      ↓
Context Construction
      ↓
LLM
      ↓
Answer + Citations
```

---

# 六、Chunking 为什么重要？

Embedding 并不是“把整个 PDF 扔进去”。

例如一本 500 页手册：

```text
500 pages
 ↓
documents
 ↓
sections
 ↓
paragraphs
 ↓
chunks
```

Chunk 太大：

```text
Context 噪音 ↑
检索精度 ↓
```

Chunk 太小：

```text
语义不完整
上下文缺失
```

所以 Chunking 是 Retrieval Quality 的基础。

常见策略：

- Fixed-size
- Sliding Window
- Sentence-based
- Paragraph-based
- Heading-aware
- Semantic Chunking

实际项目一般优先利用文档结构，而不是机械地每 500 tokens 切一次。

---

# 七、Embedding 到底解决什么问题？

Embedding 把文本映射到向量空间：

```text
Text
 ↓
Embedding Model
 ↓
Vector
```

例如：

```text
"公司年假怎么计算"
        ↓
[0.12, -0.73, 0.41, ...]
```

语义相近的文本，希望在向量空间中更接近。

常见相似度：

```text
Cosine Similarity
Dot Product
Euclidean Distance
```

所以：

> Embedding ≠ Search。

Embedding 是表示方法。

Vector Search 才是利用这种表示做检索。

---

# 八、Vector Search 怎么工作？

```text
Documents
 ↓
Embedding
 ↓
Vectors
 ↓
Vector Index

Query
 ↓
Embedding
 ↓
Query Vector
 ↓
Nearest Neighbor Search
 ↓
Top-K
```

如果数据只有几千条，可以暴力计算。

数据达到百万、千万级时，需要 ANN：

- HNSW
- IVF
- PQ
- DiskANN 等

这里进入 Vector Database / Vector Index。

---

# 九、为什么实际企业 RAG 很少只做 Vector Search？

因为不同搜索方法擅长不同问题。

### Keyword Search

擅长：

- SKU
- 编号
- 人名
- 专有名词
- 精确词汇
- 数字

### Vector Search

擅长：

- 语义相似
- 同义表达
- 意图匹配

### Hybrid Search

把两者结合：

```text
Query
 ├── Keyword Search
 └── Vector Search
          ↓
       Fusion
          ↓
       Reranker
          ↓
         Top-K
```

所以企业 RAG 常见路线：

```text
Hybrid Retrieval
+
Reranking
```

---

# 十、Reranker 和 Embedding 是什么关系？

Embedding Retrieval 通常追求：

> 快速从大量候选中找到可能相关的内容。

Reranker 追求：

> 更准确地判断候选与 Query 的相关性。

所以：

```text
1,000,000 documents
       ↓
Vector Search
       ↓
Top 100
       ↓
Reranker
       ↓
Top 10
       ↓
LLM
```

这叫：

```text
First-stage Retrieval
+
Second-stage Ranking
```

不要让昂贵的模型对 100 万文档逐个比较。

---

# 十一、RAG 最重要的指标

不能只看最终答案。

应该拆：

```text
Retrieval
   ↓
Recall@K
Precision@K
MRR
NDCG

Generation
   ↓
Faithfulness
Answer Relevance
Correctness

System
   ↓
Latency
Cost
```

一个非常重要的诊断逻辑：

```text
正确答案不在 Top-K
→ Retrieval Failure

正确答案在 Top-K
但 LLM 没用
→ Context / Generation Failure

LLM 使用了正确 Context
但回答错误
→ Generation / Reasoning Failure
```

---

# 十二、RAG 和 LLM Wiki / Structured Knowledge

传统 RAG：

```text
Query
 ↓
Search raw documents
 ↓
Top-K chunks
 ↓
LLM
```

另一种思路是：

```text
Raw Documents
 ↓
LLM
 ↓
Structured Knowledge
 ↓
Entities / Concepts / Relationships / Summaries
 ↓
LLM
```

它们并不是互斥的。

可以组合：

```text
                Knowledge Layer
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
       Vector       Keyword      Structured
       Search        Search       Knowledge
          │            │            │
          └────────────┼────────────┘
                       ▼
                    Rerank
                       ▼
                   Context
                       ▼
                      LLM
```

---

# 十三、什么时候需要 Knowledge Graph？

当问题不只是：

> “哪篇文档和我的问题最相似？”

而是：

> “A 和 B 是什么关系？”

例如：

```text
Company
  │
  ├── owns → Product
  │             │
  │             └── depends_on → Service
  │
  └── employs → Person
```

Graph 更适合显式关系。

Vector 更适合语义相似。

两者可以结合：

```text
Vector Retrieval
+
Graph Traversal
```

---

# 十四、Agent 是什么？

RAG 主要解决：

> 找知识。

Agent 主要解决：

> 完成任务。

典型：

```text
User
 ↓
LLM
 ↓
Decide
 ↓
Tool
 ↓
Observe
 ↓
Reason
 ↓
Tool
 ↓
Observe
 ↓
Final Answer
```

这与 ReAct 的思想相关：

```text
Reason → Act → Observe → Reason
```

---

# 十五、Function Calling 和 Agent 的关系

Function Calling 本身不是 Agent。

它只是：

> LLM 生成结构化 Tool Call 的能力。

例如：

```json
{
  "name": "get_weather",
  "arguments": {
    "city": "Shanghai"
  }
}
```

Agent 则是在此基础上增加：

```text
Planning
+
Tool Selection
+
Execution
+
Observation
+
State
+
Iteration
```

所以：

```text
Function Calling
       ↓
Tool Use
       ↓
Agent
```

不是完全等价关系。

---

# 十六、Agent 和 Workflow 也不能混

Workflow：

```text
A
↓
B
↓
C
↓
D
```

路径基本固定。

Agent：

```text
A
 ↓
LLM 决策
 ↓
选择 B / C / D
 ↓
观察结果
 ↓
再次决策
```

因此：

> 能确定流程时，优先 Workflow；需要动态决策时，再引入 Agent。

这是实际系统设计中非常重要的原则。

---

# 十七、Function Call 成功率低怎么办？

完整排查树：

```text
Function Call Failure
│
├── Base Model Capability
│
├── Instruction Following
│
├── Tool Selection
│
├── Tool Retrieval
│
├── Tool Description
│
├── Schema
│
├── Argument Generation
│
├── Structured Decoding
│
├── Context
│
└── Tool Execution
    ├── Timeout
    ├── 5xx
    ├── Rate Limit
    └── Permission
```

这也是一个典型企业 Case。

---

# 十八、基座模型和应用层的关系

整个 AI Stack 可以理解成：

```text
                 Base Model
                     │
       ┌─────────────┼──────────────┐
       │             │              │
     SFT            RL          Inference
       │             │              │
       └─────────────┼──────────────┘
                     ▼
                  LLM API
                     │
       ┌─────────────┼──────────────┐
       ▼             ▼              ▼
     Prompt         RAG           Tool
       │             │              │
       └─────────────┼──────────────┘
                     ▼
                   Agent
                     │
                     ▼
                 Application
```

如果应用效果不好，不应该默认是 Prompt 问题。

可能是：

```text
Model Capability
Data
Training
Retrieval
Context
Tool
Execution
```

---

# 十九、Prompt、RAG、Fine-tuning 怎么选择？

这是企业面试非常高频的问题。

### Prompt

解决：

> 如何告诉模型完成任务。

成本低、迭代快。

---

### RAG

解决：

> 模型缺少外部知识。

尤其适合：

```text
私有知识
动态知识
需要引用
```

---

### Fine-tuning

解决：

> 模型行为、格式、风格、任务能力需要稳定改变。

例如：

```text
Classification
Structured Output
Domain Style
Tool Use
```

---

### 三者可以组合

```text
Base Model
   ↓
Fine-tuning
   ↓
Prompt
   ↓
RAG
   ↓
Tool
   ↓
Agent
```

不要认为：

```text
RAG vs Fine-tuning
```

一定只能选一个。

它们解决不同问题。

---

# 二十、Memory 是什么？

Conversation History：

```text
当前对话
```

Memory：

```text
跨对话长期信息
```

可以进一步分：

```text
Short-term Memory
Long-term Memory
Semantic Memory
Episodic Memory
User Profile
Task State
```

例如：

```text
User Profile:
喜欢简洁回答

Task State:
当前正在处理合同

Conversation:
最近三轮对话
```

---

# 二十一、Context Engineering

现代 Agent/RAG 系统里，一个非常重要的概念是：

> 不只是 Prompt Engineering，而是 Context Engineering。

也就是：

```text
System Instruction
+
Conversation
+
Retrieved Documents
+
Tool Results
+
Memory
+
User State
+
Task State
```

全部决定模型看到什么。

因此：

```text
Model quality
```

并不等于：

```text
Application quality
```

因为模型实际接收到的是：

```text
Model
+
Context
```

---

# 二十二、为什么 Context 太长反而可能变差？

因为：

```text
Context ↑
Token Cost ↑
Latency ↑
Noise ↑
```

而且模型不一定会均匀利用所有信息。

所以 RAG 的目标不是：

> 尽可能塞更多文档。

而是：

> **给模型最有用的最小充分 Context。**

这也是 Retrieval、Reranking、Context Compression 的意义。

---

# 二十三、Inference 为什么也是核心？

模型训练完不代表系统完成。

在线推理涉及：

```text
Prefill
Decode
KV Cache
Batching
GPU Memory
Quantization
Scheduling
```

例如：

```text
User Requests
      ↓
Scheduler
      ↓
Batch
      ↓
LLM
      ↓
KV Cache
      ↓
Tokens
```

这里会连接：

- FlashAttention
- PagedAttention
- vLLM
- Quantization
- Continuous Batching

---

# 二十四、为什么 KV Cache 重要？

自回归生成：

```text
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
...
```

每一步都需要 Attention。

KV Cache 保存过去 Token 的 Key / Value：

```text
Past Tokens
    ↓
K / V Cache
    ↓
Next Token
```

减少重复计算。

但：

```text
KV Cache
→ GPU Memory Consumption
```

因此长上下文、多并发时，KV Cache 成为系统瓶颈之一。

这就连接到：

```text
PagedAttention
vLLM
Serving
GPU Memory
```

---

# 二十五、Quantization

如果模型：

```text
FP16
```

变成：

```text
INT8
INT4
```

通常可以降低：

```text
Memory
Cost
Latency
```

但可能带来：

```text
Accuracy / Quality Loss
```

所以需要实际 Benchmark，而不是认为“量化一定更好”。

---

# 二十六、Evaluation 是贯穿所有模块的

任何优化都应该回答：

```text
Before
 ↓
Change
 ↓
After
```

例如：

```text
RAG
Recall@10: 72% → 91%

Function Calling
Tool Accuracy: 81% → 94%

Agent
Task Success: 64% → 78%

System
P95 Latency: 2.8s → 1.7s

Cost
$0.018/request → $0.011/request
```

这就是工程化。

---

# 二十七、一个完整企业 AI 项目应该怎么落地？

建议实际顺序：

```text
1. 明确业务任务
        ↓
2. 定义 Success Metrics
        ↓
3. 建 Golden Dataset
        ↓
4. 选择 Base Model
        ↓
5. 做最简单 Baseline
        ↓
6. 判断是否需要 RAG
        ↓
7. 文档解析 / Chunking
        ↓
8. Embedding / Index
        ↓
9. Retrieval
        ↓
10. Reranking
        ↓
11. Context Construction
        ↓
12. Prompt
        ↓
13. Generation
        ↓
14. 如果需要行动 → Tool Calling
        ↓
15. 多步动态任务 → Agent
        ↓
16. Memory / State
        ↓
17. Evaluation
        ↓
18. Observability
        ↓
19. Latency / Cost Optimization
        ↓
20. Online Experiment
        ↓
21. Regression
        ↓
22. 持续迭代
```

注意：

**不是每个项目都需要走完所有步骤。**

---

# 二十八、一个实际例子：企业内部 AI 助手

需求：

> 员工可以询问公司制度，并让系统执行一些操作。

架构：

```text
                     User
                       │
                       ▼
                  LLM / Router
                       │
          ┌────────────┼─────────────┐
          ▼            ▼             ▼
        RAG          Memory        Tools
          │            │             │
          ▼            ▼             ▼
     Company Docs   User State    HR APIs
          │
          ▼
    Hybrid Retrieval
          │
          ▼
       Reranker
          │
          ▼
       Context
          │
          └──────────┐
                     ▼
                    LLM
                     │
            ┌────────┴────────┐
            ▼                 ▼
          Answer            Tool Call
                              │
                              ▼
                            API
                              │
                              ▼
                           Result
                              │
                              ▼
                             LLM
```

例如用户：

> 我今年还有多少年假？

系统可能：

```text
1. Memory / User State
   → user_id

2. Tool
   → get_leave_balance(user_id)

3. RAG
   → 查询年假规则

4. LLM
   → 综合个人余额 + 公司规则

5. Answer
```

这里同时用了：

```text
Memory
+
Tool Calling
+
RAG
+
LLM
```

---

# 二十九、最值得建立的“关联图”

```text
Transformer
   │
   ├── Attention
   │
   ├── Position Encoding / RoPE
   │
   └── Decoder
         │
         ▼
       GPT
         │
         ├── Scaling Laws
         │
         ├── Pretraining
         │
         ├── SFT
         │
         └── RL / Preference
                │
                ▼
              LLM
                │
     ┌──────────┼──────────┐
     │          │          │
   Prompt      RAG       Tool Use
     │          │          │
     │      Embedding      │
     │          │          Function Calling
     │      Vector Search  │
     │          │          │
     │       Reranker       │
     │          │          │
     └──────────┼──────────┘
                ▼
             Context
                │
                ▼
              Agent
          ┌─────┼─────┐
          ▼     ▼     ▼
       Memory  Tools  Workflow
          │     │
          └─────┘
             │
             ▼
          Application
             │
       ┌─────┴─────┐
       ▼           ▼
    Evaluation  Observability
       │           │
       └─────┬─────┘
             ▼
        Optimization
```

---

# 三十、最终你应该形成的思维方式

遇到一个 AI Case，不要问：

> “我要不要用 RAG？”

而是依次问：

```text
① 模型知道吗？
       ↓
② 如果不知道，是需要外部知识吗？
       ↓
③ 知识在哪里？
       ↓
④ 怎么切？
       ↓
⑤ 怎么表示？
       ↓
⑥ 怎么检索？
       ↓
⑦ 怎么排序？
       ↓
⑧ 给模型多少 Context？
       ↓
⑨ 模型能不能正确理解？
       ↓
⑩ 是否需要行动？
       ↓
⑪ 是否需要 Tool？
       ↓
⑫ 是否需要多步 Agent？
       ↓
⑬ 是否需要 Memory？
       ↓
⑭ 怎么评测？
       ↓
⑮ 怎么降低成本 / 延迟？
       ↓
⑯ 怎么监控回归？
```

这套顺序比背各种框架名称重要得多。

---

# 三十一、面试 Case 的统一分析框架

以后遇到：

> RAG 效果差

拆：

```text
Parsing
→ Chunking
→ Embedding
→ Retrieval
→ Reranking
→ Context
→ Generation
```

遇到：

> Function Call 成功率低

拆：

```text
Base Model
→ SFT / Alignment
→ Prompt
→ Tool Retrieval
→ Tool Selection
→ Schema
→ Arguments
→ Execution
```

遇到：

> Agent 成功率低

拆：

```text
Planning
→ Tool Selection
→ Execution
→ Observation
→ State
→ Memory
→ Loop
```

遇到：

> LLM 成本高

拆：

```text
Model
→ Token
→ Context
→ Retrieval
→ Cache
→ Routing
→ Quantization
→ Serving
```

遇到：

> LLM 延迟高

拆：

```text
TTFT
→ Prefill
→ Decode
→ KV Cache
→ Batch
→ GPU
→ Network
→ Tool Latency
```

遇到：

> AI 产品效果差

最后都回到：

```text
Task Definition
→ Evaluation
→ Error Taxonomy
→ Bottleneck
→ Experiment
→ Measurement
```

---

## 这份知识库的核心原则

> **模型不是应用。RAG 不是 Vector DB。Vector DB 不是 Embedding。Function Calling 不是 Agent。Agent 不是 Workflow。Prompt 不是全部的 Context。Context 不是 Knowledge。Knowledge 也不等于 Retrieval。**

真正的 AI 应用是：

```text
Model Capability
+
Data / Knowledge
+
Context
+
Retrieval
+
Reasoning
+
Tools
+
State
+
System Engineering
+
Evaluation
```

最终目标是：

```text
             User Task
                 ↓
        ┌────────────────┐
        │  AI Application │
        └───────┬────────┘
                ↓
      ┌─────────┴─────────┐
      ↓                   ↓
   Knowledge            Action
      │                   │
   Retrieval             Tools
      │                   │
   RAG / Graph          Agent
      └─────────┬─────────┘
                ↓
               LLM
                ↓
             Answer
                ↓
            Evaluation
                ↓
            Iteration
```

