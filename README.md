# java架构师-技术专家 学习笔记
项目架构演进：
- 单体，前后端在一起部署在vm上
- 集群，前后端分离，一个项目分成多个实例部署在vm上
- 分布式，一个项目的多个实例分别部署在不同的vm上。
- 云原生，Docker作为部署的单元，使用K8S实现部署的编排，调度、管理等功能
## Stage 1 计算机基础
- 计算机操作系统
- 计算机网络
- 计算机组成原理
- linux操作系统
- 数据结构（链表，数组，树，图）
- 算法（动态规划，贪心算法）
## stage 2 java
- java进阶（JUC&JVM）
- SSM基础和进阶（单体应用，微服务）
- Mysql基础和进阶（分库分表|读写分离）
- Redis基础和进阶
- Nginx
## stage 3 分布式
- Zookeeper基础
- ES基础和进阶
- RocketMQ、Kafaka
- Tomcat、Netty、GRPC 
- Sentinel 、SkyWalking
## stage 4 devops和云原生
- Go、Gin Gorm
- Docker|K8S
- git|maven 
- agent增强|idea插件|maven插件  
## stage 5 不断更新
- 高并发|分布式|高可用|微服务
- 常用组件源码分析
- 思考和实践经验
- 学习方法

Doocs 社区优质项目
Doocs 技术社区，致力于打造一个内容完整、持续成长的互联网开发者学习生态圈！以下是 Doocs 旗下的一些优秀项目，欢迎各位开发者朋友持续保持关注。

#	项目	描述	热度
1	advanced-java	互联网 Java 工程师进阶知识完全扫盲：涵盖高并发、分布式、高可用、微服务、海量数据处理等领域知识。 https://github.com/doocs/advanced-java	

2	leetcode	多种编程语言实现 LeetCode、《剑指 Offer（第 2 版）》、《程序员面试金典（第 6 版）》题解。	
https://github.com/doocs/leetcode
3	source-code-hunter	互联网常用组件框架源码分析。	
https://github.com/doocs/source-code-hunter
4	jvm	Java 虚拟机底层原理知识总结。	
https://github.com/doocs/jvm
5	coding-interview	代码面试题集，包括《剑指 Offer》、《编程之美》等。
https://github.com/doocs/coding-interview

https://github.com/CyC2018/CS-Notes
https://github.com/Snailclimb/JavaGuide
https://github.com/labuladong/fucking-algorithm



我不想听你看来的这些东西，我想听你思考的东西，你们具体在什么场景下用的MQ，如果不用MQ，你的项目又怎么设计？你思考一下你的XX项目，中间还有没有哪一块功能可以用上MQ？为什么？如果用了，你猜一下生产上可能出现什么故障？怎么解决？既然你知道他的作用是“解耦、消峰、异步”，那么在你简历中提到的XXX技术中（比如nginx，或者任何知识点），分别可以通过什么手段去做这三个目的？你在Java/Android/IOS中还见过类似的组件或者机制吗？他们怎么做的？为什么？你怎么看如何解决MQ中消息重复的问题？有必要对所有的消费者都做幂等吗？为什么？幂等在你们xx项目中，具体怎么实现。还有哪些情况你碰到过“消息重复”类似的问题？BASE理论里，如果涉及到MQ的场景，怎么设计？除了你说的这种设计，还有哪种设计？在你的xxx项目中应该怎么设计？为什么？


