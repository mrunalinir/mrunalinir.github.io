---
layout: page
title: Neural Music Recommender for Personalized Playlists
description: Learning user and track representations to generate personalized, sequence-aware playlists
importance: 1
category: projects
github: 
related_publications: false
---

## Project Overview

Built a **neural music recommendation system** that learns joint representations of users and tracks to generate personalized, sequence-aware playlists.

## Key Achievements

- **Hybrid Recommender**: Combined collaborative filtering signals (implicit feedback, co-listens) with content-based features (artist, genre, tempo, key) to improve cold-start performance on new tracks and users.
- **Sequence-Aware Modeling**: Used a recurrent / Transformer-style architecture over recent listening history to capture **short-term preferences** and session-level context.
- **Ranking Optimization**: Optimized for ranking metrics (NDCG@k, Recall@k) rather than pure reconstruction loss, improving top-k recommendation quality.

## Technical Stack

- **Data**: User–track interaction logs, basic audio/metadata features
- **Techniques**: Collaborative filtering, sequence modeling, representation learning
- **Tools**: Python, PyTorch, Pandas

## Impact

Demonstrated a practical path from raw listening logs to a production-like music recommender that can adapt to both long-term tastes and short-term session context.

