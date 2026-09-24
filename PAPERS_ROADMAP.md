# LLM / AI 原理论文与学习路线

## 第一阶段：Transformer 与模型基础

1. Attention Is All You Need
2. BERT
3. GPT-2
4. GPT-3

核心问题：

```text
Attention 怎么工作？
为什么 Decoder-only 成为主流？
为什么 Scaling 有效？
```

## 第二阶段：Scaling 与训练

5. Scaling Laws for Neural Language Models
6. Training Compute-Optimal Large Language Models (Chinchilla)
7. InstructGPT
8. DPO

核心：

```text
Pretraining
→ SFT
→ Preference Optimization
```

## 第三阶段：高效推理

9. RoFormer / RoPE
10. FlashAttention
11. FlashAttention-2
12. PagedAttention / vLLM
13. MoE / Switch Transformer

核心：

```text
Model Quality
+
GPU Efficiency
+
Serving
```

## 第四阶段：应用层

14. Retrieval-Augmented Generation
15. ReAct
16. Chain-of-Thought
17. LoRA

核心：

```text
Knowledge
+
Reasoning
+
Tool Use
+
Fine-tuning
```

## 第五阶段：现代 Reasoning

18. DeepSeek-R1 及相关 reasoning / RL 工作

重点理解：

```text
Test-time Compute
+
RL
+
Verification
+
Reasoning
```

---

# 阅读论文的方法

不要只读 Abstract。

每篇至少回答：

1. 它解决什么问题？
2. 之前的方法为什么不够？
3. 核心技术是什么？
4. 改变了哪一层？
5. 代价是什么？
6. 有什么失败模式？
7. 后续哪些工作建立在它上面？
8. 在企业系统中对应什么组件？

例如 FlashAttention：

```text
不是：
“Attention 变成了新的数学公式”

而是：
“Attention 数学目标基本不变，
通过 IO-aware implementation 降低 GPU memory traffic。”
```

这种理解方式更适合面试和系统设计。
