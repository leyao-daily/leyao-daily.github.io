---
layout: post
title: Deep Learning - Day 8 - Training a Neural Network - Forward and Backward Propagation
categories: ['Deep Learning']
description: A comprehensive guide to understanding forward and backward propagation in neural networks.
keywords: Deep Learning, Neural Network, Forward Propagation, Backward Propagation, Python, Training, Optimization
---
# Day 8 - Training a Neural Network: Forward and Backward Propagation

Training a neural network involves two key steps: forward propagation and backward propagation. In this article, we will explore these concepts in detail, explaining how they are used to compute gradients and update weights in a neural network.

- [Forward Propagation](#forward-propagation)
- [Backward Propagation](#backward-propagation)
- [Gradient Descent](#gradient-descent)
- [Summary](#summary)

## Forward Propagation

Forward propagation is the process of computing the output of a neural network by passing input data through its layers. The input data is passed through a series of activation functions, and the resulting output is compared to the ground truth labels to compute the loss.

### Steps of Forward Propagation

1. Initialize input data and weights.
2. Multiply input data with weights and add biases.
3. Pass the result through an activation function.
4. Repeat steps 2 and 3 for each layer in the neural network.
5. Compute the loss using the output from the final layer and the ground truth labels.

## Backward Propagation

Backward propagation, or backpropagation, is the process of computing gradients for the weights and biases in a neural network using the chain rule of calculus. The gradients are used to update the weights and biases, allowing the model to learn and improve its performance.

### Steps of Backward Propagation

1. Compute the gradient of the loss function with respect to the output of the final layer.
2. Compute the gradient of the output of the final layer with respect to its pre-activation value.
3. Compute the gradients of the weights and biases in the final layer using the computed gradients.
4. Use the chain rule to compute the gradients for the previous layers, repeating steps 2 and 3 for each layer.
5. Update the weights and biases using the computed gradients and a learning rate.

## Gradient Descent

Gradient descent is an optimization algorithm that is commonly used to update the weights and biases in a neural network during training. It adjusts the model parameters iteratively to minimize the loss function.

There are several variants of gradient descent, including:

- Batch Gradient Descent: Computes gradients and updates weights using the entire dataset at once.
- Stochastic Gradient Descent: Computes gradients and updates weights using a single training example at a time.
- Mini-batch Gradient Descent: Computes gradients and updates weights using a small batch of training examples.

## Summary

In this article, we have covered the essential concepts of forward and backward propagation, the core mechanisms for training neural networks. Understanding these concepts is crucial for building and training deep learning models. In the next part of our series, we will explore advanced topics such as regularization, overfitting, and hyperparameter tuning. Stay tuned!
