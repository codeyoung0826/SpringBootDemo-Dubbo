# dubbo介绍

Dubbo 是一个分布式服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案，以及 SOA 服务治理方案

## 一、网站架构的发展历程  

网站架构随着业务的发展，逻辑越来越复杂，数据量越来越大，交互越来越多.......

![网站架构的发展历程](https://raw.githubusercontent.com/Baijq/others/master/images/dubbo-img/dubbo-1.png)

- 单一应用架构（OORM）

当网站流量很小时，将所有的功能部署到一起，以减少部署节点和成本。此时，只需要使用简化增删改查的工作量，采用数据访问框架(ORM)。

- 垂直应用架构 （MVC）

当访问量逐渐增大，单一应用带来的加速度越来越小。此时，将应用拆分成互不相干的几个应用，所以采用MVC框架。

- 分布式服务架构 （RPC）

当垂直应用越来越多，应用之交互不可避免，将核心业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，使前端应用能更快速地响应多变的市场需求。此时，用于提高业务复用及整合的服务框架(RPC)是关键。

- 流动计算框架 （SQA）

当服务越来越多，容量的评估，小服务资源的浪费等问题逐渐显现，此时需增加一个调度中心基于访问压力实时管理集群容量，提高集群利用率。此时，用于提高机器利用率的 资源调度和治理中心(SOA) 是关键。

## 二、dubbo核心工作原理

![dubbo核心工作原理](http://dubbo.apache.org/img/architecture.png)

节点 | 角色说明
--|--
Provider|暴露服务的服务提供方
Registry|服务的注册与发现的注册中心，如zookeper(推荐)、multicast、redis、simple
Consumer|调用远程服务的服务消费方
Monitor|统计服务的调用次数和调用时间的监控中心
Container|服务运行容器

### 调用流程

- 服务器负责启动，加载，运行服务提供者。

- 服务提供者在启动时，向注册中心注册自己所提供的服务

- 服务消费者在启动时，向注册中心订阅自己所需的服务

- 注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于TCP长连接推送变更数据给消费者

- 服务消费者从提供的服务列表中，基于软负载均衡算法，选一台提供者进行调用，如果失败，则选择另一台调用

- 服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到检测中心

### 三、dubbo特点

1. Dubbo 支持 RPC 调用，服务之间的调用性能会很好，效率很高

2. 支持多种序列化协议，如 Hessian(默认)、HTTP、WebService

3. 对比springcloud

![dubbo和SpringCloud对比](https://raw.githubusercontent.com/Baijq/others/master/images/dubbo-img/dubbo-4.png)