---
layout: post
title: maven install jars to local
category: 开发环境
keywords: maven local
---

下载个推的sdk:
[下载地址](http://www.igetui.com/download/server/GETUI_SERVER_SDK.zip)

解压后,进入解压得到的文件夹,执行:

```
    mvn install:install-file -Dfile=gexin-rp-sdk-base-4.0.0.1.jar -DgroupId=com.gexin.platform -DartifactId=gexin-rp-sdk-base -Dversion=4.0.0.1 -Dpackaging=jar
    mvn install:install-file -Dfile=gexin-rp-sdk-http-4.0.0.1.jar -DgroupId=com.gexin.platform -DartifactId=gexin-rp-sdk-http -Dversion=4.0.0.1 -Dpackaging=jar
    mvn install:install-file -Dfile=gexin-rp-sdk-template-4.0.0.1.jar -DgroupId=com.gexin.platform -DartifactId=gexin-rp-sdk-template -Dversion=4.0.0.1 -Dpackaging=jar
    mvn install:install-file -Dfile=jackson-all-1.8.5.jar -DgroupId=com.jackson -DartifactId=jackson-all -Dversion=1.8.5 -Dpackaging=jar
```

参考链接:
[Guide to installing 3rd party JARs](https://maven.apache.org/guides/mini/guide-3rd-party-jars-local.html)
