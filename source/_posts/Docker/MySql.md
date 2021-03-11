---
title: MySql
date: 2021-03-11 21:53:44
categories: [Docker, Images]
---

Mysql 配置

<!-- more-->

## 拉取镜像

```
docker pull mysql
```

## 创建容器

```
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```

- name：容器名，此处命名为mysql
- e：配置信息，此处配置mysql的root用户的登陆密码
- p：端口映射，此处映射 主机3306端口 到 容器的3306端口
- d：后台运行容器，保证在退出终端后容器继续运行

## 连接MySql

```shell
docker exec -it mysql bash
mysql -uroot -p123456
```

## 如果容器运行正常，但是无法访问到MySQL，一般有以下几个可能的原因：

开放端口：
```shell
$ systemctl status firewalld
$ firewall-cmd  --zone=public --add-port=3306/tcp -permanent
$ firewall-cmd  --reload
```

关闭防火墙：
```shell
$ sudo systemctl stop firewalld
需要进入docker本地客户端设置远程访问账号

$ sudo docker exec -it mysql bash
$ mysql -uroot -p123456
mysql> grant all privileges on *.* to root@'%' identified by "password";
```
