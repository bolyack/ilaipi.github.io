---
layout: post
title: ubuntu安装ssh服务
category: 操作系统
keywords: ubuntu ssh server 龙芯笔记本 8089D
---

在ubuntu12.04上安装ssh，参考：[服务器上安装ssh](http://blog.istef.info/2008/10/02/setup-ssh-server-on-ubuntu-serverubuntu)。

我的环境是:

1. 主机  `Thinkpad T420 ubuntu12.04`    通过无线上网  
通过`ifconfig`看，无线网卡`wlan0`，IP地址为`192.168.0.102`
2. 虚拟机  centOS 6.3 minimal 运行于主机上  
3. 客户端  龙芯笔记本8089D  原装系统  

按照前面教程很容易的安装好了。  
我在虚拟机中通过`ssh 192.168.0.102 -l uname`，是可以连接成功的。  
但是，我在客户端就是不能成功，提示：`No Route to Host`

网上找，大部分说的是关闭防火墙。但是，ubuntu自带就不开防火墙啊。。

我发现的解决方案：

```
sudo vim /etc/network/interfaces
```

找到你正使用的网卡，一般如果是有线就是`eth0`，无线`wlan0`，  
我的：`auto wlan0`，可能找不到，就是没有。如果找到了，基本就不是我遇到的这种情况，不用看了。

找不到，那么就在最下面加上：  

```
auto wlan0
iface wlan0 inet dhcp
```

然后保存，执行： 
 
```
sudo /etc/init.d/networking restart
```

重新在客户端连，会有一个提示，直接写yes，成功。