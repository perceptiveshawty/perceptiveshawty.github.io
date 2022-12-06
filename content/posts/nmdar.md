+++
author = "Sachin Chanchani"
title = "NMDA receptors are nonlinear activation functions"
date = "2022-11-17T10:44:39-06:00"
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

The hippocampus is a region of the brain thought to be essential for consolidation and retrieval of long term episodic and spatial memory. Studying this part of the brain led to the discovery of place cells, which (kind of) resemble the function of nonlinear activations in neural networks.

Place cells act collectively to form place fields [think feature maps in convolutional neural networks]. Their firing-patterns correlate strongly with environmental stimuli like familiar visual, olfactory, and vestibular cues. In one [experiment](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6672960/) with rats in a maze, place cells were monitored and each cell gave rise to its own mode in recorded action potentials. The modes were distinguished only by the rat's position in the maze, which suggests a connection between these cells and the navigation task.

{{< figure src="/img/nmdar2.png" caption="Current-voltage dynamics of the NMDAR IV with varying levels of magnesium ions. We can observe an increase in this blockade of ions at resting potential correlates with smaller activations in the negative direction. It closely resembles the GELU activation function, which leaks a small negative gradient for small negative inputs." width="35%" >}}

Crucial to the function of these cells (and consequently, the formation of long-term memories) are the self-regulating dynamics of the NMDA receptor and its blockade of Mg<sup>2+</sup> ions at resting potential. An influx of cations through the receptor is thought to be a primary mechanism for cellular learning, since Ca<sup>2+</sup> and Na<sup>+</sup> go on to bond with and influence the behavior of a number of essential proteins. However, this influx is activity dependent:

1. Unblocking the ion channel requires depolarizing the neuron enough to dislodge the Mg<sup>2+</sup> ions, which typically happens thru ligand binding 

2. Once the Mg<sup>2+</sup> ions are dislodged, the influx of ions is dependent on the voltage across the cellular membrane.

In the context of neural networks, a negative gradient results from seeing a data distirbution that does not match the hypothesis represented by the network at that state. In most cases, one sample should not warrant a huge parameter adjustment that overwrites what was previously learned about the population distribution. It is more likely that the sample is noisy - with the GELU activation (and other activations that suppress negative gradients), a network can avoid committing this new information to the hypothesis it represents. Analagously, increased Mg<sup>2+</sup> concentration in the brain (corresponding the the amplitude of the "bump" in the GELU activation) leads to enhanced long-term memory formation, by suppressing activations until certain conditions are met. 

{{< figure src="/img/nmdar1.png" caption="The proposed NMDAR-like activation function. Authors find that the degree of nonlinearity correlates with the long-term memory purportedly encoded in the models feed-forward layers." width="60%" >}}

The similarity between the graphs is easy to point out, and in this paper the authors propose an NMDAR-like activation function derived from the curve in Figure 1. They evaluate its impact by substituting it for the GELU activation in the transformer architecture, and design a 2D navigation task to assess working and long-term memory. Their results show that place cell representations emerge in the MLP layers of the transformer, and the reliance on "long-term memory" can be modulated by changing the nonlinearity of the NMDAR activation. Zero initial Mg<sup>2+</sup> concentration represents a purely linear activation, and the limit as Mg<sup>2+</sup> concentration → ∞ represents a ReLU activation.

It's interesting also to note how they are operationalizing "working" vs "reference" (long-term) memory in the transformer: self-attention layers corresponding to the former, and FFNs to the latter. It would be interesting to see how analgous these layers are to the episodic buffer and long-term memory store in [Baddeley's working memory model](https://en.wikipedia.org/wiki/Baddeley%27s_model_of_working_memory).








