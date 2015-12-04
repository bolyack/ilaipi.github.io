---
layout: post
title: postgresql on ubuntu
category: 操作系统 数据库
keywords: postgresql
---

操作系统：`ubuntu15.04`

#install
`apt-get install postgresql`
执行完这个命令后，会自动创建一个`postgres`的用户
这个用户是数据库的超级管理员，可以不用密码登录
修改密码：

```
sudo -u postgres psql template1 （这是默认的一个数据库）
ALTER USER postgres with encrypted password 'your_password';
```

但可以通过修改配置文件：

`/etc/postgresql/9.x/main/pg_hba.conf`
中以下两行：

```
local   all             postgres                                peer
local   all             all                                     peer
```
其中最后`peer` 改为 `md5`，即用户需要密码才能登录

!!!修改需要重启


#command line

```
sudo -u postgres psql -U username -d dbname -W
```


#add user

```
sudo -u postgres createuser -P username
```

#delete user

```
sudo -u postgres psql -U postgres
drop user username;
```

