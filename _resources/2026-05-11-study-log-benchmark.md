---
title: "大模型常用benchmark汇总"
collection: resources
type: "Resource"
permalink: /resources/benchmark
date: 2026-05-11
---
今天在看各个国内大模型的开源报告，发现里面涉及了很多benchmark的内容，特别来做一期介绍博客。

![项目截图](image\2026-05-11\try.png "hello world")

### **一、传统 Benchmark**

Benchmark 是用于评估模型性能的标准数据集或任务集合，通常包含多个任务或数据集，用于全面测试模型的能力。

### 1. **语言模型 Benchmark**

* **GLUE (General Language Understanding Evaluation)**

  * **目标** ：评估模型在自然语言理解（NLU）任务上的表现。
  * **任务** ：包括文本分类、语义相似度、自然语言推理等（如 CoLA、SST-2、MRPC、QQP 等）。
  * **适用模型** ：BERT、RoBERTa、GPT 等语言模型。

  CoLA：

  * 全称 ：The Corpus of Linguistic Acceptability (CoLA)。
  * 类型 ：单句分类数据集，用于二分类任务（判断句子是否符合英语语法）。
  * 数据来源 ：该语料库中的句子摘自语言理论方面的书籍和期刊，涵盖了多种句法现象。
  * 标注方式 ：每个句子都由语言学家标注为“符合语法”（grammatical）或“不符合语法”（ungrammatical）。
  * 数据量 ：包含数万条英语句子。 [[1](https://blog.csdn.net/qq_43525676/article/details/125358377), [2](https://cloud.tencent.com/developer/article/2464100)]
* SST-2：

  * **用途：（Stanford Sentiment Treebank，斯坦福情感树库）** 用于文本分类任务，具体是二元情感分类（Positive 或 Negative），即判断一句话是正面情感还是负面情感。
  * **来源：** 源自电影评论，包含了人们对电影的真实评价和人类标注的情感标签。
  * **地位：** 是 GLUE（General Language Understanding Evaluation）基准测试** 中的核心任务之一，常用于衡量预训练模型（如 BERT, RoBERTa）的情感分析能力。** [[1](https://opendatalab.com/OpenDataLab/SST/download), [2](https://www.tensorflow.org/lite/models/modify/model_maker/text_classification?hl=zh-cn), [3](https://blog.csdn.net/qq_33583069/article/details/115734097), [4](https://zhuanlan.zhihu.com/p/135283598)]
  * **二分类：** 与 SST-1（5分类：极负、负、中、正、极正）不同，SST-2 将中间情绪去除，只保留了正面和负面两类。
  * **规模：** 训练集通常包含约 67,000 条左右的样本，用于训练模型；测试集有数百条用于模型评估。
  * **特点：** 每个句子都经过了短语级的标注，涵盖了从非常负面到非常正面的不同程度评价。 [[1](https://zhuanlan.zhihu.com/p/129838073), [2](https://opendatalab.com/OpenDataLab/SST/download), [3](https://www.tensorflow.org/lite/models/modify/model_maker/text_classification?hl=zh-cn)]
* MRPC：

  * 内容： 它包含 5,801 对从在线新闻源中自动抽取并经过人工标注的英文句子。
  * 任务目标： 判定一对句子在语义上是否属于 “同义改写” (Paraphrase) ，即判断两句话是否表达了相同的含义。
  * 标注方式： 是一个二分类任务（标注为：相同/不相同）。 [[1](https://zhuanlan.zhihu.com/p/135283598), [2](https://edu.51cto.com/article/note/34553.html), [3](https://opendatalab.com/OpenDataLab/MRPC), [4](https://adg.csdn.net/697087c7437a6b40336a9150.html)]
  * 语义相似度计算： 用于评估模型区分两句话是语义重复还是仅文字相似的能力。
  * GLUE 基准测试： MRPC 是著名的 GLUE（通用语言理解评估）基准测试中的核心任务之一，用于衡量BERT等预训练语言模型的句子理解能力。
* QQP：

  * **全称** **：Quora Question Pairs**
  * **来源** **：该数据集由著名问答社区平台 ****Quora** 发布。
  * **任务类型** **：句子对二分类任务（Binary Classification）。**
  * **目标** **：输入两个问题（句子），模型需要判断它们在语义上是否表示同一种意思（即“等效”或“不等效”）。** [[1](https://docs.feishu.cn/v/wiki/A8NvwyXKki0Wgok8lnbcI883nLb/a5), [2](https://www.atyun.com/datasets/info/glue.html)]
* **SuperGLUE**

  * **目标** ：GLUE 的升级版，任务更具挑战性。
  * **任务** ：包括 BoolQ、CB、COPA 等更复杂的 NLU 任务。
* BoolQ:（Boolean Questions）是一个专门用于评估机器阅读理解能力的自然语言处理数据集，由Google研究院发布

  * 任务类型 ：阅读理解、二元分类问答。
  * 答案形式 ：布尔值，即答案仅为“是”（Yes）或“否”（No）。
  * 数据规模 ：包含15,942个样例。每个样例是一个三元组：（问题, 段落, 答案）。
  * 自然产生 ：问题均来源于真实的Google搜索引擎场景，而非人工伪造，反映了人们在实际搜索时的提问方式。
  * 上下文内容 ：问题通常关联一个从维基百科中提取的段落，模型需要根据该段落内容判断问题的对错。 [[1](https://www.volcengine.com/docs/82379/1150781), [2](https://modelscope.cn/datasets/OmniData/BoolQ), [3](https://docs.aws.amazon.com/zh_cn/bedrock/latest/userguide/model-evaluation-prompt-datasets.html), [4](https://www.atyun.com/datasets/info/boolq.html), [5](https://github.com/Ascend/MindSpeed-LLM/blob/master/docs/zh/pytorch/training/evaluation/evaluation_datasets/boolq_evaluation.md)]
* **MMLU (Massive Multitask Language Understanding)**
* 1. **多任务覆盖**：包含57个学科领域，横跨人文社科（哲学、历史）、STEM（数学、物理、计算机）、专业学科（医学、法律）等，任务难度从高中水平延伸至专家级别。
  2. **评估方式**：采用四选一多选题形式，要求模型在无提示（zero-shot）或少量示例（5-shot）的情况下回答问题，直接计算正确率。
  3. **行业地位**：自2020年推出以来，成为LLM技术报告的标配测试集，用于横向对比不同模型的知识广度与推理深度。

  **延伸拓展**：

  * **演进版本**：衍生出MMLU-Pro（10选项干扰项设计）、MMLU-Redux（动态题库）等变体，通过增加选项数量、引入专业领域难题（如抽象代数、量子物理）等方式提升难度，当前顶尖模型在MMLU-Pro上的准确率已接近人类水平（约85%-90%）。
  * **争议与改进**：随着模型性能提升，MMLU的区分度逐渐降低，斯坦福2025年AI指数报告指出其已进入“饱和阶段”，行业开始转向动态更新的“竞技场模式”（如Chatbot Arena）或结合用户反馈的实时评估体系。
  * **应用场景**：除学术评测外，MMLU也被用于验证本地部署模型（如Qwen3.5-9B量化版）的性能，甚至通过认知增强层（如JUZI-RAGnet）实现小模型（4B参数）在MMLU上接近70B大模型的表现。
* **HumanEval**

  * **任务类型**：主要以算法导向的函数级代码片段生成任务为主，每个任务通常要求模型根据问题描述生成一个Python函数，例如实现一个特定的算法或解决一个具体的编程问题。
  * **评估标准**：HumanEval通过测试模型生成的代码是否能够通过预设的测试用例来评估其正确性，通常使用如pass@k（例如pass@1, pass@10）等指标来衡量模型在不同测试用例下的表现。
  * **局限性**：虽然HumanEval在早期被广泛用于评估代码生成模型，但近年来也受到一些批评，认为其任务过于简单，可能无法完全代表真实世界中的复杂编程任务。真实世界的编程任务往往涉及更多的库和函数调用，而HumanEval中的任务可能缺乏这些多样性。此外，模型在HumanEval上的表现也可能受到训练数据污染和过拟合问题的影响，从而影响其对模型泛化能力的评估准确性。
  * **后续发展**：为了解决这些局限性，后续出现了一些改进的基准测试，例如HumanEval+，通过增强测试用例来提高评估的准确性和全面性，以及BigCodeBench等更全面的基准测试工具，以应对更复杂的编程任务和实际应用场景。

### 2. **多模态 Benchmark**

* **[COCO](https://zhida.zhihu.com/search?content_id=252117679&content_type=Article&match_order=1&q=COCO&zhida_source=entity) (Common Objects in Context)**

  * **目标** ：图像描述生成、目标检测等。
  * **任务** ：生成与图像匹配的文字描述。
* **[VQA](https://zhida.zhihu.com/search?content_id=252117679&content_type=Article&match_order=1&q=VQA&zhida_source=entity) (Visual Question Answering)**

  * **目标** ：评估模型对图像和问题的理解能力。
  * **任务** ：根据图像回答问题。
* **CLIP Benchmark**

  * **目标** ：评估图文匹配模型的性能。
  * **任务** ：图像和文本的匹配度。

### 3. **生成模型 Benchmark**

* **[WMT](https://zhida.zhihu.com/search?content_id=252117679&content_type=Article&match_order=1&q=WMT&zhida_source=entity) (Workshop on Machine Translation)**

  * **目标** ：评估机器翻译模型的性能。
  * **任务** ：多种语言对的翻译任务。
* **BIG-bench (Beyond the Imitation Game Benchmark)**

  * **目标** ：评估模型在复杂和多样化任务上的表现。
  * **任务** ：包括 200+ 个任务，涵盖推理、知识、语言生成等。

### 4. **推理和知识 Benchmark**

* **[GSM8K](https://zhida.zhihu.com/search?content_id=252117679&content_type=Article&match_order=1&q=GSM8K&zhida_source=entity)**

  * **目标** ：评估数学推理能力。
  * **任务** ：解决小学数学问题。
* **[StrategyQA](https://zhida.zhihu.com/search?content_id=252117679&content_type=Article&match_order=1&q=StrategyQA&zhida_source=entity)**

  * **目标** ：评估复杂推理能力。
  * **任务** ：回答需要多步推理的问题。

---

### 二、2026最新Benchmark

#### 1. 深度推理与硬核科学 (Reasoning & Science)

| **评测名称**       | **全称 / 定义**                     | **核心考查点**                                                                                                       |
| ------------------------ | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **HLE**            | **Humanity's Last Exam**            | 目前公认最难的通用推理榜单，旨在测试模型是否达到了人类博士级别的认知极限。                                                 |
| **HLE (w/ Tools)** | **HLE (工具增强版)**                | 允许模型在答题时调用 Python 解释器或搜索引擎，考查其“思维+工具”的综合解决能力。                                          |
| **GPQA-Diamond**   | **Graduate-Level Google-Proof Q&A** | 由各领域专家编写的极难科学问题（生物、物理、化学等），普通人即便搜 Google 也很难答对，专门针对大模型的“幻觉”和深度理解。 |

#### 2. 竞赛级数学 (Competitive Mathematics)

| **评测名称**       | **定义**                                          | **难度级别**                                                                                             |
| ------------------------ | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **AIME 2026**      | **American Invitational Mathematics Examination** | 美国数学邀请赛 2026 题库。考查模型在不需要微积分的情况下，处理极高难度组合、数论及几何的能力。                 |
| **HMMT (Nov/Feb)** | **Harvard-MIT Mathematics Tournament**            | 哈佛-麻省理工数学竞赛。分为 11 月（基础）和 2 月（进阶）两个版本，后者难度极高，是评估模型天才逻辑的关键指标。 |
| **IMOAnswerBench** | **International Mathematical Olympiad Bench**     | 国际数学奥林匹克竞赛级别。测试模型解决世界顶级中学生数学竞赛题的能力，通常涉及极其复杂的证明过程。             |

#### 3. 编程与软件工程 (Coding & Software Engineering)

| **评测名称**           | **定义**                                 | **核心考查点**                                                                          |
| ---------------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **SWE-bench Pro**      | **Software Engineering Benchmark (Pro)** | 测试模型修复真实 GitHub Issue 的能力。Pro 版更强调复杂项目的跨文件理解和代码重构。            |
| **NL2Repo**            | **Natural Language to Repository**       | 考查模型根据自然语言需求，直接生成或补全整个代码库（而不是单个函数）的能力。                  |
| **Terminal-Bench 2.0** | **Terminus-2**                           | 终端操作能力测试。模型需要像真实程序员一样在 Linux 命令行中执行指令、调试环境并完成特定任务。 |

#### 4. 智能体与工具使用 (Agentic & Tool Use)

| **评测名称**        | **定义**                         | **核心考查点**                                                                                                    |
| ------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **CyberGym**        | **Cybersecurity Gymnasium**      | 网络安全实战。考查模型在网络攻防、漏洞扫描和逆向工程方面的表现。                                                        |
| **BrowseComp**      | **Browsing Comprehensive**       | 网页导航与信息采集。考查模型在复杂网页中点击、搜索及处理实时网页信息的能力。                                            |
| **τ³-Bench**      | **Tau-Bench**                    | 多步骤任务自动化。模拟用户真实需求（如订机票、查物流），考查模型在多轮对话中调用 API 完成闭环任务的稳定性。             |
| **MCP-Atlas**       | **Model Context Protocol Atlas** | 针对 Anthropic 发布的**MCP 协议**的专项测试，衡量模型与各类工具、服务器连接的兼容性与效率。                       |
| **Tool-Decathlon**  | **工具十项全能**                 | 集合了 10 种不同类型的工具调用场景（天气、日历、数据库等），测试模型的泛化工具使用能力。                                |
| **Vending Bench 2** | **自动零售/商业智能评测**        | 模拟复杂的商业决策场景。表格中的货币符号暗示该榜单考查的是模型在分配资源、预算管理及达成最大经济效益（ROI）方面的表现。 |

---

### **三、常见 Metric**


#### **1. 基础逻辑与硬核推理指标**

| **指标名称**          | **定义**                                                  | **典型适用 Benchmark (2026)**                   |
| --------------------------- | --------------------------------------------------------------- | ----------------------------------------------------- |
| **Accuracy (准确率)** | 模型预测正确的样本占总样本的比例。                              | **HLE** ,**GPQA-Diamond**                 |
| **Exact Match (EM)**  | 模型输出必须与标准答案**字符级完全匹配** 。               | **AIME 2026** , **HMMT** ,**SQuAD** |
| **Pass@k**            | 模型针对同一问题生成**$k$**个答案，只要其中一个正确即算通过。 | **HumanEval** ,**SWE-bench Pro**          |

#### **2. 编程与软件工程指标**

| **指标名称**            | **定义**                                                 | **典型适用 Benchmark (2026)**                    |
| ----------------------------- | -------------------------------------------------------------- | ------------------------------------------------------ |
| **Resolved Rate**       | 在软件工程任务中，模型成功修复的真实 Bug 或 Issue 的比例。     | **SWE-bench Pro**                                |
| **Tool Invocation Acc** | 模型在解决复杂问题时，调用外部工具（如 Python, SQL）的准确性。 | **HLE (w/ Tools)** ,**Terminal-Bench 2.0** |
| **MCP Compliance**      | 符合模型上下文协议 (Model Context Protocol) 的标准化程度。     | **MCP-Atlas**                                    |

#### **3. 智能体 (Agent) 与商业决策指标**

| **指标名称**          | **定义**                                       | **典型适用 Benchmark (2026)**                   |
| --------------------------- | ---------------------------------------------------- | ----------------------------------------------------- |
| **Success Rate (SR)** | 智能体完成整个任务链（如从订票到确认支付）的成功率。 | **τ³-Bench** ,**BrowseComp**            |
| **Profit / ROI**      | 模型在模拟商业环境中的获利能力或投资回报率。         | **Vending Bench 2**                             |
| **Step-wise Cost**    | 完成单位任务所消耗的 Token 成本或时间成本。          | **Vending Bench 2** ,**Agentic Workflow** |

#### **4. 传统语言与生成指标**

| **指标名称**         | **定义**                                                | **典型适用任务**            |
| -------------------------- | ------------------------------------------------------------- | --------------------------------- |
| **F1 Score**         | 精确率 (Precision) 和召回率 (Recall) 的调和平均。             | 关系抽取、QA、MRPC 分类           |
| **BLEU / ROUGE**     | 通过 N-gram 重合度评估生成文本与参考文本的相似度。            | 机器翻译 (BLEU)、文本摘要 (ROUGE) |
| **Perplexity (PPL)** | 困惑度，衡量模型对文本预测的不确定性，值越低越好。            | 语言模型预训练评估                |
| **CIDEr / mAP**      | 专门用于评估图像描述的共识性 (CIDEr) 或目标检测的精度 (mAP)。 | 多模态 (COCO Captions, YOLO)      |
