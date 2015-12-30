---
layout: post
title: vim常用命令
category: vim
keywords: vim
---

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
