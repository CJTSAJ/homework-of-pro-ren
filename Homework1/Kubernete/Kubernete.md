# Kubernete
## 1 简介
 Kubernete是google公司开源的大规模容器集群管理系统，它为容器化应用提供了资源调试、部署、服务发现、扩展机制等功能。
 
## 2 Kubernete可以做什么？
在现代Web服务中，用户希望应用程序一周7天24小时可用，开发人员希望每天部署这些应用程序的新版本几次。容器化帮助软件包实现这些目标，使应用程序能够以简单快速的方式发布和更新，而不会停机。Kubernetes帮助您确保这些容器化的应用程序在您希望的位置和时间运行，并帮助它们找到它们需要工作的资源和工具。

## 3 基本模型
### 3.1 Create a Kubernetes cluster
![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework1/Kubernete/module_01.svg)
### 3.2 Deploy an app
![](https://github.com/CJTSAJ/homework-of-pro-ren/blod/master/Homework1/Kubernete/module_02.svg)
### 3.3 Explore your app
![](https://github.com/CJTSAJ/homework-of-pro-ren/blod/master/Homework1/Kubernete/module_03.svg)
### 3.4 Expose your app publicly
![](https://github.com/CJTSAJ/homework-of-pro-ren/blod/master/Homework1/Kubernete/module_04.svg)
### 3.5 Scale up your app
![](https://github.com/CJTSAJ/homework-of-pro-ren/blod/master/Homework1/Kubernete/module_05.svg)
### 3.6 Update your app
![](https://github.com/CJTSAJ/homework-of-pro-ren/blod/master/Homework1/Kubernete/module_06.svg)
## 4 核心概念 

### 4.1 Node
Node是Kubernete中的一个工作机器，可以是物理机或虚拟机。依据角色不同分类主控节点（Master）与从属节点（Minion)。其中Master提供调试与控制功能，负责整个集群的管理工作，而Minion则是集群的工作节点。

### 4.2 Pod
Pod是Kubernetes的基本操作单元，是最小的可创建、调试和管理的部署单元。把相关的一个或多个容器构成一个Pod，通常Pod里的容器运行相同的应用。Pod包含的容器运行在同一个Minion(Host)上，作业一个统一管理单元，共享相同的volumes和network namespace/IP和Port空间。     

### 4.3 Service
Services也是Kubernetes的基本操作单元，是真实应用服务的抽象，每一个服务后面都有很多对应的容器来支持。Kubernete用于定义一系列Pod逻辑关系与访问规则，服务的目标是为了隔绝前端与后端的耦合性。通过服务Proxy的port和服务selector决定服务请求传递给后端提供服务的容器，对外表现为一个单一访问接口，外部不需要了解后端如何运行。

### 4.4 Replication Controller
Replication Controller是Kubernete的副本控制器，确保任何时候Kubernetes集群中有指定数量的pod副本(replicas)在运行， 如果少于指定数量的pod副本(replicas)，Replication Controller会启动新的Container，反之会杀死多余的以保证数量不变。Replication Controller使用预先定义的pod模板创建pods。对于利用pod 模板创建的pods，Replication Controller根据label selector来关联。

### 4.5 Label
Label是一组附加在各类对象上的键值对，是Kubernete中最重要的节点分组方法，用于区分Pod、Service、Replication Controller。每个Pod、Service、 Replication Controller可以有多个label，但是每个label的key只能对应一个value。Labels是Service和Replication Controller运行的基础，Kubernete通过Label来选择正确的容器，将访问Service的请求转发给后端提供服务的多个容器。同样，Replication Controller也使用labels来管理通过pod 模板创建的一组容器。

## 5 Kubernete的特性和优点

kubernete既是一个容器平台、也是一个微服务平台、还是一个便携式云平台。这使其拥有了Paas的大部分简单性、Iaas的灵活性以及可移植性。

## 6 Kubernete和Docker的关系
Docker和Kubernete均脱胎于Paas。Docker舍弃了一些Paas原有的复杂的功能，只负责代码的封装和发布，这恰好成为了Docker的优势，其简单性让docker获得了巨大的市场。而google的kubernete则基于容器技术提供了源调度、部署运行、均衡容灾、服务注册、扩容缩容等功能实现了对容器的管理与调度。从某种意义上来讲kubernete较docker更为强大，但在提升管理层次的同时，又给使用者带来了巨大的学习负担。

## 7 reference
[Kubernete官网](https://kubernetes.io/)

[Kubernete主要概念](http://f.dataguru.cn/thread-716080-1-1.html)

[Docker、 Google Kubernetes与PaaS不得不说的渊源](https://www.sdnlab.com/13380.html)
 
