---
layout: page
title: Cross-Modal Bottleneck Transformers for Efficient Multimodal Fusion
description: Hierarchical bottleneck fusion for multimodal sentiment analysis
img: assets/img/1.jpg
importance: 1
category: work
github: 
related_publications: false
---

## Project Overview

This research project, conducted at **Carnegie Mellon University** (October 2025 - December 2025), focused on designing efficient multimodal fusion architectures for sentiment analysis tasks using bottleneck transformers.

## Key Achievements

### Architecture Design & Implementation
- Designed and implemented multiple **Multimodal Bottleneck Transformer** architectures on CMU MOSI and CMU MOSEI datasets
- Developed early-fusion, mid-fusion, late-fusion, and bottleneck-based baseline models
- Created a hierarchical bottleneck fusion mechanism that **improved Acc2 by 4.3%** and **F1 by 2.8%** over the strongest Multimodal Bottleneck Transformer baseline

### Systematic Evaluation
- Performed systematic ablations over bottleneck placement and token budgets using reproducible training pipelines
- Quantified accuracy-compute tradeoffs via **FLOPs analysis** to understand efficiency gains
- Ensured experimental robustness by reproducing results across **multiple random seeds** and dataset splits

### Engineering & Reproducibility
- Built **config-driven training and logging pipelines** to support extensible ablations
- Implemented comprehensive experiment tracking for reproducibility
- Developed scalable pipeline infrastructure for multimodal model training

## Technical Stack

- **Frameworks**: PyTorch, HuggingFace Transformers
- **Datasets**: CMU MOSI, CMU MOSEI
- **Techniques**: Transformer architectures, bottleneck fusion, multimodal learning
- **Tools**: Python, Weights & Biases (experiment tracking)

## Research Impact

This work demonstrates that hierarchical bottleneck mechanisms can significantly improve multimodal fusion efficiency while maintaining or improving performance on sentiment analysis tasks. The systematic evaluation framework enables reproducible research and provides insights into the tradeoffs between model capacity and computational cost.

## Skills Demonstrated

- Deep Learning & Transformer Architectures
- Multimodal Machine Learning
- Experimental Design & Ablation Studies
- ML Systems & Pipeline Development
- Research Reproducibility Best Practices
