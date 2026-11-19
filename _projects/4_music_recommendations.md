---
layout: page
title: Real-Time Movie Recommendation Platform
description: Low-latency movie recommender with automated retraining, monitoring, and A/B testing
importance: 1
category: projects
github: 
related_publications: false
---

## Problem

A recommender that works in a notebook falls apart in production. New users get nothing useful (cold start), quality decays as data shifts, and nobody notices until users complain.

## Fix

Built a production-style movie recommender at **CMU**: an SVD collaborative-filtering model served behind a Flask API, retrained automatically every 3 days, with a hybrid cold-start strategy blending interaction and content signals for new users. Wrapped the whole thing in schema validation, drift detection, and a monitoring dashboard.

## Impact

- Serves recommendations under 50ms, trained on roughly 200K Kafka interactions, containerized with Docker.
- Cold-start coverage hit 85%+ on new users. An A/B test confirmed it, showing an 8% lift in NDCG@10, not just an assumption.
- CI/CD pipeline at 82% test coverage; offline/online eval locked in at NDCG@10 = 0.52, HR@10 = 0.68.
- Dashboard tracks uptime above 99%, model accuracy, infra cost, and data drift, catching problems before users feel them.

## Technical Stack

- **Data & serving:** Kafka, Flask, Docker
- **Modeling:** SVD collaborative filtering, hybrid cold-start design
- **Tooling:** Python, Pandas, CI/CD, monitoring dashboards
