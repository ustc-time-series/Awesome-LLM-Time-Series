# LLM-driven 时间序列预测调研笔记

检索与核验日期：2026-11-03。本文对应仓库中的 56 条去重记录，其中 41 条为预测方法，15 条为数据集、评估、综述、立场论文和工具。覆盖从 2022 年先行工作到 2026 年 10 月的新近预印本，属于定向调研，不是穷尽性的系统综述。

## 主要判断

从本次选入文献可以观察到，研究正在扩大 LLM 在预测流程中的角色：除了直接输出数值，还包括学习时序表征、解释外部事件、检索历史案例、调用预测工具、搜索候选轨迹以及反思修正。这个趋势是对文献的归纳，不能据此判断某条路线已经普遍优于数值预测模型。

更值得追问的是：语言预训练、外部信息和额外计算分别带来了什么收益？三者常同时变化，仅比较最终误差难以识别机制。建议把下面的技术分类与评估边界一起阅读。

## 技术路线与代表工作

| 路线 | LLM 的实际职责 | 代表工作 | 判断增益时要区分什么 |
|---|---|---|---|
| 数值序列文本化与直接预测 | 将数值编码为文本或 token，生成后续序列 | [PromptCast](https://arxiv.org/abs/2210.08964)、[LLMTime](https://arxiv.org/abs/2310.07820)、[NLTS](https://aclanthology.org/2026.findings-acl.2054/) | 是否训练过、数字表示方式、精度、上下文长度及预训练数据重叠 |
| 预训练语言模型适配 | 通过 patch、原型、prompt、adapter 或 LoRA 连接连续时序与语言表示 | [GPT4TS](https://arxiv.org/abs/2302.11939)、[Time-LLM](https://arxiv.org/abs/2310.01728)、[AutoTimes](https://arxiv.org/abs/2402.02370)、[CALF](https://arxiv.org/abs/2403.07300) | 语言预训练本身与新增编码器、预测头、训练预算的贡献 |
| 外部上下文增强 | 解释新闻、事件或外生变量，并使其影响预测 | [GPT4MTS](https://ojs.aaai.org/index.php/AAAI/article/view/30383)、[From News to Forecast](https://arxiv.org/abs/2409.17515)、[TokenCast](https://ijcai.org/proceedings/2026/338)、[VoT](https://arxiv.org/abs/2603.15452) | 文本是否提供数值历史以外的新信息，以及预测时能否取得这些信息 |
| 多模态表示 | 融合数值、文本或时序图像表示 | [ChatTime](https://arxiv.org/abs/2412.11376)、[Time-VLM](https://proceedings.mlr.press/v267/zhong25a.html) | 从同一序列生成图像或描述，与取得额外观测是不同的信息条件 |
| Agent、推理与反思 | 组织数据处理和工具、规划、记忆、搜索或迭代修正 | [TimeCopilot](https://arxiv.org/abs/2509.00616)、[TimeSeriesScientist](https://arxiv.org/abs/2510.01538)、[CastFlow](https://arxiv.org/abs/2604.27840)、[MemCast](https://proceedings.mlr.press/v306/tao26a.html)、[KairosAgent](https://aclanthology.org/2026.emnlp-main.1343/) | 增益来自规划、检索、基座预测器、集成，还是更多搜索与推理计算 |

这些类别存在交叉。例如，TokenCast 同时涉及离散化和上下文建模；新闻驱动预测也可能使用 Agent。README 按主要职责只收录一次，避免把同一篇预印本与正式版本重复计数。

## 2026 年值得关注的变化

一类工作更明确地划分语义推理与数值计算的职责。[LLM as Forecasting Planner](https://arxiv.org/abs/2607.24892) 让时序基础模型提出数值轨迹，再由 LLM 在搜索中评价其与文本上下文的匹配；[ChronoScribe](https://arxiv.org/abs/2610.16345) 把指令理解和配置交给 LLM，把分位数轨迹交给冻结的时序基础模型；[CTRL](https://aclanthology.org/2026.findings-acl.1104/) 将推理变为控制信号，再通过残差模块修正预测。三者的接口不同，不能简单等同于让 LLM 自由生成未来数值。

另一类工作把记忆、检索和反思纳入预测过程。[MemCast](https://proceedings.mlr.press/v306/tao26a.html) 组织历史模式、推理轨迹和经验，[CastFSR](https://arxiv.org/abs/2608.03031) 结合快速预测先验、慢速上下文推理与反思，[Prompt Evolution](https://arxiv.org/abs/2610.27468) 通过结果反馈更新文本指导。这些方法需要分别说明记忆构建、反馈到达时间和更新成本；“冻结模型参数”仍可能伴随持续变化的外部状态。

计算预算本身也成为研究对象。[SCALER](https://arxiv.org/abs/2608.08675) 研究粗到细的预测修正与推理开销，[Forecast Workflow Bench](https://arxiv.org/abs/2609.27385) 评价显式工具预算下的决策效用。后者的目标包含预测成本与下游决策损失，不能与单纯的 MSE 排名混为一谈。[TSFLab](https://arxiv.org/abs/2610.40901) 则服务于预测研究的自动化，属于研究工具，与推理时预测 Agent 分开列出。

## 如何看待实证争议

[Are Language Models Actually Useful for Time Series Forecasting?](https://arxiv.org/abs/2406.16964) 对三种常用架构做移除或替换 LLM 的消融，质疑所测试设置中语言预训练的必要性。这一结论有具体架构与协议边界，不能直接外推到所有上下文预测或工具调用方法。

[Rethinking the Role of LLMs in Time Series Forecasting](https://arxiv.org/abs/2602.14744) 在作者报告的 80 亿观测、17 种场景和 4 个预测长度下研究规模、对齐及跨域泛化，并报告不同条件下的收益。它扩大了证据范围，但与前述消融的训练规模和评估条件并不相同，不能视作同一实验的直接反转。

更晚的 [MUSE-Bench](https://arxiv.org/abs/2609.15087) 在 14 个数据集、8 个领域、6 类上下文上统一比较多类方法。其所测设置中，数值时序基础模型总体领先，直接通用 LLM 及 LLM 引导修正未表现出稳定优势；上下文错配也会损害预测。这些结果支持“信息与设置决定收益”的判断，同时仍受该基准所选模型和任务范围约束。

[Context is Key](https://proceedings.mlr.press/v267/williams25a.html) 特意构建必须使用文本才能解决的预测任务；[Time-MMD](https://arxiv.org/abs/2406.08627) 提供跨领域数值与文本资源。它们回答的问题与纯数值基准不同。较好的阅读方式是先明确预测对象和信息条件，再比较性能。

## 对后续研究的启发

下面是基于本次调研的研究建议，不代表已经完成实验或得到验证。

1. 把 LLM 的额外贡献拆开验证。比较完整系统、移除语言预训练、移除外部上下文、移除规划或反思等设置，并保持主要模块和训练、搜索预算可比。纯数值模型、数值基础模型和简单集成应作为有竞争力的参照。
2. 将上下文时间边界作为任务定义的一部分。区分预先已知的节假日和约束、预测前已经发布的新闻、预测后才出现的解释；保存检索语料版本及发布时间。记忆和反馈也要采用相同的时间纪律。
3. 研究按需获取证据和按需推理。比较固定流程与自适应流程，在预测误差、决策效用、延迟和总成本之间评价收益，避免只报告增加调用次数后的最优结果。
4. 让解释接受可检验的干预。替换相关或无关文本、打乱时间对齐、改变候选轨迹和工具返回值，检查预测是否按证据变化；流畅的推理文本本身不能证明预测机制可靠。

## 本次整理的证据边界

元数据优先采用出版方、PMLR、ACL Anthology、arXiv 和作者明确关联的仓库。方法说明来自摘要、选读正文和公开项目材料；未逐篇复现实验，也未下载并验证所有 PDF。没有采集引用量，不以星标或引用量推断质量。

正式出版、作者自述、投稿、Workshop 和预印本分别标注。代码链接只表示找到并核验了作者关联的公开入口，不保证实现完整；CTRL 已确认是只有 README 的占位仓库。CastFlow 和 CastFSR 的说明只依据公开资料。完整条目、来源和缺失项见 [papers.json](../data/papers.json)，检索与元数据修正见 [SEARCH.md](SEARCH.md)。
