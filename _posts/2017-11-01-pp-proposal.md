---
title: "PP Team Project Proposal"
categories:
  - PP-Team
tags:
  - CNN
  - parellel
  - cuda
---

# Summary

We are going to implement and design the domain-specific language for the parallel version of the deep neural network (DNN) on CUDA so that users can use this language to define their own structure of the DNNs. We focus our application mainly on the convolutional networks that aim to solve computer vision related problems.

Deep neural networks normally take very long time to train, and require large computation and memory overhead. And parallelizing the computation could be of great help to accelerate the training phase and leads to feasibility of more complex network structures. Specifically, we will mainly explore the parallelism on convolutional networks that uses expensive convolutional matrix multiplication to form training features. 
For convolutional neural networks, there are several kinds of the layers to represent features:
1. Convolutional layers: 
Convolutional layers apply a convolution operation to the input, passing the result to the next layer. And commonly convolutional layers would share weights, referred to as filters or weights banks, which reduces memory footprint and improves performance.
2. Pooling layers
Pooling layers are used to combine the outputs of a group of cells from previous layer into a single value. For example, max pooling uses the maximum value from each of a cluster of neurons at the prior layer. Another example is average pooling, which uses the average value from each of a cluster of neurons at the prior layer.
3. Fully connected layers
Fully connected layers connect every neuron in one layer to every neuron in another layer. It is in principle the same as the traditional multi-layer perceptron neural network
There are also various settings of the neural networks, such as using different loss functions, using different activation functions, etc. We want to have a general convolutional neural networks that let users define which types the layers are and the parameters of each layer by using our domain-specific language.

Most important of all, the computation convolutional neural network can benefit greatly from parallelism. Convolutional neural network is computation intensive, but by using shared weights, parallelizing over images or parameters, and trade atomicity with parallelism, large speedup can be expected via parallelism. 

# The Challenge
The problem is challenging and might be difficult to parallelize for the following reasons:
1. Training data is huge for computer vision problems, which are very typical applications of the convolutional neural networks. So parallelism and computation efficiency are very important to achieve a relatively good performance.
2. Intensive matrix multiplication is required to train the neural network, therefore finding optimizations to do the matrix multiplication is important for this problem.
3. For the back propagation phase to train the model, multiple threads may try to update some weights at the same time. So tradeoff between time and absolute correctness is important and worth thinking in this problem.
4. Barriers are required for each iteration, which implicitly add dependency of the threads across different thread blocks.
We hope to learn how to do tradeoffs between parallelism and absolute correctness in real-world applications, such as training convolutional networks in this project. And we also expect to learn different techniques for parallelism in this application.
As for the workload, the dependencies are across different training iterations, and are within updates of the same weights. The memory access pattern would be of spatial locality. For convolutional matrix multiplication, it only requires a group of grids with locality, so it is for the pooling layer. 
As for the constraints, as we’ve mentioned, updates to the shared weights limit parallelism, and input samples are trained batch by batch, therefore making the performance different from stochastic gradient descent, and we need to further investigate into this.

# Resources.
We will use provided GHC GPU machines for the CUDA code, and we are managing to find starter code for serialized version of the configurable convolutional neural networks. If there isn’t any, we will have to implement our own version of serialized configurable CNNs from scratch. We also need to investigate into optimizations of the parallelism of neural networks and matrix multiplication, and we are working on it.

# Platform choice.
We believe CUDA is a good choice because we can utilize the thread blocks and shared/global memory of it, and the scales in CUDA make it easier to divide the problems in CNN. It makes sense for the workload because large number of threads in CUDA make it possible for let us parallel over training samples efficiently. We also choose c++ as the supporting language because it is compatible with CUDA.



* Lists within lists do not break the ordered list numbering order
* Your list styles go deep enough.

### Ordered -- Unordered -- Ordered

1. ordered item
2. ordered item 
  * **unordered**
  * **unordered** 
    1. ordered item
    2. ordered item
3. ordered item
4. ordered item

### Ordered -- Unordered -- Unordered

1. ordered item
2. ordered item 
  * **unordered**
  * **unordered** 
    * unordered item
    * unordered item
3. ordered item
4. ordered item

### Unordered -- Ordered -- Unordered

* unordered item
* unordered item 
  1. ordered
  2. ordered 
    * unordered item
    * unordered item
* unordered item
* unordered item

### Unordered -- Unordered -- Ordered

* unordered item
* unordered item 
  * unordered
  * unordered 
    1. **ordered item**
    2. **ordered item**
* unordered item
* unordered item