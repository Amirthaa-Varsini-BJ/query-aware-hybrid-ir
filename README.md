# Query-Aware Adaptive Hybrid Retrieval for Financial IR

> **Paper:** Query-Aware Adaptive Hybrid Retrieval for Financial Information Retrieval: A Systematic Evaluation on the FiQA Benchmark  
> **Authors:** Amirthaa Varsini B J, Ketrolin Sharon K R, Thulasi Shri N A N  
> **Institution:** Department of Information Technology, Thiagarajar College of Engineering, Madurai, India  
> **Submitted to:** Information Retrieval Research Journal (IRRJ) — https://irrj.org

---

## What This Paper Is About

We propose a **Query-Aware Adaptive Hybrid Retrieval** system that improves financial information retrieval by dynamically adjusting fusion weights based on query type. Instead of using fixed equal weights (0.5 BM25 + 0.5 Dense), our system classifies each query and assigns appropriate weights.

| Query Type | Example | BM25 Weight | Dense Weight |
|---|---|---|---|
| Numeric | "401k withdrawal age 59.5" | 0.9 | 0.1 |
| Keyword | "stock buyback" | 0.8 | 0.2 |
| Balanced | "tax implications of retirement" | 0.5 | 0.5 |
| Conceptual | "What are the risks of high-yield bonds?" | 0.2 | 0.8 |

---

## Key Results

Evaluated on the **FiQA dataset** from the BEIR benchmark (57,638 documents, 648 queries):

| System | NDCG@10 | MAP@10 | Recall@100 |
|---|---|---|---|
| BM25 | 0.1591 | 0.1163 | 0.3590 |
| Dense Retrieval | 0.3687 | 0.2914 | 0.7061 |
| Static Hybrid (α=0.5) | 0.2943 | 0.2231 | 0.6633 |
| **Adaptive Hybrid (Ours)** | **0.3395** | **0.2669** | **0.6683** |

**Our adaptive system achieves 15.4% improvement in NDCG@10 over static hybrid fusion.**

---

## Repository Structure

```
query-aware-hybrid-ir/
│
├── notebooks/
│   └── hybrid_model_IR.ipynb          ← Main Colab notebook (all experiments)
│
├── results/
│   ├── all_scores.json                ← Final scores for all 4 systems
│   ├── results_bm25.json              ← BM25 retrieval results
│   ├── results_dense_full.json        ← Dense retrieval results
│   ├── results_static_hybrid.json     ← Static hybrid results
│   ├── results_adaptive_hybrid.json   ← Our adaptive hybrid results
│   ├── query_type_log.json            ← Query type classifications
│   ├── failure_analysis.json          ← Failure analysis data
│   └── ablation_results.json          ← Ablation study results
│
├── figures/
│   ├── architecture.png               ← System architecture diagram
│   ├── chart_comparison.png           ← Performance comparison chart
│   ├── chart_ndcg_comparison.png      ← NDCG@10 comparison chart
│   ├── chart_failure_analysis.png     ← Failure analysis charts
│   └── chart_heatmap.png              ← Success rate heatmap
│
└── README.md                          ← This file
```

---

## How To Run The Experiments

### Step 1 — Open Google Colab

Click the badge below to open the notebook directly in Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/query-aware-hybrid-ir/blob/main/notebooks/hybrid_model_IR.ipynb)

### Step 2 — Install Dependencies

Run the first cell in the notebook:

```python
!pip install beir rank_bm25 pytrec_eval sentence-transformers faiss-cpu
```

### Step 3 — Run In Order

Run each cell in order. The notebook is organized as:

```
Cell 1  → Install libraries + load FiQA dataset
Cell 2  → BM25 baseline
Cell 3  → Dense retrieval (takes ~90 mins on CPU, ~20 mins on GPU)
Cell 4  → Static hybrid fusion
Cell 5  → Adaptive hybrid (our system)
Cell 6  → Ablation study
Cell 7  → Failure analysis
Cell 8  → Visualizations
```

### Step 4 — Enable GPU (Recommended for Dense Encoding)

```
Colab Menu → Runtime → Change Runtime Type → T4 GPU → Save
```

---

## Dependencies

| Library | Version | Purpose |
|---|---|---|
| beir | 2.2.0 | Dataset loading + evaluation framework |
| rank_bm25 | latest | BM25 sparse retrieval |
| sentence-transformers | latest | Dense encoder (all-MiniLM-L6-v2) |
| faiss-cpu | latest | Approximate nearest neighbour search |
| pytrec_eval | latest | IR evaluation metrics |
| matplotlib | latest | Visualizations |

---

## Dataset

We use the **FiQA** (Financial Question Answering) dataset from the **BEIR benchmark**.

- **Corpus:** 57,638 financial documents
- **Queries:** 648 test queries
- **Source:** https://github.com/beir-cellar/beir
- **License:** Apache 2.0

The dataset is automatically downloaded when you run the notebook. No manual download needed.

---

## Reproducing The Results

The exact numbers from our paper can be reproduced by running the notebook end-to-end. Expected output:

```
=== Final Results ===
BM25              NDCG@10: 0.1591   MAP@10: 0.1163   Recall@100: 0.3590
Dense             NDCG@10: 0.3687   MAP@10: 0.2914   Recall@100: 0.7061
Static Hybrid     NDCG@10: 0.2943   MAP@10: 0.2231   Recall@100: 0.6633
Adaptive Hybrid   NDCG@10: 0.3395   MAP@10: 0.2669   Recall@100: 0.6683
```

---

## Citation

If you use this code or results in your research, please cite:

```bibtex
@article{varsini2025queryadaptive,
  title   = {Query-Aware Adaptive Hybrid Retrieval for Financial
             Information Retrieval: A Systematic Evaluation on the FiQA Benchmark},
  author  = {Varsini, Amirthaa and Sharon, Ketrolin and Shri, Thulasi},
  journal = {Information Retrieval Research Journal (IRRJ)},
  year    = {2025},
  url     = {https://irrj.org}
}
```

---

## Guide

This research was conducted under the guidance of **Dr. M. Akila Rani**, Department of Information Technology, Thiagarajar College of Engineering, Madurai, Tamil Nadu, India.

---

## License

This code is released under the **MIT License**. The FiQA dataset is licensed under Apache 2.0 by the BEIR team.
