# Contributing

Contributions that improve coverage, metadata, or reproducibility are welcome.

## Scope

The main list focuses on numerical time-series forecasting in which a pretrained language model, a vision-language model, or an LLM agent has an explicit role. Surveys, forecasting benchmarks, datasets, and research toolkits are listed separately.

Methods trained only on numerical time series can be useful baselines, but sharing a Transformer architecture, tokenizer, or a name with an LLM is not sufficient for inclusion in the main method tables. Classification, anomaly detection, temporal question answering, and event forecasting belong in adjacent resources unless a numerical forecasting experiment is present.

## Adding or correcting a record

1. Provide the exact title and a primary paper link: publisher proceedings, journal, arXiv, or OpenReview.
2. State the first public year separately from the conference or journal year. Preserve the arXiv identifier when the title changes.
3. Describe what the language model does in one original sentence. State the forecasting task and any important scope boundary.
4. Use an author-linked repository for the code link. Distinguish code, data, project pages, and empty placeholders. A working link does not establish reproducibility.
5. Cite a source for the publication status. An OpenReview submission is not evidence of acceptance; workshops must be labeled as workshops. Prefer publisher metadata when it conflicts with a repository citation.
6. Check for an existing entry using DOI and arXiv ID before adding a record. Keep one entry for a preprint and its published version.

Update both `README.md` and `data/papers.json`. If the work is relevant to the research discussion, update `docs/research-notes.zh-CN.md` as well. Record the source-check date and keep unknown fields as `null`; do not substitute guesses or zero citation counts.

## Performance claims

Describe mechanisms and evaluation settings rather than copying a paper's claim of being the first or the best. Cross-paper performance comparisons require matching datasets, splits, horizons, metrics, training data, and compute budgets. Make all quantitative claims traceable to their original tables or released results.
