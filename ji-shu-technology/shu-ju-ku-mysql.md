---
description: python操作mysql数据库
---

# Pandas操作数据库（Mysql）

## Mysql VS SQLite

*  SQLite: Python自带，不需要额外的安装，轻量级、可嵌入，但不能承受高并发访问，适合桌面和移动应用
* Mysql：**今天的主角**
  * MySQL是为服务器端设计的数据库，能承受高并发访问，同时占用的内存也远远大于SQLite，是Web世界中使用最广泛的
  * 需要额外的安装

## Mysql的安装

[官网](https://dev.mysql.com/downloads/mysql/)下载对应的版本，这里下载的是：MySQL Community Server 8.0.13，按照提示一路next/execute就行

![](../.gitbook/assets/image%20%286%29.png)

Windows上可能需对应的Python，去[python官网](https://www.python.org/downloads/windows/)下载对应版本即可，由于这里安装是在Windows下进行的，关于MAC和Linux的安装，强烈推荐[廖老师的教程](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014320107391860b39da6901ed41a296e574ed37104752000)

## Python操作数据库

由于MySQL服务器以独立的进程运行，并通过网络对外服务，所以，需要支持Python的MySQL驱动来连接到MySQL服务器。MySQL官方提供了mysql-connector-python驱动，但是安装的时候需要给pip命令加上参数`--allow-external`：

```text
$ pip install mysql-connector-python --allow-external mysql-connector-python
```

如果上面的命令安装失败，可以试试另一个驱动：

```text
$ pip install mysql-connector
```

