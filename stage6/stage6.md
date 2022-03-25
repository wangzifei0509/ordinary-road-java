## Netty
## TCP通信基础
socket是网络上运行的两个程序之间双向通信链路的一个端点。套接字绑定到端口号，以便 TCP 层可以识别数据要发送到的应用程序。是通信隧道。
TCP/IP通信模型设计为四个层级，由上到下分别是：应用层、传输层、网络层、网络接口层。
应用层-java程序
传输层-TCP UDP
网络层-IP
网络接口层-硬件接口层









## 性能调优
### 理论四板斧
> 1. 借助监控预防问题、发现问题;
> 2. 借助工具定位问题;
> 3. 定期复盘，防止同类问题出现;
> 4. 定好规范，一定程度上规避问题;

### 应用性能调优
#### skywalking
[skywalking官方文档](https://skywalking.apache.org/docs/main/v8.4.0/en/concepts-and-designs/overview/)
1. 定义  
APM（application performance manage）工具，一个开源可观测平台，用于收集、分析、聚合和可视化来自服务和云原生基础设施的数据。SkyWalking 为服务、服务实例、端点提供可观察性能力。
  
- **架构**包括Probes、Platform backend（Observability Analysis platform，OAP）、Storage 和 UI。
- **核心概念** 


### jvm调优
### 数据库调优
### 架构调优
### 操作系统调优

### 常见问题分类
- CPU飙高
- 内存飙高，OOM
- 响应缓慢
    - 线程数耗尽
    - GC频繁
- 502服务宕机


