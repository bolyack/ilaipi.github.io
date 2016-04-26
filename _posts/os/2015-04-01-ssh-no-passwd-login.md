---
layout: post
title: ssh免密码登录
category: 操作系统
keywords: ssh server
---

## 目的

在本机通过一个命令直接登录服务器，不需要输入密码。

## 实现

### 生成ssh密钥

  在本机执行：
  `ssh-keygen`

### 把公钥上传到服务器

  在本机执行：
  `scp .ssh/id_rsa.pub user@xxx.xxx.xxx.xxx:~/.ssh/xxxx.pub`

### 把公钥写入服务器上的authorized_keys

  在服务器上执行：
  `cat ~/.ssh/xxxx.pub >> ~/.ssh/authorized_keys`

### 创建config文件

  在本机.ssh目录创建'config'文件 `vim .ssh/config`

  内容：

  ```
  Host 221
    HostName 192.168.100.221
    User ncd
    IdentityFile ~/.ssh/id_rsa
  ```

### 使用

  在本机终端：`ssh 221`

## 参考：

 - [Linux/UNIX下使用ssh-keygen设置SSH无密码登录](http://blog.csdn.net/leexide/article/details/17252369)

 - [How to create an ssh connection Terminal shortcut on Mac OS X 10.6.8 (Snow Leopard)?](http://superuser.com/questions/76193/how-to-create-an-ssh-connection-terminal-shortcut-on-mac-os-x-10-6-8-snow-leopa)
