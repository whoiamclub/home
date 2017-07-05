---
title: 初学docker1
date: 2017-07-05 19:26:03
tags: [docker]
categories: docker
---
Docker是一个开源的应用容器引擎，可以让开发者打包自己的应用及依赖到一个可移植的容器中，然后发布到任何流行的Linux机器上，也可实现虚拟化。
<!-- more -->
对于在CentOS 7下的用户，安装非常简单，直接运行如下命令，就可以安装最新版本的Docker。
    $ sudo yum install docker

启动Docker服务，并且把Docker服务开机启动。

    $ sudo service docker start
    $ sudo chkconfig docker on

输入如下命令，检查Dcoker进程是否已经启动。

    $ ps -ef|grep docker

现在Docker服务已经安装并启动，接下来需要下载Image镜像，镜像就是应用运行的环境，比如自己装好Node.js和npm然后发布到Docker Hub上，供自己或者别人下载，也可以下载安装一些官方的镜像，把它作为镜像的基础。
先下载CentOS镜像
    
    $ sudo docker pull centos:7

执行命令查看镜像是否安装成功。
    
    $ sudo docker images centos

#### docker基本命令

    1、获取镜像。
    $ sudo docker pull NAME[:TAG]
    $ sudo docker pull centos:latest 
    2、启动Container盒子。
    $ sudo docker run [OPTIONS] IMAGE [COMMAND] [ARG...] 
    $ sudo docker run -t -i centos /bin/bash
    3、查看镜像列表，会把本地所有的images列出。
    $ sudo docker images [OPTIONS] [NAME]
    $ sudo docker images centos
    4、查看容器列表，可以看到所有我们创建过的Container。
    $ sudo docker ps [OPTIONS] 
    $ sudo docker ps -a
    5、删除镜像，从本地删除一个已经下载的镜像。
    $ sudo docker rmi IMAGE [IMAGE...] 
    $ sudo docker rmi centos:latest
    6、移除一个或多个容器实例。
    $ sudo docker rm [OPTIONS] CONTAINER [CONTAINER...]
    $ sudo docker rm sudo docker ps -aq
    7、停止一个正在运行的容器。
    $ sudo docker kill [OPTIONS] CONTAINER [CONTAINER...]
    $ sudo docker kill 026e
    8、重启一个正在运行的容器。
    $ sudo docker restart [OPTIONS] CONTAINER [CONTAINER...]
    $ sudo docker restart 026e
    9、启动一个已经停止的容器。
    $ sudo docker start [OPTIONS] CONTAINER [CONTAINER...]
    $ sudo docker start 026e

简单说明一下Image和Container的关系。Image顾名思义就是镜像的意思，可以把它理解为一个执行环境（env），当执行docker run命令之后，Dock就会根据当前的Image创建一个新的Container，Container是一个程序运行的沙箱，它们互相独立，但都是运行在Image创建的执行环境之上。