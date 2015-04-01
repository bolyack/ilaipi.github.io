---
layout: post
title: ubuntu安装mysql
category: 开发环境
keywords: ubuntu mysql
---

## 1. 使用apt-get安装

执行：

```
sudo apt-get install mysql-server mysql-client
```

## 2. 设置编码

执行：

```
sudo vim /etc/mysql/my.cnf
```

找到客户端配置```[client]``` 在下面添加

```
default-character-set=utf8
```

在找到```[mysqld]``` 添加

```
character-set-server=utf8
```

找到```[mysql]```添加

```
default-character-set=utf8
```

## 3. 重启mysql服务

执行：

```
sudo service mysql restart
```

## 4. 查看编码

执行：

```
mysql -uroot -p
//输入root的密码
show variables where Variable_name like "%chara%";
```

# 注意

在修改编码前创建的表，修改编码之后，表的编码并不会被改变，所以再向表里插入数据还是会乱码。最简单的解决办法是把表删除了重建。
建议所有建表、建库语句都带上编码设置，如：

```
//create db:
CREATE DATABASE IF NOT EXISTS db_name 
DEFAULT CHARSET utf8 COLLATE utf8_general_ci;

//create table:
create table IF NOT EXISTS table_name(
 id int(10) not null primary key auto_increment
)DEFAULT CHARACTER SET = utf8;
```
