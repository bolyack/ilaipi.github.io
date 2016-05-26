---
layout: post
title: jar包集成spring之配置文件引入方式
category: java
keywords: java spring
---

## environment  

```
modules:
spring-loader   // 所有spring jar包定义，入口文件定义context.xml
env             // 数据库配置文件定义db-*.properties，spring数据源定义文件db-*.xml
init            // 程序入口
```

### 在`spring-loader`模块中定义：`ApplicationHelper.java`

```
package com.imedpower.sync;

import org.apache.commons.lang3.ArrayUtils;
import org.apache.commons.lang3.StringUtils;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.ArrayList;
import java.util.List;

/**
 * Created by billy on 5/23/16.
 */
public class ApplicationHelper {
    private static ApplicationContext context;

    private ApplicationHelper() {}

    public static <T> T getInstance(Class<T> clazz) {
        return context.getBean(clazz);
    }

    public static <T> T getInstance(String name) {
        return (T) context.getBean(name);
    }

    /**
     * 启动spring，加载必要的配置文件
     * 配置文件名中不能有空格(: 和 文件名之间)
     */
    public static void start(String... contexts) {
        List<String> config = new ArrayList<>();
        config.add("classpath*:context.xml");
        if (ArrayUtils.isNotEmpty(contexts)) {
            for (String context : contexts) {
                if (StringUtils.isNotBlank(context)) {
                    config.add(context);
                }
            }
        }
        context = new ClassPathXmlApplicationContext(config.toArray(new String[]{}));
    }
}
```

### 在`init`模块定义`context.xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-4.0.xsd">
    <context:component-scan base-package="com.imedpower.sync"/>
    <context:annotation-config/>

    <bean id="propertyConfigurer"
          class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
        <property name="locations">
            <list>
                <value>classpath*:db-mongo.properties</value>
                <value>classpath*:db-oracle.properties</value>
            </list>
        </property>
    </bean>
    <!-- 这里 : 和 文件名之间可以有空格 -->
    <!-- 但是好像所有要加载的文件中，import标签只能出现一次 -->
    <import resource="classpath*: db-*.xml"/>
</beans>
```

### 调用

在`Main.java`中，可以通过
```
ApplicationHelper.start("classpath*:db-oracle.xml", "classpath*:db-mongo.xml");
```
启动`spring`

### 总结

关键点：

1. 在代码中指定配置文件名时，:和文件名之间不能有空格
2. 在配置文件中通过`import`标签引入时，不能出现多次
