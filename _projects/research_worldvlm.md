---
layout: page
title: WorldVLM – Tuning Vision-Language Models as World Models for Web Agents
description: World-model-style training of Qwen2.5-VL on Mind2Web trajectories
importance: 4
category: research
github: 
related_publications: false
---

## Overview

WorldVLM is a **CMU** project exploring how vision-language models can serve as **world models** for web agents.

## Highlights

- **Joint Action & State Prediction:** Fine-tuned **Qwen2.5-VL** on **Mind2Web** trajectories to jointly predict the **next action** and **resulting visual page state**, upgrading current SoTA that simulates next states only via text with no visual grounding.
- **Consequence-Aware Planning:** Framed web browsing as a **transition function over (state, action) pairs**, enabling consequence-aware planning rather than reactive, step-by-step execution.

## Keywords

Web agents, vision-language models, world models, Mind2Web.

