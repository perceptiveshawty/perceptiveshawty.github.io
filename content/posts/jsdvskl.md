+++
author = "Sachin Chanchani"
title = "Jensen-Shannon vs Kullback-Leibler Divergence"
date = "2022-11-17T13:31:30-06:00"
description = ""
draft="true"
tags = [
    "knowledge-distillation",
]
categories = [
    "excerpt",
    "ml"
]
series = ["ML"]
+++

[Original post on Stack Overflow](https://stats.stackexchange.com/questions/117225/jensen-shannon-divergence-vs-kullback-leibler-divergence)

> I recently stumbled into a similar question.
> 
> To answer why an asymmetric divergence can be more favourable than a symmetric divergence, consider a scenario where you want to quantify the quality of a proposal distribution used in importance sampling (IS). If you are unfamiliar with IS, the key idea here is that to design an efficient IS scheme, your proposal distribution should have heavier tails than the target distribution.
> 
> Denote two distributions 𝐻=Normal(0,25) and 𝐿=Normal(0,1). Suppose you target 𝐻 with IS, using 𝐿 as the proposal distribution. To quantify the quality of your proposal distribution, you might compute the Jensen-Shannon (JS) divergence of 𝐿,𝐻, and the Kullback-Leibler (KS) divergence of 𝐿 from 𝐻 and obtain some values. Both values should give you some sense of how good your proposal distribution 𝐿 is. Nothing to see here yet. However, consider reversing the setup, i.e., target 𝐿 with IS using 𝐻 as the proposal distribution. Here, the JS divergence would be the same due to its symmetric property, while KL of 𝐻 from 𝐿 would be much lower. In short, we expected using 𝐻 to target 𝐿 to be OK, and 𝐿 to target 𝐻 is not OK. KL divergence aligns with our expectation; KL(𝐻||𝐿)>KL(𝐿||𝐻). JS divergence doesn't.
> 
> This asymmetric property aligns with our goal in that it can correctly, loosely speaking, account for the direction of discrepancy between two distributions.
> 
> Another factor to consider is that sometimes it can be significantly more computationally challenging to compute JS divergence than KS divergence.
>
> — <cite>user</cite>