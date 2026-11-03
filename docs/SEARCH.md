# Search scope and evidence record

Curated on 2026-11-03 (Asia/Shanghai). This is a targeted literature update, not a systematic review with an exhaustive search universe or a PRISMA screening count.

## Search strategy

The search combined foundational method-name searches with recent-year and venue queries. Actual query families included:

- `LLM "time series forecasting" 2026`
- `"time series forecasting" "large language models" 2025 survey`
- `LLM "time series forecasting" 2026 site:arxiv.org/abs`
- `LLM "time series forecasting" 2026 site:proceedings.mlr.press`
- `LLM forecasting 2026 site:aclanthology.org`
- `"Large Language Models for Time Series" Survey arxiv`
- `"LLM-driven" "Time Series Forecasting" survey 2026`
- `LLM4Series forecasting library 2026`
- `"LLM-driven" "time series forecasting" October 2026 arxiv`
- Method-name searches for PromptCast, GPT4TS, LLMTime, Time-LLM, TEST, TEMPO, UniTime, LLM4TS, S²IP-LLM, CALF, AutoTimes, Time-LlaMA, GPT4MTS, TimeCMA, ChatTime, Time-VLM, TimeRAG, TokenCast, TimeCopilot, TimeSeriesScientist, and recent context/agent papers.
- Topic combinations of forecasting with text, context, news, events, retrieval, VLMs, reasoning, and agents, followed by exact-title searches and primary-source verification.

Search engines and secondary paper lists were discovery aids. Retained evidence uses the paper, publisher, arXiv, PMLR, ACL Anthology, OpenReview, author project pages, or author-linked repositories. Some AAAI, IEEE, Elsevier, and OpenReview pages returned access or bot-check errors; in those cases the search-indexed primary-source text, openly available paper, author source, or publisher-deposited metadata was used where available. Access failures are not evidence that a paper or code does not exist.

## Inclusion and organization

The core requires numerical time-series forecasting and an explicit pretrained language-model, vision-language-model, or LLM-agent role. The snapshot retains 56 distinct records: 41 methods, 3 dataset/benchmark papers, 4 evaluation papers, 6 surveys/positions, and 2 toolkits.

Earlier pretrained language models are retained for historical continuity. Numerical-only foundation models are adjacent baselines. Pure event classification, anomaly detection, time-series question answering, and general event-outcome forecasting are outside the method tables.

Categories express the primary role, not mutually exclusive technical ingredients. Textualized statistics from the same numerical history are not treated as independent external information. Thus TimeCMA, TimeSAF, and TimeMRA appear under adaptation; numerical-neighbour retrieval in the selected TimeRAG appears under prompting/retrieval. LLM trajectory search and prompt evolution appear under agents/reasoning/refinement. TSFLab appears under research tooling.

The same DOI or base arXiv ID identifies a single entry across preprint and formal versions. Exact-title matches are checked manually. TimeCMA was discovered independently in two research streams and retained once. RTS-LLM was investigated but omitted from this chronology because its first full-paper public date was unresolved; its 2026 volume and 2025 acceptance/DOI creation dates alone do not settle that question. Augur was omitted from the main method tables after checking the primary PDF's task definitions: its four main evaluated targets are classifications, with F1 and AUROC metrics; a supplementary numerical forecasting ablation is noted below.

## Important metadata decisions

- [PromptCast](https://arxiv.org/abs/2210.08964): first public in 2022, journal online in 2023, TKDE volume in 2024. These dates are different bibliographic events.
- [LLM4TS](https://doi.org/10.1145/3719207): 2023 preprint and ACM TIST 2025 publication are one paper lineage.
- [Time-LlaMA](https://aclanthology.org/2025.acl-srw.90/): the final publisher title and five-author list are used. The venue is the ACL 2025 Student Research Workshop, not the main track.
- [CALF](https://github.com/Hank0626/CALF): the former `Hank0626/LLaTA` repository redirects to CALF; no second method entry is created.
- [TokenCast](https://ijcai.org/proceedings/2026/338): IJCAI 2026 publisher metadata takes precedence over an inconsistent AAAI citation in the author repository. First arXiv release is 2025.
- [TimeRAG](https://arxiv.org/abs/2412.16643): the Yang et al. ICASSP 2025 paper is distinct from the similarly named OpenReview submission *TimeRAG: It's Time for Retrieval-Augmented Generation in Time-Series Forecasting*. Their metadata and code must not be mixed.
- [Time-VLM](https://proceedings.mlr.press/v267/zhong25a.html): the repository linked by the publisher is `CityMind-Lab/ICML25-TimeVLM`.
- [ExoTimer](https://ojs.aaai.org/index.php/AAAI/article/view/39908): no code link was inferred from search snippets mixing its title with another method.
- [Nexus](https://arxiv.org/abs/2605.14389): the October 2026 revision's title and description supersede the older title.
- [CastFlow](https://arxiv.org/abs/2604.27840): a journal template label in a manuscript does not establish acceptance. Listed as an arXiv preprint.
- [MemCast](https://proceedings.mlr.press/v306/tao26a.html): the paper's older repository URL redirects to `ustc-time-series/MemCast`; the canonical destination is used.
- [CTRL](https://aclanthology.org/2026.findings-acl.1104/): the paper explicitly links `mfriendly/CTRL`, but the retrieved repository contained only a README. It is labeled a placeholder.
- [SCALER](https://arxiv.org/abs/2608.08675): KDD 2026 is explicitly author-reported in the arXiv record and official repository; the label retains that evidence qualification.
- [LLM4Series](https://github.com/llm4time/llm4series): labeled as the ICLR 2026 TSALM Workshop, author-reported, rather than ICLR main conference.

## Excluded tasks and unselected related resources

[TimeCAP](https://arxiv.org/abs/2502.11418) centrally studies time-series event prediction and reports F1 in its abstract; it is adjacent to this numerical-forecasting list. [Augur](https://aclanthology.org/2026.acl-long.32.pdf) defines its main classification targets in §5.1: a power threshold, severe pollution, traffic-direction classes, and financial-direction classes. Its text consists of dataset and variable descriptions. Appendix D.1.1 / Table 7 also reports a numerical forecasting ablation with MSE and MAE. It is omitted from this snapshot's main methods because the principal task is categorical prediction; this is not a claim that the paper contains no numerical forecasting experiment.

[Aurora](https://arxiv.org/abs/2509.22295) is an additional multimodal forecasting resource not selected into this snapshot. The checked version uses language/vision encoders with a numerical forecasting backbone and GPT-4-assisted corpus creation. Any future entry should describe those roles precisely; the present omission is not a claim that it has no language-model component.

## Structured metadata and limitations

[`data/papers.json`](../data/papers.json) preserves exact titles, authors, earliest located public years, publication status, arXiv/DOI identifiers when verified, paper and repository links, method summaries, source URLs, and record-specific caveats. Missing code and citation-count fields remain null with reasons. Some author lists or titles follow the final publisher version rather than the initial preprint.

`fetched_at` records this curation date. `year` is the earliest public paper year located in the checked sources, not a claim that no earlier release exists. No citation counts were collected. PDF download was not requested and file-format validation was not performed. Source availability, repository reachability, implementation completeness, experimental reproducibility, and scientific validity are separate questions.

The evidence includes abstracts, selected method sections, publisher metadata, and repository contents; it is not a full-text review of every paper. Published numerical gains were not independently reproduced. Newer manuscripts and repositories can change after this snapshot.
