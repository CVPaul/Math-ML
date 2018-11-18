---
description: python操作mysql数据库
---

# Pandas读写Mysql

## Mysql VS SQLite

*  SQLite: Python自带，不需要额外的安装，轻量级、可嵌入，但不能承受高并发访问，适合桌面和移动应用
* Mysql：**今天的主角**
  * MySQL是为服务器端设计的数据库，能承受高并发访问，同时占用的内存也远远大于SQLite，是Web世界中使用最广泛的
  * 需要额外的安装

## Mysql的安装

[官网](https://dev.mysql.com/downloads/mysql/)下载对应的版本，这里下载的是：MySQL Community Server 8.0.13，按照提示一路next/execute就行

![](../.gitbook/assets/image%20%2814%29.png)

Windows上可能需对应的Python，去[python官网](https://www.python.org/downloads/windows/)下载对应版本即可，由于这里安装是在Windows下进行的，关于MAC和Linux的安装，强烈推荐[廖老师的教程](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014320107391860b39da6901ed41a296e574ed37104752000)，下面的安装过程主要参考廖老师的教程，不在细说，而把重点放在pandas对sql数据的读写

## Python操作数据库

### 支持ORM的数据库接口

`pip install sqlalchemy`

 Anaconda本身带了sqlalchemy，下面使用的也是sqlalchemy，很方便；[这里](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014320114981139589ac5f02944601ae22834e9c521415000)是廖老师的教程

### 不支持ORM的数据库接口（不推荐）

由于MySQL服务器以独立的进程运行，并通过网络对外服务，所以，需要支持Python的MySQL驱动来连接到MySQL服务器。MySQL官方提供了mysql-connector-python驱动，但是安装的时候需要给pip命令加上参数`--allow-external`：

```text
$ pip install mysql-connector-python --allow-external mysql-connector-python
```

如果上面的命令安装失败，可以试试另一个驱动：

```text
$ pip install mysql-connector
```

###  'caching\_sha2\_password' is not support 问题

![](../.gitbook/assets/image%20%2813%29.png)

In MySQL 8.0, `caching_sha2_password` is the default authentication plugin rather than `mysql_native_password`.

#### [解决方案一](https://blog.csdn.net/u010026255/article/details/80062153)

`ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER; #修改加密规则` 

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'; #更新一下用户的密码`

`FLUSH PRIVILEGES; #刷新权限`

`ALTER USER 'root'@'localhost' IDENTIFIED by '123qwe';# 重置一下密码`

#### [解决方案二](https://stackoverflow.com/questions/50243506/caching-sha2-password-is-not-supported-mysql?rq=1)

安装即可：`pip install mysql-connector-pytho` 

### Pandas数据读写mysql

* 从csv文件load数据

![](../.gitbook/assets/image%20%289%29.png)

* 数据写入mysql

![](../.gitbook/assets/image%20%2819%29.png)

* 数据从mysql读出来到padans

![](../.gitbook/assets/image%20%287%29.png)



