---
layout: page
title: "PRISM: Probing Routed Information Flow via Structured Multimodal Bottlenecks"
description: Hierarchical multimodal fusion study on CMU-MOSEI/MOSI
importance: 3
category: research
github: 
related_publications: false
---

## Problem

Multimodal fusion papers mostly guess at where audio, video, and text should combine, and how much fusion capacity to pay for. Nobody tests it directly.

## Fix

A research project at **Carnegie Mellon University**. We tracked how information moves through hierarchical fusion modules on the CMU-MOSEI and CMU-MOSI sentiment benchmarks, comparing fusion structure and bottleneck size head to head.

## Impact

- Hierarchical fusion beat the symmetric baseline by 2.7% (Acc2/F1). Routing modalities through a structured bottleneck beats dumping them together.
- Asymmetric fusion (one modality into another) matched symmetric fusion at lower parameter cost. The trade-off that matters when a model has to ship.
- Scaling the bottleneck from 4 to 12 tokens dropped correlation by 6%. More capacity, worse model.

Design rule for multimodal systems: spend parameters on where and how you fuse, not on how much.

## Keywords

Multimodal fusion, routed information flow, CMU-MOSEI, CMU-MOSI.
