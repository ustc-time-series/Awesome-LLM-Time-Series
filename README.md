# Awesome LLM Time Series

A curated collection of research on LLM-driven time-series forecasting (TSF), including pretrained language-model adaptation, contextual forecasting, vision-language models, and forecasting agents.

Last curated: 2026-11-03. This snapshot contains 56 distinct papers and resources: 41 forecasting methods and 15 datasets, evaluations, surveys, positions, and toolkits. Coverage is selective, with foundational work from 2022 onward and an emphasis on 2025–2026 developments.

[中文调研笔记](docs/research-notes.zh-CN.md) · [Structured metadata](data/papers.json) · [Search scope and evidence](docs/SEARCH.md) · [Contributing](CONTRIBUTING.md)

## Scope

The main method tables require both a numerical forecasting objective and an explicit role for a language-pretrained model, a vision-language model, or an LLM agent. Earlier pretrained LMs such as GPT-2 and text-to-text models are retained to show the development of the field.

Numerical time-series foundation models such as Chronos, TimesFM, Moirai, Timer, and Time-MoE are adjacent baselines; they enter this list when a paper explicitly combines them with an LLM. Sharing a Transformer architecture or a model name does not establish language pretraining. Classification, anomaly detection, temporal question answering, and event-outcome prediction are outside the main forecasting scope.

Each paper appears once under its primary role; categories can overlap. `Year` is the earliest public paper year located in the cited sources, while `Venue / status` describes the verified publication record. A preprint year can precede the conference year. Author-reported venues are labeled. `—` means no verified author-linked repository was recorded, not that no code exists. Repository links can contain code, data, or literature collections and do not establish reproducibility.

## Start here

