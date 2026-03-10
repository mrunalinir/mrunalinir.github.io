---
layout: page
title: SteelRAG – Hybrid Sparse-Dense Retrieval over a Crawled Local Knowledge Corpus
description: Hybrid BM25 + dense retrieval over a curated local corpus
importance: 2
category: projects
github: 
related_publications: false
---

## Overview

SteelRAG is a **CMU** project that builds a hybrid sparse–dense retrieval system over a crawled local knowledge corpus to improve answer quality on previously unanswered question clusters.

## Key Achievements

- **Corpus Construction:** Built a **5,334-document corpus** from **20+ sources** via three targeted scraping rounds, guided by gap analysis of ~117 unanswered question clusters; corpus expansion alone drove a **+6.8% absolute gain** in a hybrid F1 and LLM-judge score.
- **Hybrid Retrieval:** Implemented **BM25 (bm25s)**, **FAISS** with **all-MiniLM-L6-v2 (384-dim)**, and **RRF** from scratch; hybrid RRF outperformed dense-only by **+4.46%** across **F1, Recall, ROUGE-L, and LLM Judge**.
- **Efficient Indexing:** Deployed **Qwen2-7B-Instruct** on **Modal A10G GPU**; batch embedding cut index build time from **3 hours to under 15 minutes**, and reducing chunk size from 200 to 100 words improved F1 by **+1.40%** with no recall loss.

## Technical Stack

- **Retrieval:** BM25 (bm25s), FAISS, RRF
- **Models:** all-MiniLM-L6-v2, Qwen2-7B-Instruct
- **Infra:** Modal A10G GPU, Python

