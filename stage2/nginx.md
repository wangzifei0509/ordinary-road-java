### nginx 文件夹结构
```
|-config    
    |- default.conf  #配置文件 
|-html  
    |- index.html  #默认的首页
    |- 50x.html  
|-sbin  
    |- nginx  #启动程序  
```
### nginx common command
`./nginx `  启动nginx  
`./nginx -s stop ` 停止  
`./nginx -s reload` 重新加载配置  
### nginx 工作模式
`master&worker`  
nginx之所以高并发的原因：
- worker的抢占机制
- 类似于多路复用器的异步处理



