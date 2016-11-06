---
layout: post
title: 阿里云数据库 MongoDB版
category: 数据库
keywords: mongodb aliyun database
---

## 相关资料
>[mongodb manage-users-and-roles](https://docs.mongodb.com/v3.2/tutorial/manage-users-and-roles/)
>[Mongo shell 连接](https://help.aliyun.com/document_detail/44629.html?spm=5176.doc44651.6.126.leW2aJ)
>[公网连接](https://help.aliyun.com/document_detail/44651.html?spm=5176.doc44629.6.128.fwxdy6)

刚创建好的云数据库只有一个`admin`帐号

自己程序用的时候，先创建一个普通的读写权限的帐号:

```javascript
// use your_database_name
db.createUser({
  user: "your_user_name",
  pwd: "your_password",
  roles: ["readWrite"]
});
```
PS: 因为首先`use`了自己的数据库，所以在设置`roles`的时候不需要再设置`db`  
PPS: 执行这个语句必须是 `admin` 用户(或者有创建用户权限的用户)

如果需要只读帐号，只需要把`readWrite`改为 `read`.

然后参考公网连接篇，在阿里ECS上安装 `rinetd` 并配置代理。

然后我在自己的电脑上，创建了两个 `bash aliases` :

```bash
# 可以直接在.bashrc 之类的文件里加
# 我的.bashrc 文件中推荐自定义的别名可以单独一个文件
vim .bash_aliases

// add:
alias cloud_mongo_primary='mongo --host ECS-IP -u YOUR_USER -p YOUR_PWD --port YOUR_PORT --authenticationDatabase YOUR_DB_NAME'
```
