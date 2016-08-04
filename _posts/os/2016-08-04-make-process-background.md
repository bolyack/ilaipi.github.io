---
layout: post
title: 启动后台运行进程
category: 操作系统
keywords: 后台运行 进程
---

doing the following steps:

 1. ssh [server]
 2. command
 3. CTRL+Z
 4. bg
 5. disown
 6. exit

Step 3 pauses the current process (e.g. my 'mv' command).
Step 4 puts the paused process in to the background and resumes it.
Step 5 lets you disown the process.

