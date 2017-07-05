---
title: 初学docker3
date: 2017-07-05 20:02:36
tags: [docker,nodejs]
categories: docker
---

制作一个Node.js包含Express.js环境的镜像，通过pm2来启动web应用，然后发布到Docker云上；
我们还会使用redis数据库来暂存用户的访问次数；
在Node.js应用前端，我们需要放置一个Nginx作为反向代理。
<!-- more -->

第一步，我们把需要用到的Image镜像统统都下载到本地，执行如下命令。

    $ sudo docker pull redis:latest
    $ sudo docker pull node:latest
执行docker images检查一下这些镜像是否都安装完毕。

我们先在本地创建一个部署Node.js应用的目录，然后写上package.json

    $ mkdir /var/node/
    $ mkdir /var/node/docker_node
在创建我们的应用之前，我们从node这个镜像基础上，开始制作自己的镜像，这个镜像只是比node镜像多了一个pm2的命令。
运行如下命令，进入到Container的命令行，然后我们安装pm2软件。
它是Node.js进程管理软件，可以方便地重启进程和查看Node.js日志。

    $ sudo docker run -i -t node /bin/bash
    #进入Container的bash	
    $ npm install pm2 -g
    #从Container的bash退出
    $ exit
这样我们就成功地在node这个镜像的基础上安装了pm2，然后我们要把这个新的Container保存为镜像，这样以后我们要用到带pm2的Node.js镜像，只需下载它即可。
执行命令，进行登录，然后把镜像push到云上，非官方不允许直接提交根目录镜像，所以必须以<用户名>/<镜像名>这样的方式提交，比如doublespout/node_pm2这样
    
    #使用docker官网注册的用户名和密码进行登录
    $ sudo docker login
    Username: <Your Docker Account>
    Password: 
    Email:  <Your Email>
    Login Succeeded
    
    #查看所有Container，找到node_pm2的CONTAINER ID
    $ sudo docker ps -a
    CONTAINER ID  IMAGE   COMMAND       CREATED         STATUS           PORTS      NAMES
    7a3e85bfaddf  node:0  "/bin/bash"   5 minutes ago   Exited (130)...             goofy_fermi
    
    #登录成功之后，把Container提交为Images
    $ sudo docker commit 7a3e doublespout/node_pm2
    
    #然后查看Images列表
    $ sudo docker images node_pm2
    REPOSITORY          TAG                 IMAGE ID            CREATED              VIRTUAL SIZE
    node_pm2            latest              9a418757ae2b        About a minute ago   714.8 MB
    
    #把镜像提交到云上
    $ sudo docker push doublespout/node_pm2

    #从云上下载node_pm2
    $ sudo docker pull doublespout/node_pm2

接下来我们将通过redis镜像，启动一个redis的Container，命令如下：

    docker run --name redis-server -d redis redis-server --appendonly yes

然后我们要准备编写Node.js代码，实现这个计数访问应用的功能。
在/var/node/docker_node目录下创建如下的package.json文件。

    {
      "name": "docker_node",
      "version": "0.0.1",
      "main": "app.js",
      "dependencies": {
           "express":"4.10.2",
           "redis":"0.12.1",
       },
      "engines": {
        "node": ">=0.10.0"
      }
    }
    
然后我们创建app.js，启动并监听8000端口，同时通过redis记录访问次数。
``` bash
var express = require('express');
var redis = require("redis");
var app = express();
//从环境变量里读取redis服务器的ip地址
var redisHost = process.env['REDIS_PORT_6379_TCP_ADDR'];
var redisPort = process.env['REDIS_PORT_6379_TCP_PORT'];

var reidsClient = redis.createClient(redisPort, redisHost);

app.get('/', function(req, res){
	  console.log('get request')
	  reidsClient.get('access_count', function(err, countNum){
	  		if(err){
	  			return res.send('get access count error')
	  		}
	  		if(!countNum){
	  			countNum = 1
	  		}
	  		else{
	  			countNum = parseInt(countNum) + 1
	  		}
	  		reidsClient.set('access_count', countNum, function(err){
	  			if(err){
		  			return res.send('set access count error')
		  		}
		  		res.send(countNum.toString())
	  		})
	  })
});

app.listen(8000);
```
启动一个Container把依赖包装一下，命令如下：

    $ sudo docker run --rm -i -t -v /var/node/docker_node:/var/node/docker_node -w /var/node/docker_node/ doublespout/node_pm2 cnpm install
