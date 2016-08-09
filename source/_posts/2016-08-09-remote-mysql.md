---
layout: post
title: 远程访问非标准 MySQL
date: 2016-08-09 11:02:05
comments: true
categories: [MySQL]
---

当使用非标准安装 MySQL 的情况下，如何开启远程访问呢？对这个问题进行了研究。

1. 登录到远程服务器，登录 MySQL：
```
mysql -uroot -ppassword
```
报了下面的错误：
```
Can’t connect to local MySQL server through socket /tmp/mysql.sock
```
原因是 sock 文件不是默认的位置，而是 `/tmp/mysql-generic-5.5.40.sock`，做个软链接解决：
```
ln -s /tmp/mysql-generic-5.5.40.sock /tmp/mysql.sock
```

2. 可以正常登录了，退出到本地，登录发现还是不能访问，还需要修改 MySQL 参数，重启即可：
```
skip_networking: on #开启即启动端口监听，如需要使用IP地址访问请开启
```

---

标准 MySQL 设置详见文章：[MySQL、Postgres 开启远程访问权限](http://wenzhixin.net.cn/2012/05/15/mysql_open_the_remote_access_ubuntu)