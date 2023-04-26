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
We will base our case study on examples provided in the [Flame Repository][flame repo]. Specifically, we will focus on the Med-MNIST example [Med-MNIST][med mnist] in our prototype. Since Machine Learning is not within the scope of this course, we will not modify any of the Python code that implements the actual ML tasks. Instead, we will demonstrate the mechanisms of the FLAME framework using special functions such as aggregate, distribute, fetch, and upload, which we will describe later. Additionally, we will implement our own functions that operate on nodes for a simple example. Furthermore, we will create a few examples with our own topologies described in Topology Abstraction Graphs (TAGs).

## 4. Solution architecture

## 5. Environment configuration description
[Flame's ubuntu setup guide][flame setup]

A Kubernetes cluster can be deployed on either physical or virtual machines. In our case it will be a local linux machine.

To get started with Kubernetes development, one can use Minikube. Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one node. Minikube is available for Linux, macOS, and Windows systems. The Minikube CLI provides basic bootstrapping operations for working with your cluster, including start, stop, status, and delete.

### Starting flame
We start minikube and create a tunnel:
```shell
minikube start --cpus 4 --memory 4096m --disk-size 100gb
minikube tunnel
```
To bring up flame and its dependent applications, helm is used. Flame provides a script to ensures that the latest official flame image from docker hub is used:
```shell
./flame.sh start
```

### Validating deployment
```shell
kubectl get pods -n flame
```
An example output looks like the following:
```
NAME                                READY   STATUS    RESTARTS       AGE
flame-apiserver-5df5fb6bc4-22z6l    1/1     Running   0              7m5s
flame-controller-566684676b-g4pwr   1/1     Running   6 (4m4s ago)   7m5s
flame-mlflow-965c86b47-vd8th        1/1     Running   0              7m5s
flame-mongodb-0                     1/1     Running   0              3m41s
flame-mongodb-1                     1/1     Running   0              4m3s
flame-mongodb-arbiter-0             1/1     Running   0              7m5s
flame-mosquitto-6754567c88-rfmk7    1/1     Running   0              7m5s
flame-mosquitto2-676596996b-d5dzj   1/1     Running   0              7m5s
flame-notifier-cf4854cd9-g27wj      1/1     Running   0              7m5s
postgres-7fd96c847c-6qdpv           1/1     Running   0              7m5s
```
As a way to test a successful configuration of routing and dns, test with the following commands:
```
ping -c 1 apiserver.flame.test
ping -c 1 notifier.flame.test
ping -c 1 mlflow.flame.test
```
### Stopping flame
Once using flame is done, one can stop flame by running the following command:
```
./flame.sh stop
```


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
[flame setup]: https://github.com/cisco-open/flame/blob/main/docs/03-a-ubuntu.md
[med mnist]: https://github.com/cisco-open/flame/tree/main/examples/medmnist