-w参数表示命令执行的当前工作目录，屏幕会打印依赖包的安装过程，等所有Node.js的包安装完成后，这个Container会自动退出。

如果出现EACCESS的权限错误，可以执行如下命令，许可SELinux的工作状态，不过这只是临时修改，重启系统后会恢复。

    su -c "setenforce 0"
代码开发完毕，基于刚才提交的doublespout/node_pm2镜像，需要启动一个运行这个程序的Container，要求这个Container有端口映射、文件挂载，并同时加载redis的那个Container，命令如下：

    #挂载pm2的日志输出
    $ mkdir /var/log/pm2
    #使用pm2启动app应用，会有问题
    $ sudo docker run -d --name "nodeCountAccess" -p 8000:8000 -v /var/node/docker_node:/var/node/docker_node -v /var/log/pm2:/root/.pm2/logs/ --link redis-server:redis -w /var/node/docker_node/  doublespout/node_pm2 pm2 start app.js
但是当我们执行docker ps后发现这个Container并没有启动，这是什么原因呢？
因为利用pm2的守护进程方式启动应用，所以Container会认为进程已经运行结束，所以自己退出了，
这时候需要让pm2以非守护进程的方式运行在Container里即可。

    $ sudo docker run -d --name "nodeCountAccess" -p 8000:8000 -v /var/node/docker_node:/var/node/docker_node -v /var/log/pm2:/root/.pm2/logs/ --link redis-server:redis -w /var/node/docker_node/  doublespout/node_pm2 pm2 start --no-daemon app.js
再执行docker ps，就可以看到nodeCountAccess这个名字的Container在运行了，使用浏览器打开主机的8000端口，也能看到访问的计数次数。

接下来配置Nginx。

由于使用Docker的Container它的ip地址是动态变化的，所以想要使用Nginx容器来做反向代理，配置写起来比较困难，暂不使用Docker容器来管理Nginx，而是直接编译安装Nginx。

我们使用Nginx的分支版本openresty来做反向代理，openresty比Nginx内置了ngx-lua模块，让Nginx具有逻辑处理能力，我们用yum安装依赖包，然后编译安装openresty。

    yum install -y gcc gcc-c++ kernel-devel
    yum install -y readline-devel pcre-devel openssl-devel openssl zlib zlib-devel pcre-devel
    wget http://openresty.org/download/ngx_openresty-1.7.2.1.tar.gz
    tar -zxvf ngx_openresty-1.7.2.1.tar.gz
    cd ngx_openresty-1.7.2.1
    ./configure --prefix=/opt/openresty \
            --with-pcre-jit \
            --with-ipv6 \
            --without-http_redis2_module \
            --with-http_iconv_module \
            -j2
    make && make install
    ln -s /opt/openresty/nginx/sbin/nginx /usr/sbin/
修改openresty的默认配置文件，配置文件在/opt/openresty/nginx/conf/nginx.conf，修改为如下内容，文件是精简的配置，不要用于生产环境，主要就看server那段配置的内容。

    worker_processes 1;
    events {
        worker_connections  1024;
    }
    http {
        include       mime.types;
        default_type  application/octet-stream;
        server_names_hash_bucket_size 64;
        access_log off;
    
        sendfile        on;
        keepalive_timeout  65;
    
        server {
            listen 3001;
            location / {
              proxy_pass http://127.0.0.1:8000;
              proxy_redirect default;
              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
              proxy_set_header Connection $http_connection;
              proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header Host $http_host;
            }
        }
    }
执行命令nginx就将openresty运行起来，然后打开浏览器，输入主机IP:3001就可以正常访问之前启动的Node.js访问计数应用。

另外如果遇到在Container里无法解析域名，则需要手动增加dns服务器，方法如下：

    DOCKER_OPTS=" --dns 8.8.8.8"
    service docker restart