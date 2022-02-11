---
layout: post
title:  "Neural Networks, Manifolds, and Topology"
description: "Understand what a neural network is really doing."
categories: learning
read_minutes: 10
is_project_page: false
show_downloads: false
linux_compatible: false
---

[link]
(https://colah.github.io/posts/2014-03-NN-Manifolds-Topology/)

# **Table of Contents**

1. Handling Missing Values
2. Scaling and Normalization
3. Parsing Dates
4. Character Encodings
5. Inconsistent Data Entry

* * *

### 문단 복사 붙여넣기용
<p>　</p>

> We can create visualizations to completely understand the behavior and training of low-dimensional deep neural networks.

### **A Simple Example**

the simplest possible class of neural network, one with only an input layer and an output layer. Such a network simply tries to separate the two classes of data by dividing them with a line.

That sort of network isn’t very interesting. Modern neural networks generally have multiple layers between their input and output, called “hidden” layers. At the very least, they have one. It separates the data with a more complicated curve than a line.

With each layer, the network transforms the data, creating a new representation. 

We learn to understand networks by looking at the representation corresponding to each layer. This gives us a discrete list of representations.

When we get to the final representation, the network will just draw a line through the data (or, in higher dimensions, a hyperplane).

In the previous visualization, we looked at the data in its “raw” representation. You can think of that as us looking at the input layer. Now we will look at it after it is transformed by the first layer. You can think of this as us looking at the hidden layer.

The hidden layer learns a representation so that the data is linearly separable.

### **Continuous Visualization of Layers**

There are a variety of different kinds of layers used in neural networks.
ex)A tanh layer tanh(Wx+b) consists of:

1. A linear transformation by the “weight” matrix W
2. A translation by the vector b
3. Point-wise application of tanh.

We can apply this technique to understand more complicated networks. While the spirals are originally entangled, by the end they are linearly separable. On the other hand, the following network, also using multiple layers, fails to classify two spirals that are more entangled.

It is worth explicitly noting here that these tasks are only somewhat challenging because we are using low-dimensional neural networks. If we were using wider networks, all this would be quite easy.

### **Topology of tanh Layers**

Each layer stretches and squishes space, but it never cuts, breaks, or folds it. Intuitively, we can see that it preserves topological properties. For example, a set will be connected afterwards if it was before (and vice versa).

Transformations like this, which don’t affect [topology], are called [homeomorphisms]. Formally, they are bijections that are continuous functions both ways.

