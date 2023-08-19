---
layout: single
title: "AI Bootcamp Assignment - Secure Spam Filter"
permalink: /projects/spam-filter
---

**GitHub:** [XGBoost Spam Filter](https://github.com/adobiss/ai-ml-portfolio/tree/main/XGBoost_spam_filter)

## Assignment Objective

The task was to design a spam filter prioritising cybersecurity. The central challenge was to robustly minimise false negatives, recognising that missing genuine threats holds significant repercussions in a cybersecurity environment.

## Approach

A conscious decision was made to avoid utilising any spam filter tutorials. This strategy aimed to ensure a comprehensive understanding of both the dataset and the algorithm.

## Dataset

A raw text dataset of labeled emails was chosen, echoing the real-world scenario where spam emails (positive class) are less frequent than genuine ones.

## Algorithm Selection

The XGBoost algorithm emerged as the choice due to:

- Its tree-based structure is efficient for sparse datasets.
- The ability to integrate a weighted loss function and L1 regularization.
- Its recognised speed and computational efficiency.

## Feature Processing

Essential preprocessing was applied to the dataset to prepare it for the model.

## Model Performance

The model was fine-tuned to strike a balance between accuracy and critical cybersecurity needs. Performance metrics revealed:

- A proficiency in detecting spam, with **99%** of such emails accurately classified.
- A cautionary stance leading to **3-4%** of legitimate emails potentially being flagged as spam.

## Future Considerations

Potential enhancements might include further feature refinement and automated hyperparameter adjustments.

For an in-depth analysis and access to the codebase, please [explore the GitHub repository](https://github.com/adobiss/ai-ml-portfolio/tree/main/XGBoost_spam_filter).
