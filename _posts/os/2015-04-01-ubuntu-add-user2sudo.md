---
layout: post
title: ubuntu设置用户到sudo组
category: 操作系统
keywords: ubuntu sudo
---

那天装完`virtualbox`，做了个操作 `usermod -G vboxers yyam`，
结果，唯一的`yyam`用户 不能用`sudo`了，提示 不在`sudoers`。

网上找到：[Ubuntu 用户不在sudoers文件中](http://xjhznick.blog.51cto.com/3608584/1537804)

这里面说要进入恢复模式，但没有说怎么进。
网上有说，在`BIOS`画面结束时按`shift`，但试了不行，而是按`esc`。

#必须在BIOS将要结束的时候，按一下esc即可。

进入恢复模式后，就和上面的网页说的一样：
1. 重启进入恢复模式；
2.选择 `fsck` 进入可读写文件模式(`exit read-only mode`)
3.选择 `root Drop to root shell prompt`
4.$ `usermod -a -G sudo yyam`

第二步如果不执行，直接执行第3步，还是不能成功的，所以第二步不能少。