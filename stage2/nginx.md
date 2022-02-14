[nginx文档](https://nginx.org/en/docs/)
### nginx 文件夹结构
```
|-conf
    |- default.conf  #配置文件 
|-html      
    |- index.html  #默认的首页
    |- 50x.html  
|-sbin  
    |- nginx  #启动程序  
```
### nginx command
`./nginx -h` 查看帮助文档
`./nginx `  启动nginx  
`./nginx -s stop ` 停止  
`./nginx -s reload` 重新加载配置  
### nginx 工作模式
`master&worker`  
nginx之所以高并发的原因：
- worker的抢占机制
- 类似于多路复用器的非阻塞处理
### root和alias的区别
### location的匹配规则
### DNS域名解析
### nginx的用途
- 反向代理 
- 负载均衡
- 动静分离
- 网关



### 配置上游服务upstream，反向代理
```
upstream tomcats {
    server 127.0.0.1:8080;
    server 145.78.0.5:8080;
    server 136.98.0.9:8080;
}
``` 
upstream配置参数
- weight=1;权重，正相关
- 
### 负载均衡的策略
- 轮询 默认的策略
- 加权轮询 weight=1;
- ip_hash 根据ip计算hash路由到上游服务
- url_hash 根据url计算hash路由到上游服务
- least_conn 根据最小连接数路由到上游服务，谁的连接数少就将请求分给该上游服务。




### 缓存
主要分为两类缓存：
- nginx控制浏览器的缓存
- nginx缓存上游服务器的静态资源
浏览器自己也有自己的缓存，如果nginx不设置，那么各个浏览器就用自己的缓存策略
### ssl 
### 动静分离
cdn



### nginx HA 
使用Keepalived组件实现nginx的高可用

keepalived使用虚拟ip技术，管理nginx的master和backup节点，从而实现高可用。
将主备nginx节点上都安装keepalived，ka将根据配置虚拟出一个ip绑定在master节点上，通过该虚拟ip访问可实现高可用。
master和backup之间保持心跳，如果检测到master宕机，那么ka将backup的ip绑定到虚拟ip上，从而访问backup节点。
master节点修复，backup与master之间的心跳检测到master节点已修复，那么会将backup的虚拟ip绑定解除，而将master的虚拟ip绑定打开。

ka中可以设置检测nginx状态的任务，如果nginx挂了就重启，重启失败，就让ka停止运行，启用备份节点。

由于ka的master和backup节点会造成backup资源的浪费，所以可以让master和backup互为主备，虚拟两个ip轮询访问。从而实现双主热备。


### LVS
Linux Virtual Server
lvs是使用四层协议，由于不需要解析报文和不接收返回，所以比nginx的性能和吞吐量都高。可以放在nginx的前面。
nginx使用七层协议的应用层做负载均衡和高可用的。






