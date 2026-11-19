---
layout: page
title: "GraphAct: Graph-Structured Action Prediction for Web Agents"
description: A DOM graph transformer fused into Qwen3-VL with LoRA to fix element grounding on Multimodal Mind2Web
importance: 5
category: research
img: /assets/img/multimodal_images/modelarch.png
github: 
related_publications: false
---

## Problem

Multimodal web agents keep clicking the wrong button. Our failure analysis on **Multimodal Mind2Web** found the model almost always knows it should click, it just picks the wrong one of several near-identical candidates. Most systems flatten the page DOM into text and expect a large model to infer structure that was right there in the HTML.

## Fix

A **CMU** team project. We represent each page as a directed graph of DOM elements instead of flattened text, and fuse it into a frozen **Qwen3-VL-8B** backbone through a graph attention network and a lightweight gated cross-attention adapter, training only a small set of LoRA weights. The whole pipeline trains and runs on a single 24GB GPU.

{% include figure.liquid path="assets/img/multimodal_images/modelarch.png" class="img-fluid rounded z-depth-1" caption="How it fits together. The page DOM is parsed into a graph and encoded by a 3-layer graph attention network, where each node is a 523-dim vector (a MiniLM text embedding plus a tag one-hot and a handful of structural features). A gated cross-attention adapter injects those node embeddings into the frozen Qwen3-VL-8B at an early decoder layer, and only the LoRA weights are trained to predict the action index." %}

## Impact

**Grounding is the bottleneck, not action choice.** Action-type accuracy sat at 74-80% across every baseline while element accuracy lagged far behind. Step success tracks element accuracy almost one to one.

{% include figure.liquid path="assets/img/multimodal_images/plots23.png" class="img-fluid rounded z-depth-1" caption="Intrinsic metrics across ablations. Action accuracy (orange) barely moves whether or not the graph is present, while element and step accuracy collapse without it and jump back once the DOM graph is added." %}

**The graph nearly quadrupled element accuracy.** 12.7% (fine-tuned Qwen, no graph) to 49.5%, beating the strongest multimodal baseline (37.4%) by about 12 points. Step accuracy reached roughly 41%.

{% include figure.liquid path="assets/img/multimodal_images/plots.png" class="img-fluid rounded z-depth-1" caption="Per-metric breakdown against the text-only baseline (dashed line). The DOM graph lifts element accuracy by about 37 points and step accuracy by about 30, while action accuracy was already near its ceiling." %}

**Full-task success stayed capped at 7.75%.** Errors compound across long multi-step trajectories, so better per-step grounding helps but isn't enough on its own for long-horizon reliability. We traced two concrete failure modes, an anchor/fixation bias from static per-step graph snapshots and node pruning that drops structurally critical but text-sparse elements like hover-trigger menus, and proposed dynamic node masking and topology-aware retention as fixes.

## Technical Stack

- **Backbone:** Qwen3-VL-8B (frozen, 4-bit NF4 quantized), LoRA (r=8, alpha=16) on layers 7 to 9, 15 to 17, and 23 to 25
- **Graph:** 3-layer Graph Attention Network over DOM nodes, 523-dim node features (all-MiniLM-L6-v2 embedding + tag one-hot + structural cues)
- **Fusion:** tanh-gated cross-attention adapter projecting graph nodes into Qwen's hidden space, injected at decoder layer 8
- **Data & infra:** Multimodal Mind2Web, precomputed graph cache, single 24GB GPU

## Keywords

Web agents, graph attention networks, DOM graphs, vision-language models, LoRA, Multimodal Mind2Web, Qwen3-VL.
