---
layout: post
title: ubuntu设置触摸板
category: 操作系统
keywords: ubuntu Touchpad
---

装了ubuntu之后，发现触摸板右边的滚动条不管用了。
今天终于找到了解决办法，赶紧记录下来。
参考：[Touchpad Synaptics (简体中文)](https://wiki.archlinux.org/index.php/Touchpad_Synaptics_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29)

---

在参考页面，有条命令：`man synaptics`可以看到所有触摸板的设置选项。
但是，`/etc/X11/xorg.conf.d/10-synaptics.conf`这个配置文件，系统中是没有的。
在页面最下面看到了这个：

```
synclient -l
```

可以看到当前触摸板的所有设置。
并且，通过

```
synclient var=value
```

可以直接设置值！
于是参考页面上面部分，设置了：

```
synclient VertEdgeScroll=1
synclient HorizEdgeScroll=1
```

然后，右边可以上下滚动，下边可以左右滚动！太棒了～

可以通过[synclient-settings-saver](https://github.com/swook/synclient-settings-saver)实现开机自动设置