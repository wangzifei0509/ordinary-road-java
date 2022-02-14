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






