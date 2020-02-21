---
layout:     post
title:      Docker制作镜像
subtitle:   基本操作
date:       2020-02-21
author:     Cheng
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - Docker
---

[TOC]

# 制作打包一份Docker镜像

> 首先运行一份docker容器 并且把东西全部制作好
>
> 接着就是查看容器的名字

```
[root@clcdocker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                NAMES
cd5081cbccdf        470671670cac        "bash"              4 minutes ago       Up 4 minutes        0.0.0.0:80->80/tcp   web

[root@clcdocker ~]# docker commit web limitrinno/centos_web:1.0
sha256:67f76cb26c134918de0c6b6dfa7bade4371d806bf13675b5c4eee0d644c484c8

[root@clcdocker ~]# docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
limitrinno/centos_web   1.0                 67f76cb26c13        7 seconds ago       283MB
centos                  latest              470671670cac        4 weeks ago         237MB

上传打包好的镜像
docker login

docker push <name>/<name1>:tag

```



# Dockerfile制作镜像

```
搭建Frp

mkdir frp
cd frp
vi Dockerfile

FROM alpine

RUN apk add --update tzdata
ENV TZ=Asia/Shanghai

ENV FRP_VERSION 0.31.2
RUN wget https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz \
    && tar -xf frp_${FRP_VERSION}_linux_amd64.tar.gz \
    && mkdir /frps \
    && cp frp_${FRP_VERSION}_linux_amd64/frps* /frps/ \
    && rm -rf frp_${FRP_VERSION}_linux_amd64*

# Clean APK cache
RUN rm -rf /var/cache/apk/*

RUN mkdir /conf
VOLUME /conf

WORKDIR /frps
ENTRYPOINT ["./frps","-c","/conf/frps.ini"]

docker build -t limitrinno/frp:1.0
```

