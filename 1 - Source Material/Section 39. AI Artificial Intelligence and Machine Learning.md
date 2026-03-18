<mark style="background: #D2B3FFA6;"></mark>2026-03-17 16:07
Tags: [[]]

# AI Artificial Intelligence and Machine Learning Overview

## Automation and its Limitations

Standard automation tools like ansible and terraform are very good at deploying straightforward predefined rule based configuration. For example, pushing an enterprise's QOS policy to all its network devices
However they are not so good at more complex dynamic dynamic tasks such as learning normal traffic patterns over an enterprise network, recognizing anomalies, and automatically taking corrective action

## Traditional Security Systems and its Limitations

Traditional IPS use signatures to inspect packets, looking for traffic patterns which match known attacks. This does not secure against new threats or anomalies that do not match those patterns

## AI Defined

Cisco defines AI as the simulation of humanlike behavior by computers

## Machine Learning Defined

- Machine Learning is a subset of AI
- Cisco defines it as mathematical and statistical methods that enable machines to mimic intelligent human behavior by learning from data without being specifically programmed
- It can analyze huge sets of data sets, identify patterns, relationships, and anomalies

### Machine Learning Training Approaches 

Supervised learning - learns relationships between input and output data by providing it 'labeled data'
Unsupervised learning - given unlabeled data and allowed to discover data patterns and insights without explicit guidance or instruction (could be used for network anomaly detection)
Semi-supervised learning - blend of supervised and unsupervised
Reinforcement learning - data is accumulated from trial and error; data is not provided as the learning method

## AI and ML in Network Operations

- Machine Learning can analyze huge sets of network related data, normal network patters (baselining) and detect anomalies
- AI functions can then report on the anomalies and automatically take action on them, predict future, patterns and issues such as upcoming congestion, and recommend optimum settings

## Predictive AI

- Utilizes algorithms and modelling to analyze past and current data to forecast future events and behaviors
- Machine Learning is used to understand the data and predict what is likely to happen to occur in the future

### Predictive AI in Network Operations

AI can analyze past and current traffic patterns and anomalies, performance statistics, help tickets, maintenance history and environmental factors in order to forecast problems such as security issues, congestion, and hardware failures

## Generative AI

- Generative AI utilized patterns and relationships learned from past data to create new outputs such as text, images, audio, and video
- Supervised learning is typically used for training

### Generative AI in Network Operations

- Generative AI can be used to generate network traffic pattern simulations. This can help identify potential issues under different conditions and help plan for future upgrades without affecting the real network
- It can also create optimized network settings and configurations based on current conditions, for planned upgrade, or as a solution for an issue

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
- For example, in image classification, lower layers may identify edges in an image, while higher layers classify it as an animal or vehicle

## Neural Network Training

- If the wrong output is produced, it must be corrected
- Backpropagation is used to signal back through the network that the weights have to be changed
- Backpropagation uses a mathematical function to iteratively fine tune the weights of connections until accurate output is consistently produces

## Generative AI Models

Transformer Models
Generative Adversarial Networks (GANs)
Variation Auto Encoder (VAEs)

### Unimodal and Multimodal Models

- Transformers typically work with text
- GANs and VAEs typically work with visual data
- They are not mutually exclusive
- Unimodal models take instruction from the same input type as their output  (Creating text from a text prompt)
- Multimodal models can take input from different sources and generate output in various forms (Creating and image from a text caption)\

## Transformer Models

- Tracks relationships in sequential data. They learn what is appropriate to come next in sequences
- They use a mathematical 'self-attention' technique to understand the importance of the different parts of the sequence and determine context
- They typically used massive data sets
- They can analyze data unsupervised and with parallel processing so they are fast to implement

- The transformer architecture is composed of encoder and decoder neural networks
- The encoder is concerned with input and is typically used for classification
- The decoder is used for output and is used to generate data, such as text articles or programming code
- They can be used together for tasks such as text translation
- Used in Large Language Models

### Natural Language Processing

- NLP uses a broad range of rule-based methods and machine learning to enable computers to understand language and generate language as it is spoken and written
- Tasks include generating and identifying language, translation, text-to-speech and speech-to-text
- Uses a comparatively small dataset and a method which is relevant to their goal

### Large Language Model

- Also performs complex language processing tasks
- LLLM uses a transformer based neural network built with a huge dataset
- They can handle almost any NLP task and are very good at generating humanlike text in response to instructions
- Used in chatbots, text summarization, translation

### Generative Pre-Trained Transformers (GPT)

GTPs are Transformer based LLM
GPT uses a decoder to generate text from a prompt

## Generative Adversarial Networks

