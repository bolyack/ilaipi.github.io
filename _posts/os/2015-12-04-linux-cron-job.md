---
layout: post
title: Linux crontab
category: 操作系统
keywords: cron job
---

### A 执行`crontab -e`,打开任务配置文件.

```
  以`root`用户执行 则以`root`用户执行命令
  以其它用户执行 则以其它用户执行命令
```

### B 在最下面添加:

```
0 4 * * * cd /opt/his2ckd/acquisition && java -jar ckd-acquisition-1.0-SNAPSHOT.jar update
```

`command`部分如果没有执行`cd`而直接`java -jar /opt/his2ckd/acquisition/ckd-acquisition-1.0-SNAPSHOT.jar update`那么日志将不能记录在`/opt/his2ckd/acquisition/logs`文件夹中

参考:[debian cron task](https://www.debian-administration.org/article/56/Command_scheduling_with_cron)