1. Problem map: [IJCAI 2024 survey](https://ijcai.org/proceedings/2024/921) and [TSF-focused systematic review](https://doi.org/10.1016/j.knosys.2026.115938).
2. Numerical continuation: [LLMTime](https://arxiv.org/abs/2310.07820); trained adaptation: [Time-LLM](https://arxiv.org/abs/2310.01728) and [AutoTimes](https://arxiv.org/abs/2402.02370).
3. Contextual forecasting: [Context is Key](https://proceedings.mlr.press/v267/williams25a.html), [Time-MMD](https://proceedings.neurips.cc/paper_files/paper/2024/hash/8e7768122f3eeec6d77cd2b424b72413-Abstract-Datasets_and_Benchmarks_Track.html), and [TokenCast](https://ijcai.org/proceedings/2026/338).
4. Agent workflows: [TimeCopilot](https://arxiv.org/abs/2509.00616), [CastFlow](https://arxiv.org/abs/2604.27840), and [KairosAgent](https://aclanthology.org/2026.emnlp-main.1343/).
5. Read the evidence together: [2024 ablation study](https://proceedings.neurips.cc/paper_files/paper/2024/hash/6ed5bf446f59e2c6646d23058c86424b-Abstract-Conference.html), [2026 large-scale study](https://arxiv.org/abs/2602.14744), and [MUSE-Bench](https://arxiv.org/abs/2609.15087). Their protocols differ and do not support a universal ranking of LLM-based forecasting.

## Contents

- [Direct prompting and numerical retrieval](#direct-prompting-and-numerical-retrieval) (4)
- [Alignment, reprogramming and fine-tuning](#alignment-reprogramming-and-fine-tuning) (17)
- [External text, events and covariates](#external-text-events-and-covariates) (5)
- [Multimodal and vision-language forecasting](#multimodal-and-vision-language-forecasting) (2)
- [Agents, reasoning and iterative refinement](#agents-reasoning-and-iterative-refinement) (13)
- [Datasets and contextual forecasting benchmarks](#datasets-and-contextual-forecasting-benchmarks) (3)
- [Critical evaluation and decision benchmarks](#critical-evaluation-and-decision-benchmarks) (4)
- [Surveys and position papers](#surveys-and-position-papers) (6)
- [Toolkits and research automation](#toolkits-and-research-automation) (2)
- [Evaluation questions](#evaluation-questions)

## Direct prompting and numerical retrieval

Observations or retrieved historical examples enter a language model as serialized inputs. Training requirements differ: PromptCast adapts text-generation models, whereas LLMTime and NLTS use unchanged language models.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2025 | [Enhancing Zero-Shot Time Series Forecasting in Off-the-Shelf LLMs via Noise Injection Prompting](https://aclanthology.org/2026.findings-acl.2054/) | Adds noise to numerical histories before digit tokenization as an inference-time augmentation for unmodified language-model forecasters, including tests on post-pretraining data. | [Findings of ACL 2026](https://aclanthology.org/2026.findings-acl.2054/) | [Repository](https://github.com/jkumh/NLTS) |
| 2024 | [TimeRAG: Boosting LLM Time Series Forecasting via Retrieval-Augmented Generation](https://ieeexplore.ieee.org/document/10889933) | Retrieves historically similar sequences using dynamic time warping and inserts the retrieved examples into prompts for an LLM-based time-series forecaster. | [ICASSP 2025](https://ieeexplore.ieee.org/abstract/document/10889933/metrics) | — |
| 2023 | [Large Language Models Are Zero-Shot Time Series Forecasters](https://arxiv.org/abs/2310.07820) | Serializes scaled observations into digit strings and uses an unchanged autoregressive language model to produce probabilistic numerical continuations. | [NeurIPS 2023](https://proceedings.neurips.cc/paper_files/paper/2023/file/3eb7ca52e8207697361b2c0fb3926511-Paper-Conference.pdf) | [Repository](https://github.com/ngruver/llmtime) |
| 2022 | [PromptCast: A New Prompt-Based Learning Paradigm for Time Series Forecasting](https://arxiv.org/abs/2210.08964) | Expresses numerical forecasting inputs and targets as natural-language sentences and adapts pretrained text generation models to the resulting sentence-to-sentence task. | [IEEE TKDE 2024 (online publication December 2023)](https://ieeexplore.ieee.org/abstract/document/10356715) | [Repository](https://github.com/cruiseresearchgroup/PISA-PromptCast) |

## Alignment, reprogramming and fine-tuning

Pretrained language representations are connected to numerical forecasting through trainable embeddings, adapters, prompts, or prediction heads. Textual descriptions derived from a series are distinguished from independently available external context.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [IMRouter: Imbalance-aware Temporal Pattern Routing for LLM-based Time Series Forecasting](https://arxiv.org/abs/2610.39246) | Uses pattern-adaptive expert routing and routing-guided semantic alignment to address imbalanced temporal patterns. | [arXiv preprint](https://arxiv.org/abs/2610.39246) | — |
| 2026 | [LagLLM: LLM-empowered lead–lag dependency learning for spatial-temporal time series forecasting](https://proceedings.mlr.press/v306/wu26ci.html) | Builds a lead–lag graph using spatial information, learned dynamics and frozen-LLM reasoning, then sorts tokens structurally for a fine-tuned language-model forecaster. | [ICML 2026](https://proceedings.mlr.press/v306/wu26ci.html) | [Repository](https://github.com/w2obin/LagLLM-2026) |
| 2026 | [M3Time: LLM-Enhanced Multi-Modal, Multi-Scale, and Multi-Frequency Multivariate Time Series Forecasting](https://ojs.aaai.org/index.php/AAAI/article/view/39383) | Combines multi-scale and multi-frequency numerical representations with language-model semantic priors, using an adaptive mixture of L1 and L2 losses for forecasting. | [AAAI 2026](https://ojs.aaai.org/index.php/AAAI/article/view/39383) | — |
| 2026 | [TF-LLM: Enhanced time series analysis with time-frequency large language models](https://doi.org/10.1016/j.neunet.2026.108687) | Integrates local time-domain and periodic frequency-domain features with pretrained language models and contextual prompts for forecasting and other time-series tasks. | [Neural Networks 2026](https://www.sciencedirect.com/science/article/pii/S0893608026001498) | — |
| 2026 | [TimeMRA: LLM-Empowered Time Series Forecasting via Multi-Scale Retrieval-Augmented Representations](https://proceedings.mlr.press/v306/shang26b.html) | Creates multiscale LLM prompt embeddings, disentangles and routes relevant scales, and retrieves cross-modal representations to improve forecasts. | [ICML 2026](https://proceedings.mlr.press/v306/shang26b.html) | [Repository](https://github.com/shangzongjiang/TimeMRA) |
| 2026 | [TimeSAF: Towards LLM-Guided Semantic Asynchronous Fusion for Time Series Forecasting](https://aclanthology.org/2026.acl-long.1208/) | Separates numerical and prompt feature learning, then asynchronously returns aggregated high-level LLM semantics to the numerical forecasting backbone. | [ACL 2026](https://aclanthology.org/2026.acl-long.1208/) | — |
| 2025 | [Time-LlaMA: Adapting Large Language Models for Time Series Modeling via Dynamic Low-rank Adaptation](https://aclanthology.org/2025.acl-srw.90/) | Aligns numerical channel tokens with text prompts and uses an input-dependent selection of low-rank adaptation modules within the pretrained language-model backbone. | [ACL 2025 Student Research Workshop](https://aclanthology.org/2025.acl-srw.90/) | — |
| 2024 | [AutoTimes: Autoregressive Time Series Forecasters via Large Language Models](https://arxiv.org/abs/2402.02370) | Maps time-series segments into a frozen decoder-only language-model embedding space and preserves autoregressive next-segment generation, with timestamp embeddings and in-context forecasting. | [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/file/dcf88cbc8d01ce7309b83d0ebaeb9d29-Paper-Conference.pdf) | [Repository](https://github.com/thuml/AutoTimes) |
| 2024 | [CALF: Aligning LLMs for Time Series Forecasting via Cross-modal Fine-Tuning](https://arxiv.org/abs/2403.07300) | Fine-tunes temporal and text-aligned branches using input matching, intermediate-feature regularization and output consistency to reduce the language–time-series distribution gap. | [AAAI 2025](https://ojs.aaai.org/index.php/AAAI/article/download/34082/36237) | [Repository](https://github.com/Hank0626/CALF) |
| 2024 | [S²IP-LLM: Semantic Space Informed Prompt Learning with LLM for Time Series Forecasting](https://proceedings.mlr.press/v235/pan24c.html) | Aligns embeddings of decomposed time-series patches with semantic anchors from pretrained word embeddings and retrieves relevant anchors as forecasting prompts. | [ICML 2024](https://proceedings.mlr.press/v235/pan24c.html) | [Repository](https://github.com/panzijie825/S2IP-LLM) |
| 2024 | [TimeCMA: Towards LLM-Empowered Multivariate Time Series Forecasting via Cross-Modality Alignment](https://arxiv.org/abs/2406.01638) | Aligns a numerical time-series branch with frozen-LLM prompt embeddings and caches last-token language features to reduce downstream forecasting cost. | [AAAI 2025](https://ojs.aaai.org/index.php/AAAI/article/download/34067/36222) | [Repository](https://github.com/ChenxiLiu-HNU/TimeCMA) |
| 2023 | [One Fits All: Power General Time Series Analysis by Pretrained LM](https://arxiv.org/abs/2302.11939) | Adapts pretrained GPT-2 representations for numerical time-series tasks using trainable input/output components while freezing self-attention and feed-forward blocks. | [NeurIPS 2023](https://papers.nips.cc/paper/2023/file/86c17de05579cde52025f9984e6e2ebb-Paper-Conference.pdf) | [Repository](https://github.com/DAMO-DI-ML/NeurIPS2023-One-Fits-All) |
| 2023 | [LLM4TS: Aligning Pre-Trained LLMs as Data-Efficient Time-Series Forecasters](https://arxiv.org/abs/2308.08469) | Uses a time-series alignment stage followed by forecasting fine-tuning, with two-level aggregation to incorporate multi-scale temporal information into a pretrained language model. | [ACM TIST 2025](https://doi.org/10.1145/3719207) | [Repository](https://github.com/blacksnail789521/LLM4TS) |
| 2023 | [TEMPO: Prompt-based Generative Pre-trained Transformer for Time Series Forecasting](https://arxiv.org/abs/2310.04948) | Adapts a pretrained language-model backbone using trend/seasonal/residual decomposition and component-specific prompts to support cross-domain forecasting. | [ICLR 2024](https://openreview.net/pdf?id=YH5w12OUuU) | [Repository](https://github.com/DC-research/TEMPO) |
| 2023 | [TEST: Text Prototype Aligned Embedding to Activate LLM's Ability for Time Series](https://arxiv.org/abs/2308.08241) | Learns time-series embeddings with instance, feature and text-prototype contrastive objectives, then applies soft prompts and frozen language models to forecasting and other tasks. | [ICLR 2024](https://proceedings.iclr.cc/paper_files/paper/2024/hash/a4352e2c9d93582898a2a20e1f514e8f-Abstract-Conference.html) | [Repository](https://github.com/SCXsunchenxi/TEST) |
| 2023 | [Time-LLM: Time Series Forecasting by Reprogramming Large Language Models](https://arxiv.org/abs/2310.01728) | Maps numerical patches onto learned text-prototype embeddings and combines them with descriptive prefix prompts before a frozen language-model backbone. | [ICLR 2024](https://proceedings.iclr.cc/paper_files/paper/2024/file/680b2a8135b9c71278a09cafb605869e-Paper-Conference.pdf) | [Repository](https://github.com/KimMeen/Time-LLM) |
| 2023 | [UniTime: A Language-Empowered Unified Model for Cross-Domain Time Series Forecasting](https://arxiv.org/abs/2310.09751) | Combines domain instructions, channel-independent time-series tokens and a language–time-series Transformer to train one forecaster across heterogeneous domains. | [The ACM Web Conference (WWW) 2024](https://doi.org/10.1145/3589334.3645434) | [Repository](https://github.com/liuxu77/UniTime) |

## External text, events and covariates

The method explicitly uses external text, events, or exogenous covariates. These inputs require a prediction-time availability boundary.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [ExoTimer: Leveraging Large Language Models for Time Series Forecasting with Exogenous Variables](https://ojs.aaai.org/index.php/AAAI/article/view/39908) | Combines an exogenous-aware numerical encoder, multi-attribute LLM prompts, and lightweight hash-space alignment to forecast endogenous variables using external covariates. | [AAAI 2026](https://ojs.aaai.org/index.php/AAAI/article/view/39908) | — |
| 2026 | [Unlocking the Value of Text: Event-Driven Reasoning and Multi-Level Alignment for Time Series Forecasting](https://arxiv.org/abs/2603.15452) | Uses historical examples to guide LLM event reasoning and combines text-time-series representation alignment with frequency-level fusion of event-driven and numerical forecasts. | [ICLR 2026](https://openreview.net/pdf/8542bcdfb88a3841aedc557da9e8d5acc406672c.pdf) | [Repository](https://github.com/decisionintelligence/VoT) |
| 2025 | [From Values to Tokens: An LLM-Driven Framework for Context-Aware Time Series Forecasting via Symbolic Discretization](https://ijcai.org/proceedings/2026/338) | Tokenizes continuous series into discrete symbols, aligns temporal and textual tokens in an LLM representation space, and generates future tokens that decode into numerical forecasts. | [IJCAI 2026](https://ijcai.org/proceedings/2026/338) | [Repository](https://github.com/ustc-time-series/TokenCast) |
| 2024 | [GPT4MTS: Prompt-based Large Language Model for Multimodal Time-series Forecasting](https://ojs.aaai.org/index.php/AAAI/article/view/30383) | Combines numerical patches and text-derived soft prompts in a pretrained GPT-2 forecasting framework, supported by an LLM-assisted pipeline for collecting and summarizing GDELT news. | [AAAI 2024](https://ojs.aaai.org/index.php/AAAI/citationstylelanguage/get/chicago-author-date?publicationId=28667&submissionId=30383) | [Repository](https://github.com/Flora-jia-jfr/GPT4MTS-Prompt-based-Large-Language-Model-for-Multimodal-Time-series-Forecasting) |
| 2024 | [From News to Forecast: Integrating Event Analysis in LLM-Based Time Series Forecasting with Reflection](https://proceedings.neurips.cc/paper_files/paper/2024/hash/6aef8bffb372096ee73d98da30119f89-Abstract-Conference.html) | Uses LLM agents and iterative reflection to filter news and align relevant events with time-series behavior before fine-tuning an LLM to forecast numeric sequences. | [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/hash/6aef8bffb372096ee73d98da30119f89-Abstract-Conference.html) | [Repository](https://github.com/daydreamer-amelia/From_News_to_Forecast) |

## Multimodal and vision-language forecasting

These methods align numerical sequences with text or visual representations. Series-derived images and descriptions need not add external information.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2025 | [Time-VLM: Exploring Multimodal Vision-Language Models for Augmented Time Series Forecasting](https://proceedings.mlr.press/v267/zhong25a.html) | Fuses temporal memory-bank features with series-derived images and textual descriptions encoded by frozen vision-language models for forecasting. | [ICML 2025](https://proceedings.mlr.press/v267/zhong25a.html) | [Repository](https://github.com/CityMind-Lab/ICML25-TimeVLM) |
| 2024 | [ChatTime: A Unified Multimodal Time Series Foundation Model Bridging Numerical and Textual Data](https://arxiv.org/abs/2412.11376) | Expands a pretrained LLM vocabulary with discretized numerical tokens and applies continued pretraining and instruction tuning for zero-shot and context-guided forecasting. | [AAAI 2025](https://ojs.aaai.org/index.php/AAAI/article/view/33384) | [Repository](https://github.com/ForestsKing/ChatTime) |

## Agents, reasoning and iterative refinement

This section includes tool orchestration, reasoning, memory, search, and iterative forecast refinement. A refinement loop alone does not imply an open-ended tool-using agent.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [CastFlow: Bridging Evidence Acquisition and Accurate Prediction in Agentic Time Series Forecasting](https://arxiv.org/abs/2604.27840) | Experience-guided tool planning gathers multi-view evidence, then a specialized LLM refines an ensemble forecast prior after supervised and verifiable-reward training. | arXiv preprint | [Repository](https://github.com/Forever-Pan/CastFlow) |
| 2026 | [CastFSR: A Fast--Slow--Reflect Agentic Reasoning Framework for Context-Aware Time Series Forecasting](https://arxiv.org/abs/2608.03031) | A fast forecasting prior is combined with slow contextual-evidence reasoning and reflective revision, supporting both off-the-shelf LLM inference and compact-model distillation. | arXiv preprint | [Repository](https://github.com/Xiaoyu-Tao/CastFSR) |
| 2026 | [ChronoScribe: Semantic-Numerical Specialization for Instruction-Driven Time Series Forecasting](https://arxiv.org/abs/2610.16345) | Separates instruction interpretation and forecast configuration in an LLM from numerical quantile forecasting in a frozen time-series foundation model. | [arXiv preprint](https://arxiv.org/abs/2610.16345) | — |
| 2026 | [CTRL: Control-Based Time Series Forecasting with LLM-Guided Residual Learning](https://aclanthology.org/2026.findings-acl.1104/) | Specialized LLM controllers analyze decomposed forecast errors and emit compact control signals that a residual decoder turns into corrections to a frozen forecasting backbone. | [Findings of ACL 2026](https://aclanthology.org/2026.findings-acl.1104/) | [Placeholder](https://github.com/mfriendly/CTRL) |
| 2026 | [KairosAgent: Agentic Time Series Forecasting with Fused Semantic Reasoning](https://aclanthology.org/2026.emnlp-main.1343/) | A tool-using LLM reasoner supplies semantic future-morphology guidance to a time-series foundation model, with forecasting-reward reinforcement learning and turn-level credit assignment. | [EMNLP 2026 main conference](https://aclanthology.org/2026.emnlp-main.1343/) | — |
| 2026 | [LLM as Forecasting Planner: Training-Free Text Conditioning for Time-Series Foundation Models](https://arxiv.org/abs/2607.24892) | Uses an LLM as policy and value judge in Monte Carlo tree search over frozen TSFM-generated trajectories to satisfy natural-language forecasting context. | arXiv preprint | — |
| 2026 | [MemCast: Memory-Driven Time Series Forecasting with Experience-Conditioned Reasoning](https://proceedings.mlr.press/v306/tao26a.html) | A hierarchical memory of patterns, reasoning trajectories and general laws guides forecast generation, trajectory selection and reflective refinement. | [ICML 2026 (PMLR 306)](https://proceedings.mlr.press/v306/tao26a.html) | [Repository](https://github.com/ustc-time-series/MemCast) |
| 2026 | [Nexus: An Agentic Framework for Context-Aware Time Series Forecasting](https://arxiv.org/abs/2605.14389) | Temporal profiling constructs a numerical anchor, macro and micro reasoning produce contextual trajectories, and covariance-weighted Bayesian synthesis reconciles their forecasts. | arXiv preprint | — |
| 2026 | [Training-Free Continual Learning for Multimodal Forecasting via Prompt Evolution](https://arxiv.org/abs/2610.27468) | Evolves a textual guidance block through outcome-based reflection and uses it to steer a frozen LLM forecaster on recent series paired with retrieved news. | arXiv preprint | — |
| 2026 | [Efficient Test-Time Scaling for LLM-based Time Series Forecasting](https://arxiv.org/abs/2608.08675) | A lightweight forecaster predicts coarse future shape and a frozen LLM performs fixed-step coarse-to-fine residual token refinement with a shorter token sequence. | [KDD 2026 (author-reported)](https://arxiv.org/abs/2608.08675) | [Repository](https://github.com/xuanmay2701/SCALER) |
| 2025 | [FLAIRR-TS - Forecasting LLM-Agents with Iterative Refinement and Retrieval for Time Series](https://aclanthology.org/2025.findings-emnlp.834/) | A forecaster agent and refiner agent adapt prompts at inference time using prior forecasts and retrieved analogues to produce numerical forecasts without intermediate code generation. | [Findings of EMNLP 2025](https://aclanthology.org/2025.findings-emnlp.834/) | — |
| 2025 | [TimeCopilot](https://arxiv.org/abs/2509.00616) | An LLM agent orchestrates feature analysis, forecasting-model selection, cross-validation and ensembling through a unified forecasting toolkit. | arXiv preprint | [Repository](https://github.com/TimeCopilot/timecopilot) |
| 2025 | [TimeSeriesScientist: A General-Purpose AI Agent for Time Series Analysis](https://arxiv.org/abs/2510.01538) | Four specialized agents curate data, plan the model search, fit and validate forecasting configurations, and report the resulting workflow. | arXiv preprint | [Repository](https://github.com/Y-Research-SBU/TimeSeriesScientist) |

## Datasets and contextual forecasting benchmarks

Data resources and evaluation tasks are listed separately from forecasting methods. Context construction and temporal availability differ across benchmarks.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [Beyond Numerical Time Series: A Unified Benchmark for Multimodal Forecasting with Heterogeneous Context](https://arxiv.org/abs/2609.15087) | Compares numerical, multimodal, and LLM forecasters under shared windows and context ablations across heterogeneous contextual datasets. | [arXiv preprint](https://arxiv.org/abs/2609.15087) | — |
| 2024 | [Context is Key: A Benchmark for Forecasting with Essential Textual Information](https://proceedings.mlr.press/v267/williams25a.html) | Tests forecasts on tasks whose solutions require textual background, constraints, or event information, alongside a direct LLM prompting baseline. | [ICML 2025](https://proceedings.mlr.press/v267/williams25a.html) | [Repository](https://github.com/ServiceNow/context-is-key-forecasting) |
| 2024 | [Time-MMD: Multi-Domain Multimodal Dataset for Time Series Analysis](https://proceedings.neurips.cc/paper_files/paper/2024/hash/8e7768122f3eeec6d77cd2b424b72413-Abstract-Datasets_and_Benchmarks_Track.html) | Provides aligned numerical series and textual information across nine domains with the MM-TSFlib library for evaluating multimodal forecasting. | [NeurIPS 2024 Datasets and Benchmarks Track](https://proceedings.neurips.cc/paper_files/paper/2024/hash/8e7768122f3eeec6d77cd2b424b72413-Abstract-Datasets_and_Benchmarks_Track.html) | [Repository](https://github.com/AdityaLab/Time-MMD) |

## Critical evaluation and decision benchmarks

Read contrasting evidence with its dataset, scale, information, metric, and compute boundaries. Decision utility and VLM preference judgments complement numerical forecast error.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [Forecast Workflow Bench: Evaluating Language-Model Decisions with Budgeted Forecast Tools](https://arxiv.org/abs/2609.27385) | A benchmark evaluates how language-model agents purchase forecasting tools, select histories and horizons, and choose capacities under an explicit decision-loss and cost objective. | arXiv preprint | [Repository](https://github.com/Neurogica/forecast-workflow-bench) |
| 2026 | [Rethinking the Role of LLMs in Time Series Forecasting](https://arxiv.org/abs/2602.14744) | A large-scale study of language-pretrained forecasting across eight billion observations and 17 scenarios contrasts alignment, architecture and pretraining under in-domain and cross-domain tests. | arXiv preprint | [Repository](https://github.com/EIT-NLP/LLM4TSF) |
| 2026 | [TimeVista: Exploring and Exploiting Vision-Language Models as Judges for Time Series Forecasting](https://arxiv.org/abs/2606.16173) | Studies VLM judgments of plotted forecasts against human preferences; complements numerical error metrics. | [arXiv preprint](https://arxiv.org/abs/2606.16173) | — |
| 2024 | [Are Language Models Actually Useful for Time Series Forecasting?](https://proceedings.neurips.cc/paper_files/paper/2024/hash/6ed5bf446f59e2c6646d23058c86424b-Abstract-Conference.html) | Controlled ablations remove or replace the LLM in three popular forecasting architectures and test whether language pretraining improves accuracy, few-shot behavior or computational efficiency. | [NeurIPS 2024 main conference](https://proceedings.neurips.cc/paper_files/paper/2024/hash/6ed5bf446f59e2c6646d23058c86424b-Abstract-Conference.html) | [Repository](https://github.com/BennyTMT/LLMsForTimeSeries) |

## Surveys and position papers

Several surveys cover broader time-series tasks; use their forecasting-specific sections. Position papers describe research agendas rather than independently validated methods.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [Position: Beyond Model-Centric Prediction -- Agentic Time Series Forecasting](https://arxiv.org/abs/2602.01776) | A forecasting-focused position defines perception, planning, action, reflection and memory, and contrasts workflow, reinforcement-learning and hybrid agentic designs. | arXiv position paper (2026) | — |
| 2026 | [LLM Agents for Time-Series: A Survey](https://aclanthology.org/2026.findings-emnlp.367/) | A problem-driven taxonomy maps time-series agents across forecasting and reasoning, augmentation, anomaly diagnosis and decision support, comparing tools, memory and workflows. | [Findings of EMNLP 2026](https://aclanthology.org/2026.findings-emnlp.367/) | — |
| 2026 | [Leveraging Large Language Models for time series forecasting: A systematic literature review](https://doi.org/10.1016/j.knosys.2026.115938) | Reviews LLM-based numerical forecasting with an emphasis on adaptation choices, datasets, and evaluation practices. | [Knowledge-Based Systems 343 (2026), 115938](https://www.sciencedirect.com/science/article/pii/S0950705126006647) | — |
| 2025 | [A Survey of Reasoning and Agentic Systems in Time Series with Large Language Models](https://openreview.net/forum?id=l3QW42g6u3) | A taxonomy crosses direct, chain and branching reasoning structures with task objectives and tags for tool use, memory, multimodality and adaptation. | [TMLR 2026](https://jmlr.org/tmlr/papers/) | [Repository](https://github.com/blacksnail789521/Time-Series-Reasoning-Survey) |
| 2024 | [Empowering Time Series Analysis with Large Language Models: A Survey](https://ijcai.org/proceedings/2024/895) | Organizes LLM-based time-series pipelines by querying, tokenization, prompts, fine-tuning, and model integration. | [IJCAI 2024, Survey Track](https://ijcai.org/proceedings/2024/895) | — |
| 2024 | [Large Language Models for Time Series: A Survey](https://ijcai.org/proceedings/2024/921) | Surveys prompting, quantization, alignment, visual bridging, and tool integration across time-series tasks. | [IJCAI 2024, Survey Track](https://ijcai.org/proceedings/2024/921) | — |

## Toolkits and research automation

LLM4Series supports forecasting experiments. TSFLab automates research around forecasting models and is adjacent tooling rather than an inference-time forecasting algorithm.

| Year | Paper | LLM role / resource | Venue / status | Repository |
|---|---|---|---|---|
| 2026 | [LLM4Series: Structured Prompting for Time Series Forecasting with LLMs](https://openreview.net/forum?id=6fbcYFRoUL) | Provides modular serialization, structured prompts, LLM interfaces, and forecast evaluation utilities. | [ICLR 2026 TSALM Workshop (author-reported)](https://github.com/llm4time/llm4series) | [Repository](https://github.com/llm4time/llm4series) |
| 2026 | [TSFLab: A Self-Improving Agent-Agnostic Workbench for Time Series Forecasting Research](https://arxiv.org/abs/2610.40901) | A shared workbench supplies coding agents with resources and tools for forecast-model reproduction, benchmarking, maintenance and pilot method development. | arXiv preprint | [Repository](https://github.com/D2I-Group/TSFLab) |

## Evaluation questions

- What does the LLM contribute: numerical generation, learned representations, genuinely new external information, tool selection, or forecast correction?
- Does an ablation preserve the encoder, forecasting head, training data, and tuning budget when removing or replacing language pretraining?
- Were text, covariates, memory entries, retrieved neighbours, and agent feedback available at the forecast origin? Were normalization and retrieval indices fitted without future leakage?
- Are zero-shot transfer, few-shot training, in-context examples, and frozen-backbone adaptation reported separately?
- Do comparisons match splits, horizons, frequencies, context windows, metrics, training data, and inference/search budgets? Are strong numerical models included?
- Are forecast error, probabilistic calibration, decision utility, latency, token cost, tool calls, training cost, and repeated-run variance reported where relevant?

This list records published descriptions and public artifacts. It does not independently reproduce reported gains. See the [Chinese research notes](docs/research-notes.zh-CN.md) for a synthesis and the [search record](docs/SEARCH.md) for evidence limits and metadata corrections.
