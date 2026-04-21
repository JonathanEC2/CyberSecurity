2026-04-06 20:59
Tags: [[]]

## Machine Learning Defined

- Machine Learning is a subset of AI
- Cisco defines it as mathematical and statistical methods that enable machines to mimic intelligent human behavior by learning from data without being specifically programmed
- It can analyze huge sets of data sets, identify patterns, relationships, and anomalies

### Machine Learning Training Approaches 

**Supervised learning** - learns relationships between input and output data by providing it 'labeled data'
**Unsupervised learning** - given unlabeled data and allowed to discover data patterns and insights without explicit guidance or instruction (could be used for network anomaly detection)
**Semi-supervised learning** - blend of supervised and unsupervised
**Reinforcement learning** - data is accumulated from trial and error; data is not provided as the learning method

## Predictive AI

- Utilizes algorithms and modelling to analyze past and current data to forecast future events and behaviors
- Machine Learning is used to understand the data and predict what is likely to happen to occur in the future

## Generative AI

- Generative AI utilized patterns and relationships learned from past data to create new outputs such as text, images, audio, and video
- Supervised learning is typically used for training

# Generative AI Models

## Neural Network 

- Neural Networks are based on how the brain work. They contain artificial neurons called nodes which area arranged in a series of layers
- They have input and output layers with hidden layers in between
- The input layer receives data which the neural network needs to analyze
- Nodes are interconnected from one later to another
- Each connection between nodes has a weight that signifies relative importance
- If a node receives a high enough total value of weights from all its inputs then it fires and passes data on the the next layer
- The data transfers the data through the layers until producing output

## Deep Learning 

- Deep Learning is a type of Machine Learning based on Neural Network with at least 2 hidden layers

## Neural Network Training

- Backpropagation uses a mathematical function to iteratively fine tune the weights of connections until accurate output is consistently produces

### Unimodal and Multimodal Models

- Unimodal models take instruction from the same input type as their output  (Creating text from a text prompt)
- Multimodal models can take input from different sources and generate output in various forms (Creating and image from a text caption)
## Transformer Models

- Tracks relationships in sequential data. They learn what is appropriate to come next in sequences
-  They use a mathematical 'self-attention' technique to understand the importance of the different parts of the sequence and determine context
- They typically used massive data sets
- The transformer architecture is composed of **encoder** and **decoder** neural networks
- The encoder is concerned with input and is typically used for classification
- The decoder is used for output and is used to generate data, such as text articles or programming code
### Natural Language Processing

- NLP uses a broad range of rule-based methods and machine learning to enable computers to understand language and generate language as it is spoken and written
- Tasks include generating and identifying language, translation, text-to-speech and speech-to-text
-  Uses a comparatively small dataset

### Large Language Model

- LLLM uses a transformer based neural network built with a huge dataset
- They can handle almost any NLP task and are very good at generating humanlike text in response to instructions

## Generative Adversarial Networks

- Two deep learning models compete against each other 
- Generator learns to create new data such as text, images, audio, or video the resembles the training data set
- Discriminator learns to distinguish between the generated data and the real data
- The train each other so that generator produces data the can fool discriminator and discriminator becomes better at detecting false information

### GANs in Network Operations

GAN models can generate network traffic simulations

## Variable Auto Encoders

- Also use two neural networks to generate data
- An encoder and decoder work in tandem to generate output that is similar to the input


## References
