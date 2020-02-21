---
layout:     post
title:      Docker搭建Wordpress步骤
subtitle:   基本操作
date:       2020-02-21
author:     Cheng
header-img: img/post-bg-map.jpg
catalog: true
tags:
    - Docker
---

# Docker简易Nginx配置

```
docker run --name nginx -p 80:80 -v /www/:/usr/share/nginx/html:rw -d nginx

-v 不是很推荐使用 建议使用mount格式
```

## 挂载本地目录到Nginx

```
docekr run -itd --name nginx -p 80:80 --mount src=/www,dst=/usr/share/nginx nginx

可以一直开不同的Docker，用同一个数据卷 扩展能力特别强
```

# 搭建一个wordpress

```
docker network create lnmp
```

```
docker pull mysql

docker run -itd --name lnmp_mysql --net lnmp -p 3306:3306 --mount src=mysql-vol,dst=/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql --character-set-server=utf8

docker exec lnmp_mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD" -e"create database wp"'

会提示 mysql: [Warning] Using a password on the command line interface can be insecure.
意思是 在命令行使用mysql密码会不安全
```

```
docker run -itd --name lnmp_web --net lnmp -p 88:80 -p 443:443 -p 9000:9000 --mount type=bind,src=/www,dst=/var/www/html richarvey/nginx-php-fpm
```