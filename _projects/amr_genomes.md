---
layout: page
title: Predicting antibiotic resistance from genomes
description: 3rd of 39 in the INF8245 Kaggle competition, with a calibrated gradient boosting ensemble
importance: 2
category: /ML&AI
related_publications: false
---

- **Context:** Kaggle competition, INF8245 (Fall 2025), team project
- **Stack:** XGBoost, CatBoost, LightGBM
- **Result:** 3rd of 39

Antimicrobial resistance is a major challenge in modern medicine, and predicting it directly from a genome is a step toward faster diagnostics. The task: given one *E. coli* genome, predict whether it is resistant to the antibiotic Cefepime. The metric is macro F1.

## Data

Each genome is turned into a bag of 31-mers: a window of 31 DNA bases slides along the sequence, and the 1 million most frequent 31-mers become features (raw counts). With about 3,000 genomes, this gives an extremely wide, sparse matrix.

## What made it hard

- **Dimensionality:** about a million features for roughly three thousand samples.
- **Class imbalance:** hence the macro F1 metric.
- **Distribution shift:** the private test set includes a phylogenetic split from a different evolutionary branch, which requires real generalization.

## Approach

An out-of-fold, calibrated mixture-of-experts ensemble of gradient boosting models (XGBoost, CatBoost, LightGBM).

Team: Adrien Saouma, Mateo Mangialomini, Maxime Tran.

[Code](https://github.com/mateo-496/ecoli-amr-kaggle) · [Report (PDF)](https://github.com/mateo-496/ecoli-amr-kaggle/blob/main/report.pdf)
