---
layout:     post
title:      Docker install
subtitle:   基本操作
date:       2020-02-21
author:     Cheng
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Docker
---

[TOC]

# Docker install 教程

##  安装依赖包

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

## 下载Docker repo

```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

## 安装Docker

```
yum install docker-ce docker-ce-cli containerd.io
```



# Docker Other

## 查看Docker历史版本

```
yum list docker-ce --showduplicates | sort -r

docker-ce.x86_64  3:18.09.1-3.el7                     docker-ce-stable
docker-ce.x86_64  3:18.09.0-3.el7                     docker-ce-stable
docker-ce.x86_64  18.06.1.ce-3.el7                    docker-ce-stable
docker-ce.x86_64  18.06.0.ce-3.el7                    docker-ce-stable
```
