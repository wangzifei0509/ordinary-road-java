# java架构师-技术专家 学习笔记
项目架构演进：
- 单体，前后端在一起部署在vm上
- 集群，前后端分离，一个项目部署多个实例在一个vm上
- 分布式，一个项目的多个实例分别部署在不同的vm上
- 云原生，Docker作为部署的单元，使用K8S实现部署的编排，调度、管理等功能
部署对象演进：以java项目为例
- war，需要外部tomcat环境
- jar，内置了tomcat
- docker image，自带java运行时，可迁移
- helm，yml文件，自带项目运行时所需要的条件
## Stage 1 计算机基础
- 计算机操作系统
- 计算机网络
- 计算机组成原理
- Linux操作系统
- 【深入理解】数据结构（数组，链表，树，图）  
- 【深入理解】算法（动态规划，贪心算法）
## Stage 2 Java
- 【深入理解】Java进阶（JUC&JVM）
- 【深入理解】SSM基础和进阶（单体应用|微服务）
- 【深入理解】maven、Tomcat
## Stage 3 中间件
- 【深入理解】Mysql（分库分表|读写分离）、Redis
- 【深入理解】RocketMQ、Kafka
- 【读过源码】Netty、GRPC 
- ~~【了解会用】Sentinel、SkyWalking、Prometheus ~~
## Stage 4 Devops和云原生
- ~~【了解会用】Go、Gin ~~
- 【深入理解】Docker、K8S
## Stage 5 Java架构师
- Go、Gin、Gorm
- Docker| K8S operator go
- argo rollout |argo workflow go 
- Istio go
- Envoy C++
- Prometheus go
- SkyWalking java
- Grafana ts&go
- kafka、TiDB、配置、etcd|Sentinel|Skywalking|JAEGER|Prometheus|fluentd
- 云原生思维|devops|CICD|微服务|可观测性|可诊断性|不可不变基础设施
- 基于微信小程序的发布管理平台
- IDEA定制代码扫描规则插件
## Stage 6 质量和性能开发
## Stage 7 AI

## 学习笔记：https://www.yuque.com/wangxiamei/nf4oq7/tf0ucqpz1r1dkcwf
本仓库存储对应的代码


