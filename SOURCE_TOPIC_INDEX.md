# Sanitized curriculum topic index

1. AI大模型应用开发实战训练营
2. 模块
3. 课程名称
4. 课程核心内容
5. 模块1: AI大模型基础
6. 理论知识
7. 从提示工程到RAG：构建大模型的知识与交互基础
8. 1. Prompt Engineering 与 Context Engineering  - 提示工程基础 - 高级提示技巧 - 上下文工程（CE）的核心 - 长上下文管理2. RAG与私有知识库的构建与作用 - RAG的核心价值 - 私有知识库构建三部曲 - 向量数据库（Vector DB） - RAG的工作流
9. Agent：从可控性到自主反思
10. 1. Agent如何控制幻觉、提升任务可控性 - Agent幻觉的成因：识别模型知识边界与推理链条的断裂 - 提升可控性1- 利用RAG或工具（Tool-use）进行事实校验 - 提升可控性2- 利用Function Calling和JSON模式约束Agent的行为与输出 - 提升可控性3- 设计 Human-in-the-Loop 的审批与干预节点2. 使用思维链构建有自主反思能力的Agent - 思维链（CoT）的原理 - 自主反思（Self-Reflection）的实现 - 案例框架（ReAct） - 自我修正：设计批评家或评估提示来引导Agent自我校准
11. 多模态前沿：从Agent构建到视频AIGC
12. 1. 多模态Agent的构建要点 - 多模态大模型（MLLM）的能力基座：理解GPT5、Gemini等模型的图文理解能力 - 核心构建点1：将视觉感知封装为Agent可以调用的工具（Tool） - 核心构建点：处理多模态输入（如图片、音频）的统一表征与分发 - 多模态Agent的应用：从看图说话到复杂的视觉问答与操作（VQA） 2. 视频检索及视频生成的技术方案 - 视频检索（Video Retrieval）：基于关键帧、音频（ASR）与时序的多模态向量化检索 - 视频理解（Video Understanding）：利用大模型进行场景分割、目标追踪与内容摘要 - 视频生成（Video Generation）：文生视频（T2V）模型（如Sora, Kling）的扩散模型原理 - 当前挑战与机遇：视频生成的时序一致性、逻辑性、物理规律与算力瓶颈
13. 实操基础
14. AI大模型基本原理及API使用
15. 1. AI大模型基本原理 - 分析式AI与生成式AI - 从GPT-1到GPT-5 - LLM是如何训练的 - Temperature与Top P 的作用 - AI Chat产品的超能力2. 大模型API使用 - 系统提示词 与 用户提示词 - LLM的输入与输出Token限制 - CASE-情感分析-Qwen（掌握DashScope调用大模型） - CASE-天气Function-Qwen（了解Function Call） - CASE-表格提取-Qwen（了解多模态大模型） - CASE-运维事件处置-Qwen
16. 1
17. AI编程-从入门到精通
18. 1. Cursor编程 - 什么是Cursor Rules - Cursor的主要功能2. Cursor编程实战 - CASE：多张Excel报表处理 - CASE：疫情实时监控大屏3. Trae与CodeBuddy使用 - Trae使用 - CodeBuddy使用 - CASE：多张Excel报表处理
19. 模块2：Agent
20. 理论知识+案例详解+实操
21. Function Calling与MCP
22. 1. 使用Function Calling进行工具调用 - 什么是Function Calling？ - Function Calling 与 MCP的区别 - 使用Qwen3完成天气调用 Function Calling - Qwen-Agent中的 Function Calling - 使用Function Calling完成数据库查询2. MCP与A2A的应用 - MCP 的核心概念 (MCP Host，MCP Client，MCP Server） - MCP 的使用场景 - CASE：旅游攻略MCP - CASE：Fetch网页内容抓取 - CASE：Bing中文搜索 - CASE：搭建你的MCP服务  - 什么是Agent2Agent - A2A与MCP的关系
23. Agent的自主规划与工具开发
24. 1. 给Agent赋予思考规划反思能力 - Agent设计范式 - 反应式（Reactive） - 深思熟虑式（Deliberative） - 混合式（Hybrid） - 实现思考链（CoT）与ReAct2. Agent自主编写代码开发工具 - 工具调用（Tool Use）基础 - 赋予Agent一个code_interpreter（代码解释器）工具 - 构建Text-to-SQL Copilot
25. Agent的能力优化与效果评估
26. 1. 使用用户使用数据提升Agent能力 - 显式反馈 - 隐式反馈 - 利用反馈进行RAG或微调2. Agent智能体效果评估 - RAG能力评估（大海捞针） - 多跳推理评估（Multi-Hop） - 业务指标评估
27. 项目实战
28. OpenManus开发实战
29. 1. 深度解析 OpenManus 框架 - OpenManus 项目导论 - 核心流程：一次“手稿生成”的完整生命周期 - 核心模块 Orchestrator - 核心模块 Agents  - 核心模块 Memory - 核心模块 Tools - 核心机制 提示词工程2. 构建自己的 AI写作助手 - 本地运行 OpenManus - Agents 的“角色”定制 - 集成企业知识库RAG - 中文写作流
30. Harness Engineering
31. 1. 编排层、记忆层、执行层、反馈层 - 记忆层 (Memory Layer)：赋予AI“持久化大脑” - 执行层 (Execution Layer)：从“能说”到“能做”的飞跃 - 编排层 (Orchestration Layer)：让AI学会“规划与协作” - 反馈层 (Feedback Layer)：建立“自动化”的纠错闭环2. OpenClaw、Hermes、Claude Code 的核心 memory 机制 - 记录全部聊天历史的SQLite数据库 - 记录每日事项的memory/YYYY-MM-DD.md的文件机制 - 四层颗粒度3. 代码执行时涉及到的环境及工具 - 工具集的设计原则 - 执行环境的构建4. 沙箱、文件系统、权限 - 文件系统隔离：Git Worktree的妙用 - 沙箱隔离的四层防护 - 权限系统的精细化设计
32. 搭建Hermes Agent 中的长期记忆和自进化能力
33. 1. 心跳唤醒时，自主收集需要整理的记忆 - 自我唤醒的心跳机制代码实战 - 自适应的心跳频率调整机制代码实现 - 记忆价值评估算法2. 整理成4层颗粒度记忆文字 - Tier2 -> Tier1 -> Tier0 的逐级自动总结摘要 - Tier2 -> Tier3 的自动相关性扩展3. Embedding 保存到 LanceDB - 存储数据的格式设计 - LanceDB实战部署 - 混合检索策略4. 用户新任务唤醒记忆 - 意图识别与记忆路由 - 上下文动态构建 - 实战演示
34. 实现Hermes中的多Agent协作、主Agent调度
35. 1. 主 Agent 核心能力 —— 意图拆解、任务分发、权限管控 - 意图理解：识别任务类型 - 任务拆解：复杂大任务拆分为原子子任务 - 智能分发：轻任务本地串行、重任务抛给后台执行单元 - 上下文分发规则：最小闭环上下文2. 子 Agent 分工、注册与执行机制 - 子 Agent 的标准结构 - 子 Agent 注册机制 - 子 Agent 执行流程3. Agent 间通信 + 任务流闭环 - Hermes 通信机制 - 任务依赖与执行顺序 - 结果聚合逻辑 - 异常处理4. 全局闭环系统 —— 结果回收、状态同步、自进化基础底座 - 状态持久化设计：任务轨迹、执行日志、对话记录结构化存储，支撑后续复盘 - 自进化前置底座：任务执行轨迹 → 事后复盘 → 自动提炼流程 → 生成个性化技能
36. 专项求职辅导
37. Agent相关简历+面试问题辅导
38. 一分钟讲清楚Agent的定义你如何处理Agent的幻觉问题？在你的项目中，Agent的‘状态’是如何管理的？你如何平衡Agent的自主性与可控性？介绍一下你最复杂的那个Agent项目如何回答“RAG的效果如何评估？”为什么用LangGraph如何处理Text-to-SQL如何搭建一个RAG Agent，实现对本地知识库（如PDF）的问答如何定义一个自定义工具处理多文件时 ，如何解决上下文长度限制问题如何评估检索效果如何收集用户使用数据Agent设计哲学
39. 模块3: 模型部署及高并发
40. 企业级AI部署：从硬件选型到框架选择
41. 1. 企业级 AI 硬件的选型，规划与优化 - GPU 选型策略：对比 H100, A100, L40S, 4090 等主流GPU - CPU 与内存配比：分析 CPU 对 Tokenization 预处理、请求调度的影响，以及内存大小如何限制并发处理能力。 - 网络基础设施：探讨 RoCE (RDMA) vs. TCP/IP 在多节点/多卡（如张量并行）推理中的延迟和带宽瓶颈。 - 服务器与集群规划2. 部署框架 Ollama, vLLM, SGLang 的特点 - Ollama：易用性、本地化部署优势 - vLLM：高吞吐推理引擎的核心优势（PagedAttention） - SGLang：在复杂控制流（如 RAG、CoT、Agents）任务中的高性能特性，及其与 vLLM 的差异。 - 选型对比
42. AI服务核心：高并发原理与性能监控调优
43. 1. 高并发的AI服务原理（KV Cache，vLLM 及 PagedAttention 原理） - KV Cache 瓶颈 - PagedAttention 核心思想 - vLLM 的实现 - Continuous Batching (连续批处理) - vLLM 如何利用 PagedAttention 实现请求的动态插入和退出，极大提升 GPU 利用率2. AI 服务的性能监测及调优 - 关键性能指标 - 监控工具栈 - vLLM 性能调优 - 瓶颈定位：分析和识别推理服务中的常见瓶颈
44. SGLang 深度优化：Radix 缓存与复杂任务的极致吞吐
45. 1. SGLang 的缓存优化及 Radix Tree 原理及运行时高级抽象 - Radix Tree (基数树) 原理 - SGLang 的 RadixAttention - 运行时高级抽象 (Frontend/Backend) - SGLang IR (中间表示)2. SGLang 对于复杂AI任务中的极致延迟及吞吐优化 - Token Healing 技术 - 复杂控制流优化 - 多租户与智能调度 - SGLang 与 vLLM 在执行中的差异
46. 短剧视频逐帧换脸的显卡资源分配及排队系统
47. 1. 换脸流程 - 视频拆帧，逐帧换脸，脸部检测识别，脸部对齐，换脸，帧组装视频 - 换脸任务管理:  - 任务提交，任务等待，任务处理2.换脸任务及算力分配 - 通过 rocketmq 进行功能解耦 - 算力消费端队列长度控制 - 换脸消息的生命周期与超时重试 - 片段，全剧，控制命令，人脸预处理的任务解耦 - 原始视频缓存（节省流量）3.脸部预处理 - 换脸常见问题 - 上传非正面人脸，牙齿为黑色，额头出现多余的头发 - 预处理方式（1）人脸识别检测（2）人物闭嘴（3）人物光头化
48. 模块4: 开发框架
49. LangChain：多任务应用开发
50. 1. LangChain多任务应用开发 - Models, Prompts, Memory, Indexes, Chains, Agents - LangChain中的tools (serpapi, llm-math) - LangChain中的Memory - LECL构建任务链2. LangChain开发实操详解 - CASE：动手搭建本地知识智能客服（理解ReAct） - CASE：工具链组合设计 （LangChain Agent） - CASE：搭建故障诊断Agent（LangChain Agent） - CASE：工具链组合设计 （LCEL）
51. AI框架设计与选型
52. 1. 自研框架设计思路 - 核心组件抽象：如何设计模块化、插件化与可扩展的框架结构 - 数据流与控制流：定义Agent、Tools与Models的标准化交互管线 - 状态管理与性能考量：异步处理、缓存机制与日志监控的设计2. 优秀开源开发框架详解 - LlamaIndex深度解析 - AutoGen多智能体框架 - 框架选型对比：LangChain vs. LlamaIndex vs. AutoGen的适用场景与优劣
53. HuggingFace生态实战：从模型应用到高效微调
54. 1. HuggingFace模型库的使用 - 核心组件（Transformers, Datasets, Tokenizers） - Pipelines API：零代码/少代码调用模型的快捷方式 - Model Hub与Dataset Hub：模型与数据集的搜索、下载与版本控制2. 使用HuggingFace做模型微调 - Trainer API：标准化的模型训练与评估高阶接口 - PEFT高效微调：LoRA与QLoRA的原理与代码实战 - TRLx：使用强化学习（RLHF/PPO）对齐语言模型
55. 神经网络基础与Tensorflow实战
56. 1. 神经网络基础 - 神经网络结构 - 激活函数 - 损失函数 - 反向传播 - 梯度下降 - 优化方法（SGD、Adam） - 使用numpy搭建神经网络2. TensorFlow实战 - TensorFlow中的计算图与会话管理 - 分布式训练与模型并行 - TensorFlow Serving部署与推理 - 使用Keras构建简单神经网络 - 使用Keras进行二手车价格预测
57. Pytorch与视觉检测
58. 1. PyTorch的核心概念 - PyTorch的张量与自动求导机制 - PyTorch的动态图与静态图2. PyTorch的分布式训练 - 在多个GPU上进行训练 - 使用PyTorch Lightning简化模型训练3. 图像识别技术与缺陷检测 - 传统图像识别模型 - 视觉检测方法 - 缺陷检测方案 - 卷积网络可视化4. 视觉检测模型 YOLO - 从Yolov1到Yolov12 - ultralytics：基于pytorch的视觉检测工具 - Project：钢铁表面缺陷检测
59. 开发框架相关简历+面试问题辅导
60. LangChain解决了什么问题？ LangChain 六大核心组件的职责与交互关系是什么 如何使用LangChain构建一个RAG系统 LangChain中的Memory机制是如何实现的？ LangChain vs. LlamaIndex：二者的核心定位有何不同？ 什么时候应该选择LangChain，什么时候应该选择LlamaIndex？ 如何看待AutoGen等多智能体框架？它与单Agent框架的核心区别是什么？ 如果让你从零设计一个LLM应用框架，你会如何进行组件抽象？ 如何设计一个可插拔的Tool/Plugin系统？ HuggingFace Pipelines API的优势和局限性是什么？ Tokenizers 的作用是什么？为什么模型和Tokenizer必须匹配？ 什么是全参数微调（Full Fine-Tuning）？它有什么缺点？ 什么是PEFT（高效微调）？ PyTorch的动态图机制（Eager Execution）是什么？它与静态图有何区别？ TensorFlow 2.x的Keras API与TF 1.x的Session/Graph模式有何不同？ 在LLM时代，你如何看待TensorFlow和PyTorch这两个框架的优劣和生态？
61. 模块5: 模型训练与微调
62. LLM微调原理
63. 1. LLM的微调原理 - 高效微调的方法 - LoRA的数学原理 - LoRA算法的核心假设 - 矩阵分解与猜你喜欢 - SVD矩阵分解2. LLM微调的数据处理与显存评估方法 - 微调数据准备 - 数据质量与数量要求 - 不同模型尺寸与场景的数据需求 - 硬件需求与显存计算 - 微调显存估算方法 - LoRA显存优化与计算示例 - 微调后的模型评估
64. 高质量微调数据工程与评估
65. 1. 微调数据的收集、清洗、标准 - 数据收集策略 - 数据清洗核心流程 - 数据标注规范 - SFT vs. RLHF 的数据差异2. 衡量数据质量和微调结果的关系 - Garbage In, Garbage Out - 自动化评估指标 - 基准测试（Benchmark）评估 - 人工评估的必要性
66. LLM模型蒸馏与微调实操
67. 1. LLM的模型蒸馏 - 知识蒸馏的核心思想 - 蒸馏的目的与价值 - 经典蒸馏方法 - LLM时代的蒸馏挑战2. LLM模型微调与蒸馏实操 - unsloth框架使用功 - 教师-学生模型的选择 - 任务蒸馏演练 - 评估蒸馏效果
68. 视觉与多模态模型
69. 1. 多模态模型与视觉识别模型 - 视觉识别（CV）的三大核心任务 - VLM在行业中的应用 - 视频理解SOTA - 智能文档模型 MinerU2. 训练Yolo目标检测模型 - YOLO（You Only Look Once）的核心原理 - 目标检测数据集的准备与标注 - 训练自定义YOLO模型 - 评估模型性能指标
70. AI质检
71. - AI在工业质检的价值 - 技术选型对决：YOLO vs. Qwen-VL - 数据集分析 (EDA)：缺陷类别、图像特点、标注格式。 - 环境准备：Python, PyTorch, Ultralytics (YOLO), Transformers (Qwen-VL) - 数据工程：从原始数据到YOLO训练集 - YOLO 训练与调优 - 模型评估与缺陷分析 - Qwen-VL多模态大模型的探索性测试 - 使用 Qwen-VL 进行“零样本”缺陷检测 - 结果分析与局限性探讨 - YOLO 与 Qwen-VL 的终极对决
72. 模型训练与微调相关简历+面试问题辅导
73. 谈谈你对预训练和微调的理解什么是全参数微调为什么需要PEFT请详细讲讲 LoRA 的原理如果要你微调一个模型，你的技术选型是什么？你的微调数据是怎么来的？是开源的、业务的、还是合成的？你认为一条‘高质量’的微调数据应该符合什么标准？SFT（指令微调）的数据格式是怎么构建的？你如何评估你微调后的模型效果？自动化评估 (如BLEU, ROUGE) 和人工评估，你倾向用哪个？你知道有哪些评估LLM的Benchmark吗？为什么要用模型蒸馏？它的核心思想是什么？你如何评估蒸馏的效果？什么是多模态模型？CV的经典三大任务（分类、检测、分割）和多模态VQA（视觉问答）有什么不同？YOLO的数据集是怎么标注和准备的？对于一个工业质检任务，你认为用 YOLO 和用 Qwen-VL，它们各自的优缺点是什么？
74. 模块6: RAG
75. Embeddings和向量数据库
76. 1. Embeddings模型及向量化 - 什么是Embedding - Word Embedding - 余弦相似度计算 - Embedding模型的选择 - MTEB榜单 - 向量维度对模型性能的影响 - 神奇的“俄罗斯套娃” - 如何选择适合的Embedding模型2. 向量数据库和向量检索 -  什么是向量数据库 - FAISS, Elasticsearch, Milvus, Pinecone的特点 - 向量数据库与传统数据库的区别 - 如何将数据导入向量数据库 - Embedding与原数据导入Faiss - 不同向量数据库的功能与性能比较
77. RAG技术与应用
78. 1. RAG检索增强生成的原理及流程 - 大模型开发的三种范式 - 什么是RAG技术？它如何增强大模型的生成能力 - RAG的核心原理与流程 - NativeRAG - CASE：DeepSeek +Faiss搭建本地知识库检索2. Query改写与知识库处理 - Query改写 - Query联网搜索 - 知识库处理 - 场景1：知识库问题生成与检索优化 - 场景2：对话知识沉淀 - 场景3：知识库健康度检查 - 场景4：知识库版本管理与性能比较 - 如何提升RAG质量
79. RAG多模态数据处理
80. 1. 多模态数据处理：PDF、Word、网页等图文数据 - PDF 文档解析：挑战与策略 - Word文档解析 - 网页数据解析 - Qwen-Agent中的RAG2. 多模态数据处理：图片、视频等多媒体数据 - 图像数据的多重表征 - 视频数据处理流程 - 语音转文本ASR - GraphRAG使用 - 全局搜索 - 局部搜索
81. RAG调优
82. 1. 混合检索的适用场景及具体方法 - 为什么需要混合检索 - 常见的混合检索方法 - 关键词（BM25）+ 向量检索（Embedding） - 多路召回（分别检索） - 引入重排序（Rerank）提升最终质量2. RAG系统的调试步骤及效果评估 - 数据准备 - 检索阶段 - 生成阶段 - RAG 效果评估：如何量化好与坏 - 持续优化的评估实践
83. 企业知识库（企业RAG大赛冠军项目）
84. 1. 企业RAG大赛：搭建RAG知识库 - RAG冠军方案（多路由+动态知识库） - RAG比赛任务说明 - 基础RAG系统流程 - 解析模块、Docling优化、表格序列化 - 内容提取（ingestion） - 检索（Retrieval） - LLM 重排序 (LLM reranking) - 父页面检索 - 整合后的检索器 - 增强 (Augmentation) - 生成 (Generation) - 思维链、结构化输出、思维链+结构化输出 - 指令细化 (Instruction Refinement) - 提示词创建、Prompt.py 实现 - RAG系统调参2. 搭建自己的RAG系统 - 选择适合的LLM和Embedding模型  - MinerU使用 - 更新中文知识库、设置相关的问题清单 - 针对开放式的问题，进行Prompt设置 - 搭建前端页面，比如使用 streamlit
85. 部分场景中可以取代RAG的技术
86. 1. Long-Context LLM - “上下文即知识”的回归 - 实战场景：全量知识注入 - 成本与性能的权衡2. Agentic Search - RAG的终结：从“Just-In-Time”到“Just-In-Case” - 核心工作流：思考-行动-观察循环 - 实战架构：ReAct与Plan-and-Solve3. LLM Wiki - RAG的致命缺陷 - LLM Wiki范式 - 自进化机制
87. LLM Wiki
88. 1. 结构化、统一口径、双向链接、去重的 Wiki 文档 - 统一口径与结构化 - 双向链接与知识图谱 - 智能去重与冲突解决2. 三层架构：Raw → Wiki → Schema - Raw 层（原始数据湖） - Wiki 层（编译输出层） - Schema 层（控制协议）3. 增量更新、持久化存储 - 增量更新机制 - 基于 Git 的版本控制 - 从 RAG 到“编译器模式”4. 知识库索引体系 - 总目录、主题索引、标签索引的设计逻辑 - 轻量化检索思路：关键词检索 + 目录路由，弱化向量
89. RAG相关简历+面试问题辅导
90. 你能谈谈大模型应用开发的三种主要模式吗？文档分块有哪些策略？你为什么选择用这个策略？你能画一下 RAG 的系统架构图吗？并解释一下关键步骤。文档分块有哪些策略？你为什么选择用这个策略？你项目中用了哪个 Embedding 模型？为什么选它？如果你的 RAG 效果很差，你会从哪几个方面去调试？当用户的问题很模糊，或者依赖上一轮对话时，RAG 怎么优化？你只用了向量检索吗？它有什么缺点？什么是混合检索？检索召回了 20 条文档，你怎么确保喂给 LLM 的是最好的 3 条？系统上线后，你怎么维护和迭代你的知识库？你如何评估一个 RAG 系统的好坏？
91. 模块7: AI Coding 带来的范式变革
92. 大厂优秀工程师使用AI Coding 的最新方法与经验
93. 1.用确定性驾驭概率性 - 告别“感觉式编程” - “Spec Coding”三铁律 - 渐进式复杂度管理2.构建你的AI流水线 - L3 AI Coding的到来 - 多智能体协作模式 - 实战案例：自动化CI/CD流水线3.构建团队的“知识飞轮” - 构建Rules+Spec+Skills三位一体体系 - 知识飞轮 - 解决“代码考古”难题4.构建“审查-优化”闭环，把风险关在上线前 - AI的自我审查与优化 - 人的最终决策权 - 从“超级个体”到“超级团队”
94. 大型软件项目的AI开发与AI重构
95. 1.从“代码实现者”到“系统架构师”的思维跃迁 - 演进式设计 - 上下文工程 - AI作为“活文档”与“知识导航”2.AI重构战略 - 重构前的战略框架 - AI辅助的“暴力拆解”与“精准缝合” - 渐进式现代化：桑树模式的AI实践3.构建“生成-验证-修正”的质量飞轮 - AI的自我反思与对抗性测试 - 人的最终决策权 - 从“超级个体”到“超级团队”的工程文化
96. AI Coding 中的团队重新分工与新协作模式
97. 1.从“职能专家”到“AI指挥官” - Spec架构师 - AI训练师 - 质量验证师2.流程重构 - Spec与Issue的协同 - 构建团队的“生产性资本” - 人机协同的“精准制导”3.组织进化 - 分形化团队组织架构 - 新角色的核心职责与技能要求4.文化重塑 - 建立AI辅助的团队学习文化 - 建立AI辅助的团队学习文化
98. 在华为昇腾‌显卡上部署DeepSeek V4 模型 并连通本地Claude Code
99. 1.DeepSeek V4 深度解析与性能基准 - V4架构揭秘 - 版本选型策略 - 能力边界测试2.华为昇腾（Ascend）生态与CANN架构详解 - 国产算力底座 - CANN软件栈入门 - 环境准备3.实战演练——在昇腾NPU上部署DeepSeek V4 - 模型适配与量化 - 推理服务化 - API兼容性配置4.Claude Code本地化集成与Agent工作流打通 - 本地环境搭建 - 无缝连接配置 - Agent能力实测
