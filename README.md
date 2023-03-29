# Project documentation



## **Flame basics**

Stanisław Łenyk, Michał Misiak,
Mateusz Słuszniak, Jerzy Wilczek

2023, Thursday 11:20



## 1. Introduction ##
The vision of **Flame** is to democratize federated learning (FL).

**Flame** is a framework for creating democratized environments for federated learning.

**Federated learning** (also known as collaborative learning) is a machine learning technique that trains an algorithm across multiple decentralized edge devices or servers holding local data samples, without exchanging them. This approach stands in contrast to traditional centralized machine learning techniques where all the local datasets are uploaded to one server, as well as to more classical decentralized approaches which often assume that local data samples are identically distributed.

Federated learning enables multiple actors to build a common, robust machine learning model without sharing data, thus allowing to address critical issues such as data privacy, data security, data access rights and access to heterogeneous data. Its applications are spread over a number of industries including defense, telecommunications, IoT, and pharmaceutics. A major open question at the moment is how inferior models learned through federated data are relative to ones where the data are pooled. Another open question concerns the trustworthiness of the edge devices and the impact of malicious actors on the learned model.[referencja do wikipedii z której to jest wzięte](https://en.wikipedia.org/wiki/Federated_learning)

The _democratization_ means that multiple people can help to teach


In that regard, it is the goal of the project that makes FL training as easy and productive as possible for data scientists and machine learning engineers. In particular, as applications and use-cases are emerging in the edge computing space, Flame aims to facilitate FL at the edge.

As FL is a fast evolving technology, Flame tries to decouple the development of a machine learning workload from its deployment and management. With Flame, a diverse of set of topologies (e.g., central, hierarchical, vertical, hybrid, etc.) can be easily composed and different backend communication protocols (e.g., mqtt) can be supported. We cover these core functionalities of Flame here.


## 2. Theoretical background/technology stack ##

### Tech stack
Other than knowing ML and flame framework itself, users needn't have extensive cloud or programming knowledge:
* `python` is used for implementing ML logic
* `json` file describes job's schema in an easily readable hierarchical way
* `flame` cli is used for combining the above and deployment


[//]: # (* **go-lang** is the backbone of the project and is needed as a dependency)

## 3. Case study concept description ##
## 4. Solution architecture ##
## 5. Environment configuration description ##
## 6. Installation method ##
## 7. How to reproduce - step by step ##
### 1. Infrastructure as Code approach ##
## 8. Demo deployment steps: ##
### 1. Configuration set-up ##
### 2. Data preparation ##
### 3. Execution procedure ##
### 4. Results presentation ##
## 9. Summary – conclusions ##
## 10. References ##
https://en.wikipedia.org/wiki/Federated_learning
