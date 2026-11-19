---
layout: page
title: "Outcome-Aware Web Agents: Does Predicting Page Transitions Help VLM Action Selection?"
description: Controlled SFT study of outcome-aware supervision on Qwen3-VL for Multimodal Mind2Web
importance: 1
category: research
img: /assets/img/idl_images/architecture.png
github: 
related_publications: false
---

## Problem

Teams keep bolting "predict what changes on the page" onto web agents, assuming it makes them pick better actions. Prior work tangles that signal up with costly inference-time simulation or several other training objectives at once, so nobody could tell if the outcome signal itself was doing anything.

## Fix

A **CMU** team project (Team 16). We isolated it: fine-tuned **Qwen3-VL-8B-Thinking** with **LoRA** on **Multimodal Mind2Web** under two conditions that differ in exactly one thing. Action-only learns to predict the next action. Outcome-aware predicts the action plus a structured transition label (type, changed region, magnitude, confidence). Architecture, the 6,445 training examples, every hyperparameter, all held constant.

{% include figure.liquid path="assets/img/idl_images/architecture.png" class="img-fluid rounded z-depth-1" caption="The setup. Multimodal input (screenshot, cleaned HTML, instruction, candidate actions) feeds a frozen Qwen3-VL-8B-Thinking with LoRA adapters. The only thing that changes between the two conditions is the supervision target: an action index, or that same index plus the transition label." %}

## Impact

**The extra signal didn't help.** Both conditions nearly doubled Step Success Rate over the zero-shot baseline on the unseen-website split (31.99% to 62.32% action-only, 59.76% outcome-aware). The two land within bootstrap variance of each other, a **null result**, and it held across all three Mind2Web test splits.

{% include figure.liquid path="assets/img/idl_images/results_metrics_barchart.png" class="img-fluid rounded z-depth-1" caption="Element Accuracy, Operation F1, and Step Success Rate across all ten configurations on the unseen-website split. Both fine-tuned conditions tower over the zero-shot and prompting baselines, but the action-only and outcome-aware bars sit almost on top of each other." %}

We checked that the outcome-aware model wasn't just undertrained.

{% include figure.liquid path="assets/img/idl_images/sft_loss_curves.png" class="img-fluid rounded z-depth-1" caption="Training and evaluation loss for both SFT conditions. Both converge cleanly, so the missing outcome-aware gain is a genuine null result rather than an artifact of poor training. The two eval-loss curves aren't directly comparable, since the outcome-aware target carries extra tokens, which is why we judge the conditions on the action metrics above, not on loss." %}

**Found why it fails: a terminal-action bias.** The outcome-aware model leans toward terminal-looking actions, clicking a child menu item instead of hovering the parent that reveals it. A hover-then-click and a direct click land on the same final page state, so a categorical outcome label can't tell them apart.

**Ruled out the obvious alternatives first.** HTML and screenshot inputs are both necessary. Few-shot and chain-of-thought prompting hurt under log-likelihood scoring (AXTree dropped 13.6pp, few-shot 4.6pp, CoT 10.7pp), which is what pushed the team toward fine-tuning in the first place.

So: a controlled comparison showing categorical outcome labels don't help. Skip bolting this signal onto an agent, and spend the effort on richer outcome representations instead.

## Technical Stack

- **Model:** Qwen3-VL-8B-Thinking, LoRA (r=64, alpha=128)
- **Data:** Multimodal Mind2Web, transition labels generated with Gemma 3 27B-IT
- **Training & eval:** HuggingFace Transformers, length-normalized log-likelihood scoring

## Keywords

Web agents, vision-language models, LoRA fine-tuning, outcome supervision, Multimodal Mind2Web, Qwen3-VL.
