+++
author = "Sachin Chanchani"
title = "RankCSE and Jensen-Shannon Divergence"
date = "2022-11-12T17:13:06-06:00"
description = "Stuff I took away from RankCSE and need to implement"
tags = [
    "sentence-embeddings",
    "iclr-2023"
]
categories = [
    "paper",
    "nlp"
]
series = ["NLP"]
+++

[Original Paper](https://openreview.net/pdf?id=y_sZyxuuFh3)

{{< figure src="/img/rankcse1.png" caption="RankCSE system overview" width="80%" >}}


RankCSE improves upon [DiffCSE](https://arxiv.org/abs/2204.10298), [SimCSE](https://arxiv.org/abs/2104.08821) and [the like](https://github.com/Doragd/Awesome-Sentence-Embedding) in unsupervised learning of sentence embeddings by introducing ranking distillation & consistency to the classic contrastive training objective. It works well becauses it addresses the largest weakness of the [NT-Xent Loss](https://paperswithcode.com/method/nt-xent) - there is no mechanism to capture how "relatively positive" each negative should be, or the continuity of the similarity of in-batch negatives. They propose adding two losses to the standard contrastive loss that better model the rankings of negative examples for each data point.
<!-- (and [RankEncoder](https://openreview.net/pdf?id=g77JafrHWyy)) -->

First, RankCSE distills ranking knowledge from a teacher by minimizing the cross entropy loss between the student/teacher top-1 probability distributions of sentence similarity lists. These similarity lists are created on the fly during training, represented by an n x n distance matrix for n examples in a mini-batch. Taking the softmax of an example's similarity list yields the top-1 similarity probability distribution for an example. 

{{< figure src="/img/rankcse.png" caption="Ranking consistency by minimizing Jensen-Shannon Divergence" width="80%" >}}

Added to the ranking distillation loss is the ranking consistency loss - since the base sentence encoder samples two instances with different dropout masks for every unique example in the dataset, minimizing the [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen%E2%80%93Shannon_divergence) between the top-1 similarity distributions for both samples may smooth the loss landscape for the ranking distillation. In practice, they observe that adding this loss without knowledge distillation results in preserving inaccurate rankings. 

In general, minimizing the Jensen-Shannon divergence (JSD) between the weights of different neural network models can lead to good results for several reasons. First, JSD is a measure of the similarity between two probability distributions, and thus minimizing JSD between the weights of different models can encourage these models to learn similar representations of the data. This can improve the performance of the models by reducing the amount of variability and noise in their predictions. Additionally, minimizing JSD between the weights of different models can encourage them to share information and learn from each other, which can lead to better generalization and improved performance on unseen data. Finally, minimizing JSD between the weights of different models can help to reduce overfitting, as it encourages the models to learn more robust and generalizable representations of the data.

I have integrated these loss functions into my own SimCSE-based code [here](https://github.com/perceptiveshawty/TreeCSE/blob/master/treecse/models.py). 
