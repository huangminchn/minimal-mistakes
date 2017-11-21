---
title: "PP Team Project Checkpoint"
categories:
  - PP-Team
tags:
  - CNN
  - parellel
  - cuda
---

# Checkpoint

By far, we have already designed and implemented the pipeline for each type of layer in convolutional neural networks, including feedforward and backforward logic for convolutional layer, pooling layer (max-pooling, avg-pooling, and sum-pooling), fully-connected layer as well as input and output layer, a.k.a. The majority types of layers needed in CNN. The pipeline is runnable now for both feed-forward and backward process. Modularize the pipeline makes parallelizing over the entire training process easy because we can easily assign different parts of the pipeline into cuda blocks and cuda threads.

Our first design for parallelizing the training process is to parallelize the work across training samples, and we have already implemented the pipeline for that. However there still needs some minor changes to the shared weights calculation to be added. We don’t have enough time to run the experiment but we are confident that this will result in high speedup compared to the serialized version. For other progress, we have also implemented a python version of the CNN by pyTorch, a python library for neural networks to validate the correctness of our program. During the past two weeks, we also gathered a lot of training data for our project to do experiments on the speedup as well as validation test of the program correctness.

With respect to the goals and deliverables stated in our proposal, we believe that we will be able to produce all our deliverables. We have met our goal of ‘implement the sequential version of CNN’ and ‘gather training and test data’ and a part of the goal of ‘implement the parallel version of CNN on CUDA’. We need to adjust our plan a little bit and arrange the plan in detail by weeks. And the revised plan is shown in later section.

For the poster session, since it’s difficult for our project to show in live. We plan to show graphs of the memory footprint, and speedup graph of the project. We also plan to show how to use the library via some simple commands and configurations. We don’t have results at this time, but we will have them shortly.

For the issues that concern us the most, we are concerned about the synchronized updates to the weight matrices, and potential memory insufficiency for the training of the networks. We will discuss with the course staff if we can’t solve them in a good way.


# Schedule

| Week | Plan | Note |
|:--------|:-------:|--------:|
| Oct. 30   | Understand the CNN   | Proposal   |
| Nov. 6   | Implement the simplest sequential version of CNN on CUDA   |    |
|----
| Nov. 13   | Design the framework that is friendly to users   |    |
| Nov. 20   | Complement the framework for sequential CNN   | Checkpoint   |
|----
| Nov. 27   | Explore the performance boost from parallel over different layers (Ye); benchmark the sequential version (Min)   |    |
| Dec. 4   | Profile the new framework that parallel over layers and find optimization(Ye); explore the performance boost from parallel over inputs (Min)   |    |
|----
| Dec. 12   | Prepare for the poster session (Ye); apply all optimizations found by Ye (Min)   | Competition & Final Report   |
|=====
{: rules="groups"}