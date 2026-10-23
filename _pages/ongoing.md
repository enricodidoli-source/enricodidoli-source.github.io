---
layout: archive
title: "Ongoing Projects"
permalink: /ongoing/
author_profile: true
---

Here is a collection of projects I am currently working on.

### Single-Cell Classification
An expansion of the work done for my Master's thesis, "Detecting Measurable Residual Disease in B-cell Acute Lymphoblastic Leukaemia using Convolutional Neural Networks", where the primary goal was sample classification. Utilizing the model trained for that purpose, I clustered the trained filters and used them to classify single cells while maintaining a MIL (Multiple Instance Learning) approach.

**Next Steps**: Finalizing the clustered filter selection and introducing filter responses.

Preliminary code is available in my [Single-cell classification GitHub repository](https://github.com/enricodidoli-source/master-thesis/blob/main/CellCNN/notebooks/refactoring_single_cell_detection.ipynb).

### Uncertainty-Aware RAG
To explore RAG structures, limits, and improvements, I employed a compact Foundation model (Qwen-0.5B) and built a pipeline to optimize chunking, overlap, and answering parameters using Bayesian Optimization. 
Additionally, I implemented the tuning of a confidence threshold to decide whether an answer should be sent to the client or rejected. 

**Next Steps**: Including the prompt template structure as an optimizable hyperparameter and implementing multiple answer selection.

Preliminary code is available in my [Uncertainty-Aware RAG GitHub repository](https://github.com/enricodidoli-source/rag_project).
