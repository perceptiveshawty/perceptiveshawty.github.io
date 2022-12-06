+++
author = "Sachin Chanchani"
title = "Self-knowledge distillation with dropout"
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

Self-knowledge distillation sounds like circular logic but it isn't. It is essentially a clever way of splitting a model into an ensemble, where each member model receives a different, independent perspective of the input during training. In computer vision, "perspectives" can be created with crops, distortions, and a host of other transforms (well documented in [SimCLR](https://arxiv.org/abs/2002.05709)); in NLP typically just token-level dropout is used. In both cases, ensembling the hidden layer weights from each member model can speed up training with a more stable loss function. 

The main reason for this is that most model architectures in deep learning are over-parameterized, and for a given downstream task, only a small fraction of the parameters are actually needed to achieve the desired performance. For [example](https://arxiv.org/pdf/2012.13255.pdf), only about 200 trainable parameters are needed to recover 90% of the performance on the heavily cited [MRPC](https://www.microsoft.com/en-us/download/details.aspx?id=52398) task.

See also: 

[Loss Surface Simplexes for Mode Connecting Volumes and Fast Ensembling](https://arxiv.org/pdf/2102.13042.pdf)

[Averaging Weights Leads to Wider Optima and Better Generalization](https://arxiv.org/pdf/1803.05407.pdf)

[Learning Neural Network Subspaces](https://arxiv.org/pdf/2102.10472.pdf)

{{< figure src="/img/kd.png" caption="SD-Dropout overview" width="100%" >}}

