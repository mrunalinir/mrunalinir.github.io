---
layout: page
title: "Multilingual Hallucination Probes: Do English Correctness Probes Transfer Across Languages?"
description: Zero-shot cross-lingual hallucination detection by probing Qwen2.5-7B hidden states
importance: 1
category: research
img: /assets/img/auc_best_by_method_stage_lang.png
github: 
related_publications: false
---

## Problem

Hallucination detectors are built and tested almost entirely in English. Billions of people use LLMs in other languages with far fewer safeguards, and nobody had checked whether English-trained detection even works there.

## Fix

A **CMU** team project. We trained a **correctness probe** only on **English** hidden states of **Qwen2.5-7B-Instruct**, then tested it zero-shot, no target-language training data at all, on **Chinese, Thai, Vietnamese, and Indonesian**. The bet: correctness probes already transfer across English tasks, and cross-lingual representations tend to converge in a model's deeper layers, so an English-trained probe should carry over. We trained linear (logistic regression) and nonlinear (MLP) probes on English MMLU hidden states and evaluated them on the post-cutoff SeaExam and M3Exam benchmarks.

## Impact

**It transfers.** Every probe cleared its language-specific confidence baseline in all four target languages. The signal lives in the representation, not just in output probabilities. Best probe (PyTorch MLP, post-answer features, layer 24): 0.704 AUC-ROC on English, 0.677 Chinese, 0.663 Indonesian, 0.650 Vietnamese, 0.641 Thai, with zero target-language training data.

{% include figure.liquid path="assets/img/auc_best_by_method_stage_lang.png" class="img-fluid rounded z-depth-1" caption="Best-layer AUC for every probe across both feature stages (dark = post-answer, light = pre-answer) and all five languages. Bars clear the per-language confidence baseline (dashed line), and the post-answer, nonlinear probes lead throughout." %}

**Timing beats probe choice.** Reading the hidden state after the model commits to an answer beats reading it before, for nearly every layer and language. Swapping classifiers barely moved the needle: random forests landed within 0.01 AUC of the MLP. The bottleneck is the representation, not the classifier.

{% include figure.liquid path="assets/img/pre_post_delta_heatmap.png" class="img-fluid rounded z-depth-1" caption="Post-answer minus pre-answer AUC per layer and language. Warm cells mark where reading the hidden state after the answer helps, which is almost everywhere, with the largest gains in the early-to-mid layers." %}

**Depth matters, language matters.** The signal is weak early and strengthens deeper in the network, converging toward English after about layer 14. Chinese transfers best (shares more of Qwen2.5's pretraining data), Thai worst. Gap to English settles at 0.03-0.08 AUC in deeper layers.

{% include figure.liquid path="assets/img/heatmap_auc_layer_lang.png" class="img-fluid rounded z-depth-1" caption="AUC by layer and language (logistic, post-answer); boxed cells mark each language's best layer. Deeper layers carry a stronger, more language-agnostic correctness signal, and Chinese stays closest to English." %}

**Cheap to train.** 30k English examples hit near-ceiling performance; even 1.5k cleared 0.60 AUC everywhere. Scaling to 45k added nothing and slightly overfit to English.

**Where it breaks.** Confident hallucinations slip through: when the model is wrong but sure of itself (average confidence 0.87), the hidden state doesn't betray the error. The probe also confuses "doesn't know" with "is hallucinating," pointing toward a three-way (correct, uncertain, hallucinating) label for real deployment.

## Method

- **Model:** Qwen2.5-7B-Instruct (4-bit quantized), hidden states read at the MLP input across all 28 layers
- **Probes:** logistic regression, MLP (sklearn and PyTorch, 3584 to 256 to 128 to 1), linear SVC, random forest
- **Labels:** stochastic resampling (10 samples, T=1.0) into correct, hallucination, and absence
- **Data:** train on English MMLU (fact-based subjects), evaluate zero-shot on SeaExam (Thai, Vietnamese, Indonesian) and M3Exam (Chinese)

## Keywords

Hallucination detection, multilingual LLMs, probing, cross-lingual transfer, interpretability, Qwen2.5, AI safety.
