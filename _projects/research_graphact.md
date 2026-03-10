---
layout: page
title: GraphAct – Graph-Structured Action Prediction for Web Agents
description: Graph Transformer over DOM graphs for multimodal web agents on Mind2Web
importance: 5
category: research
github: 
related_publications: false
---

## Overview

GraphAct is a **CMU** research project on **graph-structured action prediction** for multimodal web agents on **Multimodal Mind2Web**.

## Highlights

- **Baseline Benchmarking:** Benchmarked **10 baselines** on Multimodal Mind2Web using **Qwen3-VL** and **InternVL2-8B**, showing that prior work (e.g., MindAct, SeeAct, CogAgent) treats the HTML DOM as flat text and ignores its hierarchical structure.
- **Graph-Structured DOM Encoding:** Added a **Graph Transformer Encoder** over explicit DOM graphs to a frozen **Qwen3-VL** backbone, projecting node embeddings into the LLM token space as a first-class relational modality.
- **Composite Training Objective:** Trained with a **composite loss** that captures visual–graph alignment, action prediction, and action history consistency to better align model behavior with the underlying DOM structure.

## Keywords

Web agents, graph transformers, DOM graphs, Multimodal Mind2Web, Qwen3-VL.

