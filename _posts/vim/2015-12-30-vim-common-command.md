---
layout: post
title: vim常用命令
category: vim
keywords: vim
---

参考： [简明 Vim 练级攻略](http://coolshell.cn/articles/5426.html)

## 替换

把所有行的 `search` 替换为 `replacement`

其中，`\r`在`replacement`中表示换行

```
:%s/search/replacement
:10,20s/search/replacement    //指定10-20行之间匹配的进行替换
```

## 删除空行

把所有空白行删掉

```
//仅空白行
:g/^$/d
:v/./d
:10-20g/^$/d                  //指定10-20行之间,其它相同
//仅包含空白符也算空白行
:g/^\s*$/d
:v/\S/d
```

## 宏录制

记录一系列操作，快速重复

输入 `qa` 开始录制宏，记录在寄存器 `a` (命名为 `a`)

做任何需要的，完成后在 `Normal` 模式按 `q` 结束录制

`@a` 在当前光标下重复 `a` 宏
`@@` 在当前光标下重复 刚刚录制的宏
`10@@` 在当前光标下重复10次刚刚录制的宏


## 多光标操作

标记多个相同的文本，统一操作。常用于局部某变量重命名

使用插件： [terryma/vim-multiple-cursors](https://github.com/terryma/vim-multiple-cursors)

可以先使用 `Visual Mode` 选中需要操作的，然后`Next Key` (<C-m/n>) 选中下一个
