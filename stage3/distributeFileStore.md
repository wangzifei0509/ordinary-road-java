## 分布式文件存储常用组件
- Fdfs
- S3
- 公有云存储

## FastDFS 
Fast Distribute File service,Fdfs,开源轻量级分布式文件存储系统。
### 核心组件
- tracer，管理组件，也可以创建几个tracer节点，使用tracer集群实现管理组件的高可用
- storage，存储组件，负责具体的存储
- fdfs-nginx-module nginx组件，可以通过http访问fdfs中的文件。
- nginx nginx作为http server 反向代理
### 核心概念
组，或者是卷，一个组可以有多个节点，一个组内的节点上存储的文件都是一样的，为了高可用，为了备份，为了负载均衡。每个节点上的文件会自动同步。

### fdfs的java client
