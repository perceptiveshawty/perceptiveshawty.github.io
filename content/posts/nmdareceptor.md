+++
author = "Sachin Chanchani"
title = "NMDA-receptors are nonlinear activation functions"
date = "2022-11-17T17:13:06-06:00"
description = "Hippocampus analogy for transformers"
tags = [
    "knowledge-distillation",
]
categories = [
    "paper",
    "nlp"
]
series = ["NLP"]
+++

[Original Paper](https://openreview.net/forum?id=0z_cXcu1N6o)

The hippocampus is an area of the brain that is essential for consolidation and retrieval of long term memories, as well as spatial memory used in navigation tasks. We've been studying this organ in animals and humans for decades, and it has led to the discovery of a kind of neuron that closely resembles neural network activations in its function: the place cell. 

Place cells act collectively to form place fields, not unlike feature maps you can extract from intermediate stages of convolutional neural networks. Their firing-patterns correlate strongly with environmental stimuli like visual, olfactory, and vestibular stimuli, and in one experiment with rats in a maze where place cells were recorded, each place cell corresponded to a mode in recorded action potentials that varied with their place in the maze. 

Crucial to the function of these cells (and consequently, the formation of long-term memories) are the self-regulating dynamics of the NMDA receptor and its blockade of Mg<sup>2+</sup> ions at equilibirum. An influx of positive cations through the receptor is thought to be a primary mechanism for cellular learning, since Ca<sup>2+<sup> and Na<sup>+<sup> go on to bond with and influence the behavior of a number of essential amino acids. 

{{< figure src="/img/nmdar2.png" caption="Current-voltage dynamics of the NMDAR IV with varying levels of magnesium ions. We can observe an increase in this blockade of ions correlates with smaller activations in the negative direction. It closely resembles the GELU activation function, which leaks a small negative gradient for negative inputs." width="100%" >}}

Activation of NMDA receptors requires two things: 

1. Ungating the ion channel requires depolarizing the neuron enough to dislodge the Mg<sup>2+<sup> ions, which typically happens thru ligand binding 

2. A large enough voltage across the cellular membrane 

The neural network analogy to this phenomena is the **nonlinear** activation function. The similarity between their curves is easy to point out, and in this paper the authors propose an NMDAR-like activation function derived from the curve in Figure 1. They evaluate its impact by substituting it for the GELU activation in the transformer architecture, and design a 2D navigation task to assess working and long-term memory. Their results show that place cell representations emerge in the FFNs, the long-term memory can be modulated by changing the nonlinearity of the NMDAR activation, and that no place cells emerge in self-attention layers. 


{{< figure src="/img/nmdar1.png" caption="The proposed NMDAR-like activation function. Authors find that the degree of nonlinearity correlates with the long-term memory purportedly encoded in the models feed-forward layers." width="100%" >}}







