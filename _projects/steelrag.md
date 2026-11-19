---
layout: page
title: "SteelRAG: Hybrid Sparse-Dense Retrieval over a Crawled Local Knowledge Corpus"
description: Hybrid BM25 + dense retrieval over a curated local corpus
importance: 2
category: projects
github: 
related_publications: false
---

## Problem

An existing system kept failing on the same cluster of questions, and nobody had mapped out why.

## Fix

A **CMU** project. Built a hybrid sparse-dense retrieval system over a crawled corpus, targeted directly at the gaps: scraped a 5,334-document corpus from 20+ sources in three rounds, each guided by analysis of about 117 question clusters the old system couldn't answer. Added BM25 (bm25s), FAISS (all-MiniLM-L6-v2, 384-dim), and Reciprocal Rank Fusion from scratch.

## Impact

- Expanding the corpus around the gaps alone raised the combined F1/LLM-judge score by 6.8 points.
- Hybrid retrieval beat dense-only by 4.46% across F1, Recall, ROUGE-L, and LLM Judge.
- Batched embedding on a Modal A10G GPU cut index build time from 3 hours to under 15 minutes. Halving chunk size (200 to 100 words) added 1.40% F1 with no recall loss.

Most of the gain came from fixing the data and the retrieval, not a bigger model. The faster index build turned each experiment from an afternoon into a coffee break.

## Technical Stack

- **Retrieval:** BM25 (bm25s), FAISS, Reciprocal Rank Fusion
- **Models:** all-MiniLM-L6-v2, Qwen2-7B-Instruct
- **Infra:** Modal A10G GPU, Python
