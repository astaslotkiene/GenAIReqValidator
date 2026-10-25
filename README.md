# GenAIReqValidator: data and results

Data and result files for the article "A formal decision model for requirements compliance validation with Graph RAG-based LLMs: an industrial case study" (A. Slotkienė, M. Čenys). They allow every number, table and figure of the article to be recomputed. The files were taken from the repository of the validation tool, commit 3e5a12c of 10 May 2026.

## Contents

| Path | Content |
|---|---|
| `data/reqs_full.json` | The 31 requirements (REQ-1 to REQ-31) |
| `expert_scores/expert1_scores.json` | Scores of the first expert, the gold standard ("expert scores" in the article) |
| `expert_scores/expert2_scores.json` | Scores of the second expert. "Intermediate" on semantic compliance is counted as failed in the article |
| `results/results_*.json` | One result file per configuration (34 files) |

Each expert file gives, for every requirement, the scores for content, semantic and data compliance (Pass, Intermediate, Fail).

Each result file contains:
- `experiment` and `config`: the name and parameters of the configuration;
- `Setup Time (s)`, `Evaluation Time (s)`, `graph_metrics`, `gold_standard`;
- `results`: one record per requirement, criterion and run (31 x 3 x 2 = 186), with the compliance assessment (`Assessment`), the LLM output with its reasons (`Evaluation`), the retrieved context (`Context`), the RAG metrics (`Faithfulness`, `Context Relevance`, `Answer Relevance`, `Retrieval Quality`, `Similarity Score`) and the evaluation time per requirement.

Notes: the field "Node Degree" stores E/V, half of the node degree 2E/V of Eq. (17) in the article. Where a configuration reused an existing graph, the stored setup time is close to zero, and the article reports setup times only for configurations that built their own graph.

## Result files and configurations of the article

| File (`results_*.json`) | Configuration |
|---|---|
| baseline | B0 (chunk size 1,000, overlap 200, soft limit 800, 14 concepts, top-k 5, search depth 1, tree-of-thoughts) |
| chunk_300 ... chunk_900 | Chunk size 300 to 900 |
| overlap_100, overlap_150 | Overlap 100, 150 |
| nac_600, nac_1000 | Soft limit 600, 1,000 |
| synonyms_expanded | Expanded concept dictionary (26 concepts) |
| rso_true | Single-occurrence entity removal |
| param_value_extraction | Parameter-value extraction |
| depth_2, depth_3, depth_4 | Search depth 2, 3, 4 |
| topk_3, topk_4, topk_6, topk_7 | top-k 3, 4, 6, 7 |
| style_zero_shot, style_few_shot, style_chain_of_thought, style_cot_few_shot | Zero-shot, few-shot, chain-of-thought, CoT few-shot prompting |
| depth3_chunk700, depth3_topk6, depth3_zero_shot, depth3_pvextract | Search depth 3 combined with chunk size 700, top-k 6, zero-shot prompting, parameter-value extraction |
| combined_optimal, combined_optimal_few_shot, combined_optimal_zero_shot | C1 with tree-of-thoughts, few-shot, zero-shot prompting |
| depth3_chunk700_topk6_zero_shot | C2 |

The decision rules of the prompts and the analysis scripts are provided with the supplementary material of the article (S1 and S6). The source code of the validation tool is available from the authors on reasonable request.

## Licence
[authors: add terms of use for the data]
