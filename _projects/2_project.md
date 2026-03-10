---
layout: page
title: ZulipGPT – LLM Integration for Chat Summarization in Open-Source Messaging
description: Privacy-safe chat and inbox summarization for the Zulip open-source messaging platform
importance: 3
category: projects
github: 
related_publications: false
---

## Project Overview

Built **ZulipGPT**, a privacy-safe LLM integration for the **Zulip** open-source messaging platform that delivers chat and inbox summarization with strong privacy guarantees and low-latency inference.

## Key Achievements

- **Production Summarization**: Shipped chat and inbox summarization into the Zulip codebase with **topic-drift detection** and **citation-backed prompts** to reduce hallucination and prompt injection risk.
- **Privacy by Design**: Built a deterministic **identity-masking pipeline** using keyed pseudonym mapping *before inference*, providing a stronger privacy guarantee than post-hoc PII filtering since the model never sees real identities.
- **Latency & Cost Optimizations**: Cut summarization latency to **under 15 seconds** via **trigger-based invocation**, **rolling context windows**, and **message batching**, enabling practical deployment for active teams.

## Technical Stack

- **Platform**: Zulip (open-source)
- **Techniques**: LLM integration, privacy-preserving pre-processing, inference optimization
- **Tools**: Python, HuggingFace, structured prompting

## Impact

Demonstrated how to integrate LLM capabilities into a real-world messaging system while preserving user privacy and keeping inference latency low enough for interactive workflows.
