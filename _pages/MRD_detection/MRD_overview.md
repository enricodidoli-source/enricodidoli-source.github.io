---
layout: archive
title: "Master's Thesis: Detecting Measurable Residual Disease in B-cell Acute Lymphoblastic Leukaemia using Convolutional Neural Networks"
permalink: /MRD_overview/
author_profile: true
---


# Detecting Measurable Residual Disease in B-ALL using Convolutional Neural Networks

## Abstract & Context
For my Master's thesis, I focused on improving the detection of **Measurable Residual Disease (MRD)** in patients with **B-cell Acute Lymphoblastic Leukaemia (B-ALL)**. MRD refers to the small number of cancer cells that remain in the body during or after treatment. Being able to detect small quantity of leukaemic cells is critical for predicting relapse and guiding clinical decisions.

Traditional analysis of Multiparameter Flow Cytometry (MFC) data relies heavily on manual gating by expert clinicians, which can introduce experts' biases and that is time-consuming. In this project, I explored the **CellCNN** architecture to process and classify high-dimensional flow cytometry data.

---

## Methodology & Architecture

The project pipeline is built around several core components designed to handle complex biological data:

* **Model Architecture:** Adapted and modified the original **CellCNN** allowing grid search and different metrics to evaluate performance on validation sets during training.
* **Hyperparameter Optimization:** Integrated **Optuna** for automated Bayesian hyperparameter tuning to optimize model internal data augmentation and threshold selection.
* **Validation Strategy:** Implemented robust cross-validation schemes (such as Leave-One-Patient-Out Cross-Validation, LOPOCV) to ensure generalization on unseen patient data ant to address limited size datasets.
* **Threshold Selection:** Proposed two classification threshold tuning approaches based on F1-score and Recall performance metrics.
* **Dataset Data Augmentation:** Proposed the generation of Artificial Samples (AS) built at patient level to avoid data leakage.
* **Computational Constraints:** Experiments were engineered and executed within resource limits (utilizing Google Colab's CPU runtimes).

---

## Key Results & Outputs

The repository's experimental framework generates comprehensive evaluation metrics and visual reports, including:
* Patient-specific clinical info summaries and prediction distributions.
* CellCNN's Internal Data Augmentation parameter selection via Bayesian optimization plots.
* Single-split and ensemble model comparisons analyzing classification metrics (F1-Score, Recall, Precision and Accuracy).

---

## Thesis Document & Resources

* 📁 **Experiments, Results, and Plots:** Detailed experimental outputs and plots are available in my thesis. You can Read it in the page viewer below or  **Read/Download it** using the following two buttons.


[Download the Paper](/assets/pdf/Master_Thesis_Enrico_Didoli.pdf){: .btn .btn--info}
[View Source Code](https://github.com/enricodidoli-source/master-thesis/tree/thesis-version){: .btn .btn--primary}

---

<iframe src="/assets/pdf/Master_Thesis_Enrico_Didoli.pdf" width="100%" height="800px" style="border: 1px solid #ccc;"></iframe>
---
