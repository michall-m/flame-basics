# Project documentation



## **Flame basics**
[flame repository][flame repo]

Stanisław Łenyk, Michał Misiak,
Mateusz Słuszniak, Jerzy Wilczek

2023, Thursday 11:20



## 1. Introduction
The vision of **Flame** is to democratize federated learning (FL).

**Flame** is a framework for creating democratized environments for federated learning.

[**Federated learning**][federated learning wiki] (also known as collaborative learning) is a machine learning technique that trains an algorithm across multiple decentralized edge devices or servers holding local data samples, without exchanging them. This approach stands in contrast to traditional centralized machine learning techniques where all the local datasets are uploaded to one server, as well as to more classical decentralized approaches which often assume that local data samples are identically distributed.

Federated learning enables multiple actors to build a common, robust machine learning model without sharing data, thus allowing to address critical issues such as data privacy, data security, data access rights and access to heterogeneous data. Its applications are spread over a number of industries including defense, telecommunications, IoT, and pharmaceutics. A major open question at the moment is how inferior models learned through federated data are relative to ones where the data are pooled. Another open question concerns the trustworthiness of the edge devices and the impact of malicious actors on the learned model. 

In that regard, it is the goal of the project that makes FL training as easy and productive as possible for data scientists and machine learning engineers.

As FL is a fast evolving technology, Flame tries to decouple the development of a machine learning workload from its deployment and management. With Flame, a diverse of set of topologies (e.g., central, hierarchical, vertical, hybrid, etc.) can be easily composed and different backend communication protocols (e.g., mqtt) can be supported. We cover these core functionalities of Flame here.

## 2. Theoretical background

Flame should allow the machine learning model to be developed completely separately from the devops and infrastructure work necessary for establishing a functioning federated learning system. The framework is based on defining TAGs -- _Topology Abstraction Graphs_. TAGs describe how various parts of the federated learning system should connect with each other. They define the overall structure of the system and which nodes should receive which kinds of data from which other nodes.

### Tech stack
Other than knowing ML and flame framework itself, users needn't have extensive cloud or programming knowledge:
* `Python` is used for implementing ML logic
* `JSON` files are used for describing job's schema and properties
* `Flame` cli is used for combining the above and deployment

`golang` is the backbone of the project's development side, thought users won't interact with it.

## 3. Case study concept description
We will base our case study on examples provided in the [Flame Repository](https://github.com/cisco-open/flame). Specifically, we will focus on the Med-MNIST example [Med-MNIST](https://github.com/cisco-open/flame/tree/main/examples/medmnist) in our prototype. Since Machine Learning is not within the scope of this course, we will not modify any of the Python code that implements the actual ML tasks. Instead, we will demonstrate the mechanisms of the FLAME framework using special functions such as aggregate, distribute, fetch, and upload, which we will describe later. Additionally, we will implement our own functions that operate on nodes for a simple example. Furthermore, we will create a few examples with our own topologies described in Topology Abstraction Graphs (TAGs).

## 4. Solution architecture
Based on the case study concept, we present a solution architecture. Our TAG topology consists of three worker nodes (roles), one in the United States, Europe, and Asia which are then connected to the master node (central role). To better understand how TAG work and are build let us introduce some theoretical background about roles and channel, nucleus elements of TAGs.

A channel is an undirected edge between a pair of roles. It is an abstraction for communication backend or protocols.

Each of the two building blocks can have attributes. Attributes further define what these building blocks can do.

For role, it has two attributes: isDataConsumer and replica.

isDataconsumer: this is a boolean attribute to denote that a role is supposed to consume data. If the attribute is set, it indicates workers created from this role are training workers. It has an important implication, indicating the number of specified datasets corresponds to the number of workers from the role with isDataConsumer attribute set.

replica: This is applied to the roles with no isDataConsumer attribute set. This feature is for high availability.

A channel also has two attributes: groupBy and funcTags.

groupBy: This attribute is used to group roles of the channel based on a tag. Therefore, the groupBy attribute allows to build a hierarchical topology (e.g., a single-rooted multi-level tree), for instance, based on geographical location tags (e.g., us, uk, fr, etc). Currently a string-based tag is supported. Future extensions may include more dynamic grouping based on dynamic metrics such as latency, data (dis)similarity, and so on.

funcTags This attribute (discussed later in detail) contains what actions a role would take on the channel. As mentioned earlier, a role is associated with executable code. When a role attached to a channel, the role expresses what actions (i.e., functions) it takes on the channel, which is achieved via funcTags attribute. We will discuss how to use funcTags correctly in the later part.

![Federated Learning Schema](./FL_global.jpeg "Federated Learning Schema")

Below we present the schema with defined channels and roles. This is the usage of documentation in practice.
```
{
    "name": "Benchmark of FedOPT Aggregators/Optimizers using MedMNIST example schema v1.0.0 via PyTorch",
    "description": "A simple example of MedMNIST using PyTorch to test out different aggregator algorithms.",
    "roles": [
        {
            "name": "trainer",
            "description": "It consumes the data and trains local model",
            "isDataConsumer": true,
            "groupAssociation": [
                {
                    "param-channel": "us"
                }
            ]
        },
        {
            "name": "aggregator",
            "description": "It aggregates the updates from trainers",
            "replica": 1,
            "groupAssociation": [
                {
                    "param-channel": "us"
                }
            ]
        }
    ],
    "channels": [
        {
            "name": "param-channel",
            "description": "Model update is sent from trainer to aggregator and vice-versa",
            "pair": [
                "trainer",
                "aggregator"
            ],
            "groupBy": {
                "type": "tag",
                "value": [
                    "us"
                ]
            },
            "funcTags": {
                "trainer": [
                    "fetch",
                    "upload"
                ],
                "aggregator": [
                    "distribute",
                    "aggregate"
                ]
            }
        }
    ]
}
```
In a real situation, these nodes would receive models, data, and other resources from smaller sources like single software houses, but to make this example more general, we skip the lowest level of the hierarchy. After computing models in the worker nodes, we merge them in the master node to create a bigger model that aggregates the results from all worker nodes.

We will simulate these nodes using Kubernetes, which is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. Kubernetes provides a consistent way to deploy and manage applications across different environments, such as on-premises data centers and public clouds, and allows for easy scaling and resiliency of applications, making it a popular choice for modern cloud-native architectures. Although we can run our architecture using cloud computing, we will run it locally. Additionally, we will introduce another architecture that presents the aspects of distributed learning instead of federated learning. 


## 5. Environment configuration description
## 6. Installation method
## 7. How to reproduce - step by step
### 1. Infrastructure as Code approach
## 8. Demo deployment steps:
### 1. Configuration set-up
### 2. Data preparation
### 3. Execution procedure
### 4. Results presentation
## 9. Summary – conclusions

[federated learning wiki]: https://en.wikipedia.org/wiki/Federated_learning
[flame repo]: https://github.com/cisco-open/flame
[flame readme]: https://github.com/cisco-open/flame/blob/main/docs/README.md
[med mnist]: (https://github.com/cisco-open/flame/tree/main/examples/medmnist)