- With GANs two deep learning models compete against each other, the generator and discriminator
- The generator learns to create new data such as text, images, audio, or video the resembles the training data set
- The discriminator learns to distinguish between the generated data and the real data
- Discriminator will typically easily identify early efforts as fake and tell the generator to retry
- As training progresses, the generator will produce data that can fool the discriminator and humans. Discriminator will also improve with training
- GANs are often used to create visual data

### GANs in Network Operations

- GAN models can generate network traffic simulations
- Generator creates network traffic simulations
- With training the generator learns to create more realistic simulations and the discriminator learns to detect if the traffic patterns are fake
- GANs are good at creating network diagrams
## Variable Auto Encoders

- Also use two neural networks to generate data
- An encoder and decoder work in tandem to generate output that is similar to the input
- Decoder generates content which is optimized for the important information, reducing less desired characteristics

### VAEs In Network Operations

- VAEs are good at cleaning noise from images and finding anomalies
- GANs can also be used to detect network anomalies and security threats, as well as generating traffic

# Retrieval-Augmented Generation

## LLM Hallucination

LLMs are susceptible to hallucination where they generate incorrect output data
LLMs are very good out outputting natural text, but can fall short with technical knowledge of a topic or up to date information is required

## Ways to Reduce Hallucination

- Build a new model from scratch: Make an LLM with a relative data set; Expensive
- Fine tuning: Load additional relevant data to an existing LLM and use techniques such as backpropagation to finetune it; Not as expensive but still costly and time consuming

## Retrieval-Augmented Generation (RAG)

RAG enhances the accuracy and currentness of an existing LLM by looking up an **external database**
It is relatively easy to implement with public tools and knowledge bases available

## How RAG Works

### Creating the Database

- During preprocessing the knowledgebase is split into tokens and chunks and converted to a machine readable numeric 'vector'
- An embedding model creates a vector database optimized for search and retrieval
- In the background the embedding model continuously updates the vector database as the knowledgebase is updated
### User Queries

- When a user enters a query the Embedding Model converts it into numeric format which is compared to the vector database
- Matches are retrieved and sent to the LLM
- The LLM combines the retrieved  entries with its own response to create the output for the user

![[attachments/Pasted image 20260317181315.png]]

## RAG usage in Network Operation

- Configuration generation
- Troubleshooting
- Up-to-date documentation generation
- Predictive maintenance

# Cisco AIOps Product

Cisco has a suite of products which fall under the AIOps umbrella:
- Cisco Network Analytics
- Cisco Catalyst Center
- Cisco Meraki
- Cisco Nexus Dashboard
- Cisco AppDynamics
- Cisco ThousandEyes

Many of the software products have overlapping ML and AI capabilities, they all support:
- Traffic analytics
- Anomaly detections
- Root cause analysis

There are multiple AI products with their own separate internal teams at Cisco
This is because of: 
Separate products for separate use cases such as provision and monitoring (Cisco Nexus Dashboard) or monitoring of internet based applications (Cisco ThousandEye)

## Cisco Catalyst AI Features

Network traffic baselining and anomaly detection
Network traffic benchmark comparison with other networks
Proactive insights for pattern and trend identification

## Cisco Meraki AI Features

Meraki Wi-Fi network visualization, management and monitoring with wireless assurance
Meraki Wi-Fi self-optimization with visibility, Auto RF selects the best channel and power level for APs

## Cisco Nexus Dashboard

Designed for automated provisioning, monitoring, anomaly detection and capacity planning of data centers with NX-OS Nexus and MDS switches.
It can be installed as a hardware appliance or virtual machine on-premises, or as cloud based SaaS

## Cisco App Dynamics 

Monitors applications and their infrastructure
Agents on the application servers report their statistics to the AppDynamics controller

## Cisco ThousandEye

ThousandEyes is a cloud managed monitoring and troubleshooting platform which is designed for organizations with complex distribute networks and applications on cloud or across the internet
It monitors internal and external (ISP and cloud provider) network availability and performance for applications.
It helps identify the root cause of application performance problems
Detects Anomalies and DDoS and DNS based attacks

### Cisco ThousandEye Agents

- Enterprise agents operate within the enterprise infrastructure.
- Endpoint agents are installed on end user machines.
- Cloud agents are managed by ThousandEyes and are distributed throughout ISPs and cloud providers. They provide inbound remote monitoring of the enterprise apps and infrastructure.

## Cisco Network Analytics

- It is security software which analyzes network traffic to create a baseline of normal network behavior
- Machine Learning and advanced analytics identifies anomalies and threats and responds in real- time (threats include Command-and-Control (C&C) attacks, ransomware, DDoS, unknown malware and insider threats)
- Machine Learning and advanced analytics identifies anomalies and threats and responds in real- time
## References
