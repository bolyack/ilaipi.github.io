---
layout: post
title: debian/ubuntu iptables
category: 操作系统
keywords: iptables
---

参考:[iptables](https://wiki.debian.org/iptables)  可能需要翻墙才能打开
其中自己的配置,在`/etc/iptables.test.rules`除了参考页面提供的部分外,
增加开放80/8080的配置,在
```
-A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT(参考页面标准配置的一句)
```
后面添加:
{% highlight shell %}
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
{% endhighlight %}

然后在COMMIT之后再加上转发80到8080的配置:
```
*nat
-A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
COMMIT
```

修改完成需要执行
```
iptables-restore < /etc/iptables.test.rules
iptables-save > /etc/iptables.up.rules
```
才能生效
