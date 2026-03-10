---
layout: page
title: Real-Time Movie Recommendation Platform
description: Low-latency movie recommender with automated retraining, monitoring, and A/B testing
importance: 1
category: projects
github: 
related_publications: false
---

## Project Overview

Built a **real-time movie recommendation platform** at **CMU** that serves low-latency recommendations over a streaming interaction pipeline, with automated retraining, evaluation, and monitoring.

## Key Achievements

- **Collaborative Filtering Backbone**: Trained an SVD collaborative filtering model on ~200K Kafka interactions and deployed a Flask API with **<50 ms latency**, containerized with Docker and scheduled **retraining every 3 days**.
- **Cold-Start Coverage**: Designed a **hybrid cold-start solution** that combines interaction and content signals, achieving **85%+ coverage** on new users.
- **End-to-End Data & Evaluation Pipeline**: Built a full pipeline including schema validation, drift detection, and offline/online evaluation with **NDCG@10 = 0.52** and **HR@10 = 0.68**, wired into CI/CD with ~82% test coverage.
- **Production Monitoring**: Set up a monitoring dashboard tracking **>99% availability**, model accuracy, infrastructure costs, and data drift statistics.
- **A/B Testing Infrastructure**: Designed and ran A/B experiments to quantify cold-start impact, finding that the cold-start strategy yields a **+8% lift in NDCG@10**.

## Technical Stack

- **Data & Serving**: Kafka, Flask, Docker
- **Modeling**: SVD collaborative filtering, cold-start hybrid design
- **Tooling**: Python, Pandas, CI/CD, monitoring dashboards

