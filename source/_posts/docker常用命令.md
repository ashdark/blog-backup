---
title: docker常用命令
date: 2017-04-30 17:05:52
tags: [docker]
categories: "docker"
---



## pull docker 镜像

```
# docker pull centos:6.6

```

## 查看docker 镜像

```
# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
jun/lnmp            latest              bbb646441ce0        3 minutes ago       1.02 GB
centos              7                   a8493f5f50ff        2 weeks ago         192 MB
d4w/nsenter         latest              9e4f13a0901e        7 months ago        83.8 kB
centos              6.6                 d03626170061        7 months ago        203 MB

```

## 在docker index中搜索image（search）

    # docker search seanlo


## 运行centos镜像 bash
```
# docker run -it <IMAGE ID> /bin/bash

```

## 查看正在运行的docker 容器

```
# docker ps
```

## 查看所有docker 容器

```
# docker ps -a
```

## 删除容器

```
# docker rm <CONTAINER ID>
```

## 删除所有容器

```
# docker rm $(docker ps -q -a)
```

## 停止、启动、杀死一个容器

```
# docker stop <容器名orID>
# docker start <容器名orID>
# docker kill <容器名orID>
```

## 删除镜像

```
# docker rmi <IMAGE ID>
```

## 删除所有镜像

```
# docker rmi $(docker images -q)
```

## 把一个容器提交为镜像

```
# docker commit <container-id> <image-name>
```

## 导出 （export） 
>Export命令用于持久化容器（不是镜像）
    

```
# sudo docker export <CONTAINER ID> > /home/export.tar
```

## 保存 （save）
>Save命令用于持久化镜像（不是容器）

```
# docker save <IMAGE ID> > /home/save.tar
```

## 导入 （import）
>从容器快照文件中再导入为镜像

```
# cat export.tar | docker import - jun/lnmp:1.0
```

## 加载镜像 （load）

>加载保存的镜像
    
```
# docker load < /home/save.tar
```

## 运行一个新容器，同时为它命名、端口映射、文件夹映射。以redmine镜像为例

```
# docker run --name redmine -p 9003:80 -p 9023:22 -d -v /var/redmine/files:/redmine/files -v /var/redmine/mysql:/var/lib/mysql sameersbn/redmine
```

## 一个容器连接到另一个容器

```
# docker run -i -t --name sonar -d -link mmysql:db tpires/sonar-server sonar
```

## 连接到正在运行中的container（attach）

>要attach上去的容器必须正在运行，可以同时连接上同一个container来共享屏幕（与screen命令的attach类似）。
官方文档中说attach后可以通过CTRL-C来detach，但实际上经过我的测试，如果container当前在运行bash，CTRL-C自然是当前行的输入，没有退出；如果container当前正在前台运行进程，如输出nginx的access.log日志，CTRL-C不仅会导致退出容器，而且还stop了。这不是我们想要的，detach的意思按理应该是脱离容器终端，但容器依然运行。好在attach是可以带上--sig-proxy=false来确保CTRL-D或CTRL-C不会关闭容器。

    # docker attach --sig-proxy=false $CONTAINER_ID
    
    
## 使用docker attach进入Docker容器

    # docker attach <CONTAINER ID> 


## 使用docker exec进入Docker容器

    # docker exec -it <CONTAINER ID> /bin/bash  
