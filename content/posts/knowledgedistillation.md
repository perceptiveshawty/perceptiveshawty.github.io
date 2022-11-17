+++
author = "Sachin Chanchani"
title = "Self-Knowledge Distillation via Dropout"
date = "2022-11-16T17:13:06-06:00"
description = "Self-knowledge distillation with no add'l cost"
tags = [
    "knowledge-distillation",
]
categories = [
    "paper",
    "nlp"
]
series = ["NLP"]
+++

[Original Paper](https://arxiv.org/pdf/2208.05642.pdf)

Self-knowledge distillation sounds like circular logic but it isn't. It is essentially a clever way of splitting a model into an ensemble, where each member model receives a different, independent persepctive of the input during training. In computer vision, "perspectives" can be created with crops, distortions, and a host of other transforms (well documented in [SimCLR](https://arxiv.org/abs/2002.05709)); in NLP typically just token-level dropout is used. In any case, ensembling the hidden layer embeddings (or logits) from each member model leads to smoother, wider loss minima, and consequently faster training. 

See also: 

[Loss Surface Simplexes for Mode Connecting Volumes and Fast Ensembling](https://arxiv.org/pdf/2102.13042.pdf)

[Averaging Weights Leads to Wider Optima and Better Generalization](https://arxiv.org/pdf/1803.05407.pdf)

[Learning Neural Network Subspaces](https://arxiv.org/pdf/2102.10472.pdf)

{{< figure src="/img/kd.png" caption="SD-Dropout overview" width="100%" >}}

