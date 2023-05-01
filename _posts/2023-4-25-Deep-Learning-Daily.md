---
layout: post
title: Deep Learning - Day 5 - Building a Basic Neural Network with TensorFlow and Keras
categories: ['Deep Learning']
description: A step-by-step guide to building, training, and evaluating a basic neural network using TensorFlow and Keras.
keywords: Deep Learning, Python, TensorFlow, Keras, Neural Network
---
# Day 5 - Building a Basic Neural Network with TensorFlow and Keras

- [Step 1: Import Libraries and Load Data](#step-1-import-libraries-and-load-data)
- [Step 2: Preprocess Data](#step-2-preprocess-data)
- [Step 3: Define the Neural Network Model](#step-3-define-the-neural-network-model)
- [Step 4: Compile the Model](#step-4-compile-the-model)
- [Step 5: Train the Model](#step-5-train-the-model)
- [Step 6: Evaluate the Model](#step-6-evaluate-the-model)
- [Step 7: Visualize Training History](#step-7-visualize-training-history)

In this post, we will build a basic neural network using TensorFlow and Keras. We will use the popular MNIST dataset of handwritten digits to train our model for digit recognition.

## Step 1: Import Libraries and Load Data

First, let's import the necessary libraries and load the MNIST dataset.

```python
import numpy as np
import matplotlib.pyplot as plt
from tensorflow.keras.datasets import mnist
from tensorflow.keras.utils import to_categorical
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

(x_train, y_train), (x_test, y_test) = mnist.load_data()
```

## Step 2: Preprocess Data

Next, we preprocess the data by reshaping the images into vectors, normalizing the pixel values, and converting the labels into one-hot encoding.

```python
x_train = x_train.reshape(-1, 784).astype('float32') / 255
x_test = x_test.reshape(-1, 784).astype('float32') / 255

y_train = to_categorical(y_train, num_classes=10)
y_test = to_categorical(y_test, num_classes=10)
```

## Step 3: Define the Neural Network Model

Now, we define our neural network model using Keras' `Sequential` API. We create a simple feedforward neural network with one hidden layer and an output layer.

```python
model = Sequential([
    Dense(128, activation='relu', input_shape=(784,)),
    Dense(10, activation='softmax')
])
```

## Step 4: Compile the Model

Before training the model, we need to compile it by specifying the optimizer, loss function, and evaluation metrics.

```python
model.compile(optimizer='adam',
              loss='categorical_crossentropy',
              metrics=['accuracy'])
```

## Step 5: Train the Model

We are now ready to train our neural network using the `fit` method. We specify the number of epochs (iterations over the entire dataset) and the batch size (number of samples used for a single update of the model weights).

```python
history = model.fit(x_train, y_train, epochs=10, batch_size=32, validation_split=0.1)
```

## Step 6: Evaluate the Model

After training the model, we evaluate its performance on the test set using the `evaluate` method.

```python
test_loss, test_accuracy = model.evaluate(x_test, y_test)
print(f'Test Loss: {test_loss:.4f}, Test Accuracy: {test_accuracy:.4f}')
```

## Step 7: Visualize Training History

Finally, we can visualize the training history to observe the model's performance over time.

```python
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.plot(history.history['accuracy'], label='Training Accuracy')
plt.plot(history.history['val_accuracy'], label='Validation Accuracy')
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.legend()

plt.subplot(1, 2, 2)
plt.plot(history.history['loss'], label='Training Loss')
plt.plot(history.history['val_loss'], label='Validation Loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.legend()

plt.show()
```



With this basic neural network, we can achieve a relatively high test accuracy. You can further experiment with different architectures, optimizers, and hyperparameters to improve the performance of the model. 

That's it for Day 5! We have successfully built, trained, and evaluated a basic neural network using TensorFlow and Keras. In the next post, we will dive deeper into more advanced topics in deep learning, such as convolutional neural networks and recurrent neural networks. Stay tuned!
