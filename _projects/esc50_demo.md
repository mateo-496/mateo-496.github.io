---
layout: page
title: ESC-50 sound classification demo
description: A self-taught end-to-end deep learning project, deployed as a live web app
importance: 3
category: /ML&AI
related_publications: false
---

- **Context:** Personal project, 2026
- **Stack:** PyTorch, librosa, FastAPI, Docker, HuggingFace Spaces

An end-to-end deep learning project I built to learn the full pipeline. I extended the CNN from Salamon & Bello (2017) from 10 to 50 classes and kept its accuracy by using data augmentation techniques, which matter a lot on a small dataset like ESC-50. I then deployed the model as a FastAPI + Docker endpoint with a real-time web UI.

[Live demo](https://mateo496-esc50-model.hf.space/) · [Code](https://github.com/mateo-496/esc50-sound-classification)

<img src="/assets/img/projects/esc50-demo.png" alt="The ESC-50 demo web UI"
     style="display:block; width:100%; max-width:1000px; margin:1.5rem auto; border-radius:8px;">