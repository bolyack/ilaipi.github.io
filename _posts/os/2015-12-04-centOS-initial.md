---
layout: post
title: Linux crontab
category: 操作系统
keywords: cron job
---

本机环境： `ubuntu 12.04`
virtubox: `4.2`
centOS镜像: `CentOS-6.3-x86_64-minimal`

1. 安装比较顺利，没有问题，过程中设置了root的密码。  
2. 安装后登录，此时只有root用户，密码安装过程中设置了。
3. 用root登录后创建分组、用户。
4. 这时候可能不能上网，解决方法为：[通过virtualbox最小化安装centos 6.3后无法上网解决办法](http://www.2cto.com/os/201210/162538.html)
5. 安装wget。`yum install wget.x86_64`
6. 安装bash-completion。这个需要先安装一个软件仓库，我装了EPEL6的仓库。  
  （[EPEL6](https://fedoraproject.org/wiki/EPEL "EPEL仓库介绍")）  
首先`wget http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm`
然后`rpm -ivh epel-release-6-8.noarch.rpm`
`yum search bash-completion`
`yum install bash-completion.noarch`
安装完成后需要重启一下服务器。  
7. 安装vim  
`yum install vim-X11 vim-common vim-enhanced vim-minimal`
8. 源码安装postgreSQL  
首先，下载安装包。`wget http://ftp.postgresql.org/pub/source/v9.3.1/postgresql-9.3.1.tar.gz`
解压。
