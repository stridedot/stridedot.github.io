---
title: "使用命令行连接到 MySQL"
keywords: ['mysql', 'mysql command', 'mysql connect']
description: 本文介绍了如何使用命令行连接到 MySQL 的常用选项。
date: 2024-06-19T16:57:41+08:00
author: "StrideDot"
slug: mysql-connecting
image: MySQL-Logo.wine.png
math: 
license: 
hidden: false
comments: true
draft: false
tags: ["MySQL"]
categories: ["MySQL"]
---


---


## 命令选项
- `--host=[hostname], -h[hostname]`：指定 MySQL 服务器的主机名
- `--user=[username], -u[username]`：指定 MySQL 服务器的用户名
- `--password=[password], -p[password]`：指定 MySQL 服务器的密码
- `--port=[port], -P[port]`：指定 MySQL 服务器的端口号
- `--protocol=[TCP|SOCKET|PIPE|MEMORY]`：指定 MySQL 服务器的连接协议，`localhost` 默认使用 `unix` 套接字：
    ```shell
    mysql --host=localhost
    ```
    如何要强制使用 TCP 连接，指定 `--protocol=TCP`：
    ```shell
    mysql --host=localhost --protocol=TCP
    ```
    下面是 `--protocol` 选项值及适用平台：

    | 选项     | 传输协议                 | 适用平台       |
    |--------|----------------------|------------|
    | TCP    | 到本地或远程服务器的 TCP/IP 传输 | 所有平台       |
    | SOCKET | Unix 套接字传输到本地服务器     | Unix 平台    |
    | PIPE   | 命名管道传输到本地服务器         | Windows 平台 |
    | MEMORY | 共享内存到本地服务器           | Windows 平台 |



---


## 连接到 MySQL 服务器

### localhost
在不指定任何选项的情况下，调用 `mysql` 命令：
```shell
mysql
```
上面的命令包含以下默认选项：
- 使用默认的主机名 `localhost`
- 使用默认的用户名 `root`
- 未指定密码
- 使用默认的端口号 `3306`

执行上面的命令后会返回：
```shell
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
```
跟下面的命令等价：
```shell
mysql -h localhost -u root
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
```

使用完整的选项连接到 MySQL 服务器：
```shell
mysql --host=localhost --user=root --port=3306 --password 123456
```

在 `Unix` 上，MySQL 会对 `localhost` 使用 `Unix` 套接字连接，可使用 `--socket` 选项指定套接字文件。


### protocol
使用 `--protocol` 选项指定连接协议，即使指定了 `--host=localhost`，也会覆盖前面的规则。
示例：
```shell
sh-4.4# mysql -h localhost -u root --protocol=TCP -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 40
Server version: 8.3.0 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

如果未使用 `--protocol` 选项，`localhost` 默认使用 `Unix` 套接字连接，即使使用 `--port` 来指定端口号。
示例：
```shell
sh-4.4# mysql -h localhost -u root -P1111 -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 41
Server version: 8.3.0 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```


如果要使用 `TCP` 连接，有以下两种方式：
- 使用 `--host` 或 `-h` 指定主机 IP 值 `127.0.0.1`
- 使用 `--protocol=TCP` 指定连接协议

示例如下：
```shell
mysql --host=127.0.0.1
mysql --protocol=TCP
```

指定端口号强制建立 `TCP/IP` 连接，下面两种方式皆可：
```shell
mysql --host=127.0.0.1 --port=13306
mysql --protocol=TCP --port=13306
```