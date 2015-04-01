---
layout: post
title: ubuntu$PATH设置错误后...
category: 操作系统
keywords: ubuntu $PATH
---

今天把`mongodb`数据库放在一台Linux服务器上(centos6.5)，然后设置环境变量。
当时一时疏忽，写了

```
$PATH=$MONGO_HOME/bin
```

然后就`:wq`了，并且执行了`source /etc/profile`
然后就悲剧了。基本上所有命令都不管用了，包括`vi`。

---

突然想起来，我可以把文件下载到本地，改好之后再放上去。
我也这么做了。结果放回去之后，执行`source /etc/profile`，
提示：

```
-bash : id command is not found
-bash : tty command is not found
```

大概是这么两句。

我又这么做了：
把`/root/.bash_profile`下载到本地，改为：

```
$PATH=/usr/bin:/usr/sbin:/bin:/sbin
```

执行`source .bash_profile`后，再执行`source /etc/profile`，成功。
但是这时候`vi`命令还不能用。
我就`reboot`了一下。
启动后发现`vi`也能用了。
真是虚惊一场。

不过后来在网上也发现说，可以直接执行：

```
export PATH=/usr/bin:/usr/sbin:/bin:/sbin
```

恢复命令的暂时可用，在本机就可以还原。
下次再碰到，可以试试～～