[biejction]: 일대일 대응(https://en.wikipedia.org/wiki/Bijection)
[topology]: 위상 수학 (https://en.wikipedia.org/wiki/Topology)
[homeomorphisms]:  유사형 = 연결 상태가 같음. (https://en.wikipedia.org/wiki/Homeomorphism)
  - bijections that are invertible continuous functions both ways.
  - An often-repeated mathematical joke is that topologists cannot tell the difference between a coffee cup and a donut, since a sufficiently pliable donut could be reshaped to the form of a coffee cup by creating a dimple and progressively enlarging it, while preserving the donut hole in the cup's handle.
  - 지하철 노선도에도 위상수학이 숨어 있다고 한다. 어떤 도형을 자르거나 붙이지 않으며 서로 다른 두 점이 중복되지 않도록 도형을 늘이거나 줄이고 구부려서 얻은 도형을 처음 도형과 `연결 상태가 같은 도형`이라고 부루는데, 이러한 성질을 연구하는 수학의 분야가 위상수학, 위상기하학이다.

**Theorem:** Layers with N inputs and N outputs are homeomorphisms, if the weight matrix, W, is [non-singular]. (Though one needs to be careful about domain and range.)

[non-singular]: square one whose determinant is not zero

Proof: Let’s consider this step by step:

1. Let’s assume W has a non-zero determinant. Then it is a bijective linear function with a linear inverse. Linear functions are continuous. So, multiplying by W is a homeomorphism.
2. Translations are homeomorphisms
3. tanh (and sigmoid and softplus but not ReLU) are continuous functions with continuous inverses. They are bijections if we are careful about the domain and range we consider. Applying them pointwise is a homeomorphism
Thus, if W has a non-zero determinant, our layer is a homeomorphism. ■

This result continues to hold if we compose arbitrarily many of these layers together.

### **Topology and Classification**

Classification with a sigmoid unit or a softmax layer is equivalent to trying to find a hyperplane (or in this case a line) that separates A and B in the final represenation.

To get a better sense of what’s going on, let’s consider an even simpler dataset that’s 1-dimensional:
  - A=[−1/3,1/3]
  - B=[−1,−2/3]∪[2/3,1]
 Without using a layer of two or more hidden units, we can’t classify this dataset.
 = can’t be separated without using n+1 dimensions, namely a 2nd dimension.
But if we use one with two units, we learn to represent the data as a nice curve that allows us to separate the classes with a line

### **The Manifold Hypothesis**

Is this relevant to real world data sets, like image data? If you take the manifold hypothesis really seriously, I think it bears consideration.

**[manifold] hypothesis**: natural data forms lower-dimensional manifolds in its embedding space. There are both theoretical and experimental reasons to believe this to be true.
If you believe this, then the task of a classification algorithm is fundamentally to separate a bunch of tangled manifolds.

[manifold]: (https://en.wikipedia.org/wiki/Manifold)
  - n-dimensional manifold, or n-manifold for short, is a topological space with the property that each point has a neighborhood that is homeomorphic to an open subset of n-dimensional Euclidean space.
  - One-dimensional manifolds include lines and circles, but not figure eights. Two-dimensional manifolds are also called surfaces. Examples include the plane, the sphere, and the torus, and also the Klein bottle and real projective plane.

In the previous examples, one class completely surrounded another. However, it doesn’t seem very likely that the dog image manifold is completely surrounded by the cat image manifold. But there are other, more plausible topological situations that could still pose an issue, as we will see in the next section.

### **Links And Homotopy**

If a neural network using layers with only 3 units can classify it, then it is an unlink. (Question: Can all unlinks be classified by a network with only 3 units, theoretically?)

From this knot perspective, our continuous visualization of the representations produced by a neural network isn’t just a nice animation, **it’s a procedure for untangling links**. In topology, we would call it an [ambient isotopy] between the original link and the separated ones.

[ambient isotopy]: = h-isotopy (https://en.wikipedia.org/wiki/Ambient_isotopy)
  - in knot theory, one considers two knots the same if one can distort one knot into the other without breaking it. Such a distortion is an example of an ambient isotopy.

**Theorem:** There is an ambient isotopy between the input and a network layer’s representation if:
1. W isn’t singular, 
2. we are willing to permute the neurons in the hidden layer
3. there is more than 1 hidden unit.

Proof: Again, we consider each stage of the network individually:

1. The hardest part is the linear transformation. In order for this to be possible, we need W to have a positive determinant. Our premise is that it isn’t zero, and we can flip the sign if it is negative by switching two of the hidden neurons, and so we can guarantee the determinant is positive. The space of positive determinant matrices is path-connected, so there exists p:[0,1]→GLn(R)5 such that p(0)=Id and p(1)=W. We can continually transition from the identity function to the W transformation with the function x→p(t)x, multiplying x at each point in time t by the continuously transitioning matrix p(t).
2. We can continually transition from the identity function to the b translation with the function x→x+tb.
3. We can continually transition from the identity function to the pointwise use of σ with the function: x→(1−t)x+tσ(x). ■

Links and knots are 1-dimensional manifolds, but we need 4 dimensions to be able to untangle all of them. Similarly, one can need yet higher dimensional space to be able to unknot n-dimensional manifolds.
All n-dimensional manifolds can be untangled in 2n+2 dimensions. This result is mentioned in [Wikipedia’s subsection on Isotopy versions](https://en.wikipedia.org/wiki/Whitney_embedding_theorem#Isotopy_versions).

### **The Easy Way Out**
The natural thing for a neural net to do, the very easy route, is to try and pull the manifolds apart naively and stretch the parts that are tangled as thin as possible. 

It would present itself as very high derivatives on the regions it is trying to stretch, and sharp near-discontinuities. We know these things happen.
Contractive penalties, penalizing the derivatives of the layers at data points, are the natural way to fight this.

Since these sort of local minima are absolutely useless from the perspective of trying to solve topological problems, topological problems may provide a nice motivation to explore fighting these issues.

On the other hand, if we only care about achieving good classification results, it seems like we might not care. If a tiny bit of the data manifold is snagged on another manifold, is that a problem for us? It seems like we should be able to get arbitrarily good classification results despite this issue.

(My intuition is that trying to cheat the problem like this is a bad idea: it’s hard to imagine that it won’t be a dead end. In particular, in an optimization problem where local minima are a big problem, picking an architecture that can’t genuinely solve the problem seems like a recipe for bad performance.)

### **Better Layers for Manipulating Manifolds?**

Perhaps it might make sense to have a very different kind of layer that we can use in composition with more traditional ones?

The thing that feels natural to me is to learn a vector field with the direction we want to shift the manifold. One could learn the vector field at fixed points (just take some fixed points from the training set to use as anchors) and interpolate in some manner.

[interpolation]: 보간법 (https://www.investopedia.com/terms/i/interpolation.asp)
  - statistical method by which related known values are used to estimate an unknown price or potential yield of a security.

### **K-Nearest Neighbor Layers**
I’ve also begun to think that linear separability may be a huge, and possibly unreasonable, amount to demand of a neural network.

Possible alternative: k-nearest neighbors (k-NN). However, k-NN’s success is greatly dependent on the representation, so one needs a good representation before k-NN can work well.

Still, I really aesthetically like this approach, because it seems like what we’re “asking” the network to do is much more reasonable. We want points of the same manifold to be closer than points of others, as opposed to the manifolds being separable by a hyperplane.
This should correspond to inflating the space between manifolds for different categories and contracting the individual manifolds. It feels like simplification.

### **Conclusion**
Topological properties of data, such as links, may make it impossible to linearly separate classes using low-dimensional networks, regardless of depth. Even in cases where it is technically possible, such as spirals, it can be very challenging to do so.

To accurately classify data with neural networks, wide layers are sometimes necessary. Further, traditional neural network layers do not seem to be very good at representing important manipulations of manifolds; even if we were to cleverly set weights by hand, it would be challenging to compactly represent the transformations we want. New layers, specifically motivated by the manifold perspective of machine learning, may be useful supplements.

(This is a developing research project. It’s posted as an experiment in doing research openly. I would be delighted to have your feedback on these ideas: you can comment inline or at the end. For typos, technical errors, or clarifications you would like to see added, you are encouraged to make a pull request on github.)