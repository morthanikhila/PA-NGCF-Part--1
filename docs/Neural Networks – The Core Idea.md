# Neural Networks – The Core Foundation

## 1. What is a Neural Network?
A **Neural Network (NN)** is a machine learning model designed to learn and recognize patterns from data.  
It works by taking input, processing it through multiple layers of interconnected units (neurons), and producing an output.

Neural Network = Input → Learn patterns → Output  
Example: Given an image, the network learns to output "cat".

---

## 2. Structure of a Neural Network

A neural network consists of **layers**, and each layer contains several **neurons**.

| Layer Type     | Purpose |
|----------------|---------|
| Input Layer    | Receives raw data (numeric form) |
| Hidden Layers  | Learn and extract patterns from data |
| Output Layer   | Produces final prediction/decision |

Each neuron performs a weighted computation on inputs:
neuron_output = activation( Σ(input × weight) + bias )
---


---

## 3. How Neural Networks Learn

The learning process involves three main steps:

### (a) Forward Pass
Data flows through the network from input → hidden layers → output.  
The network produces a prediction.

### (b) Loss Calculation
The prediction is compared to the target (ground truth) using a **loss function**.  
Examples of loss functions:
- Mean Squared Error (Regression)
- Cross-Entropy Loss (Classification)

### (c) Backward Pass (Backpropagation)
Using **gradient descent**, the network updates the weights to reduce loss.  
Goal: adjust weights so predictions improve over time.

---

## 4. Neural Networks in Recommendation Systems

Recommender systems aim to learn:
- User preferences  
- Item characteristics  
- Hidden relationships between users and items

Neural networks help capture patterns like:
- Users with similar taste
- Items liked by similar groups of users
- Item similarity without needing explicit tags or categories
- Personalized preferences based on interaction history

Example insight NN can learn:
If many people who like "Avengers" also like "Iron Man", this relationship is captured automatically.

---

## 5. Limitation of Standard Neural Networks

Traditional neural networks expect **fixed-size vector data** (tables, images, numbers).  
However, recommender system data forms **relationships**, not fixed row-column data.

Example relations:
User A → Item 1
User B → Item 1
User A → Item 2
