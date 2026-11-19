---
layout: page
title: "ZulipGPT: LLM Integration for Chat Summarization in Open-Source Messaging"
description: Privacy-safe chat and inbox summarization for the Zulip open-source messaging platform
importance: 3
category: projects
github: 
related_publications: false
---

## Problem

Catching up on a busy Zulip channel means reading everything. Bolt an LLM summarizer on top and you've got a new problem: raw messages, including real identities, now leave the app and head to a model.

## Fix

Built chat and inbox summarization directly into Zulip. A deterministic masking pipeline swaps real identities for keyed pseudonyms before anything reaches the model, so the model never sees who said what. Summaries cite the messages they're drawn from to resist prompt injection, and a drift check keeps them from wandering off-topic.

## Impact

- Shipped into the actual Zulip codebase, not a demo fork.
- Summaries land in under 15 seconds, using trigger-based invocation, rolling context windows, and message batching.
- Identity protection happens before inference, not as cleanup after. Stronger guarantee than scrubbing PII from the output.

## Technical Stack

- **Platform:** Zulip (open-source)
- **Techniques:** LLM integration, privacy-preserving pre-processing, inference optimization
- **Tools:** Python, HuggingFace, structured prompting
