---
layout: page
title: "ScleraNext: Lightweight CNN Segmentation for Real-Time Biometric Identification"
description: Real-time iris/retinal segmentation optimized for edge deployment
importance: 2
category: research
github: 
related_publications: false
---

## Problem

Iris and retinal segmentation for biometric ID is usually too slow to run on a phone or IoT device. The segmentation step is what bottlenecks the whole pipeline.

## Fix

A collaboration with the **University of Ljubljana**. Replaced a cascaded two-stage segmentation CNN with a single compact model, picked after benchmarking YOLO, U-Net, MobileNet, and DenseNet on accuracy versus latency.

## Impact

- Cut inference latency by 73%, making real-time segmentation feasible on-device instead of on a server.
- Held accuracy while running far cheaper, on evidence from the benchmark, not a default choice.
- Removes the round trip to a server, so biometric data stays on the phone instead of shipping out.

## Keywords

Biometric identification, CNN segmentation, edge deployment, University of Ljubljana.
