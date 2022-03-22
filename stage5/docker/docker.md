[docker入门教程](https://www.bilibili.com/video/BV1CJ411T7BK)
CentOS6上运行docker服务
## 安装docker&设置国内代理
## docker image 相关命令
- docker images //列出所有镜像
- docker images -q //列出所有镜像的id
- docker pull centos:7 //拉取镜像
- docker rmi CONTAINERID//删除单个镜像
- docker rmi `docker images -q`//删除所有镜像
## 容器相关命令
- docker run -it --name=c1 CentOS:7 /bin/sh //-i 保持容器运行，直到exit退出。-t建立一个虚拟终端 /bin/sh 以什么命令开启终端 以交互式方式启动容器
- docker ps //查看所有正在运行的容器
- docker ps -a //查看所有容器的历史记录，包括正在运行的，和已经结束的
-  docker run -id --name=c2 centos:7 /bin/sh //以守护方式启动容器
-  docker exec -it c2 /bin/sh
