---
title: "ICLR 2023 - RankCSE, Jensen-Shannon Divergence"
date: 2022-11-12T17:13:06-06:00
draft: true
---

[Original Paper](https://openreview.net/pdf?id=y_sZyxuuFh3)

<br>
{{< figure src="/img/rankcse1.png" caption="RankCSE system overview" width="500px" >}}
<br>
<!-- <img src="/img/rankcse.png" width="400px"> -->

RankCSE improves upon [DiffCSE](https://arxiv.org/abs/2204.10298), [SimCSE](https://arxiv.org/abs/2104.08821) and [the like](https://github.com/Doragd/Awesome-Sentence-Embedding) in unsupervised learning of sentence embeddings by introducing ranking distillation & consistency to the classic contrastive training objective. It works well becauses it addresses the largest weakness of the [NT-Xent Loss](https://paperswithcode.com/method/nt-xent) - there is no mechanism to capture how "relatively positive" each negative should be, or the distinction between in-batch negatives. 
<!-- (and [RankEncoder](https://openreview.net/pdf?id=g77JafrHWyy)) -->

In contrast to the pointwise approach, RankCSE distills ranking knowledge from a teacher by minimizing the cross entropy loss between the student/teacher top-1 probability distributions of sentence similarity lists. In addition, they introduce another loss term, which presumably smooths the loss landscape for the student model:

<br>
{{< figure src="/img/rankcse.png" caption="Ranking consistency by minimizing Jensen-Shannon Divergence" width="600px" >}}
<br>

Code that I want to make use of:

{{< gist perceptiveshawty 4b6086ef1aae8cb4b29380e30d096219 >}}
