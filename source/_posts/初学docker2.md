---
title: 初学docker2
date: 2017-07-05 19:58:19
tags: [docker,redis]
categories: docker
---

使用Docker的常规做法，数据库单独用一个Image，程序一个Image，利用Docker的link属性将他们连接起来，配合使用。
<!-- more -->
下载官方的redis最新镜像

    $ sudo docker pull redis:latest 

启动redis镜像的Container，开启redis-server持久化服务。

    $ sudo docker run --name redis-server -d redis redis-server --appendonly yes

再启动一个redis镜像的Container作为客户端，连接我们刚才启动的redis-server

    $ sudo docker run --rm=true -it --link redis-server:redis redis /bin/bash

    $ redis-cli -h "$REDIS_PORT_6379_TCP_ADDR" -p "$REDIS_PORT_6379_TCP_PORT"
    $ 172.17.0.34:6379> set a 1 #成功连入redis数据库服务器
    OK
    $ 172.17.0.34:6379> get a
    "1"


