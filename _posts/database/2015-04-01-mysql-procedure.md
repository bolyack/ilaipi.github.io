---
layout: post
title: mysql存储过程基础
category: 数据库
keywords: mysql procedure
---

## 相关资料
>[mysql5.1存储过程官方中文文档](http://dev.mysql.com/doc/refman/5.1/zh/stored-procedures.html#declare)

##个人总结

####1.if语句必须有then。e.g. `if a>0 then set a = 0; end if;`

####2.`row_count()` 得到前一句查询的结果数

####3.`LAST_INSERT_ID()` 得到最后一次insert的记录的`auto_increment`列的值

####4.可以用`begin ... end` 块组织一段代码，，可以嵌套。

####5.常用三种类型的对象，变量、游标、处理器。e.g.

```sql
//所有声明语句必须在begin、end块的开始部分，并且有顺序限制：
declare var_name type [default value];//变量必须在最前
declare cur_name cursor for select from table_name;
declare continue handler for sqlexception set var_name=1;//处理器主要是用于对循环的控制
```

####6.循环语句

```
/**
* 在使用循环语句时，可能会发现一个问题，就是最后一条记录会被遍历两次。
* 解决办法是在循环体外先开始fetch，然后在循环体的结尾再来一句
*/
begin
    declare userID int;
    declare done int default 0;
    declare user_cur cursor for select id from t_user;
    declare continue handler for not found set done=1;
    open user_cur;
    fetch user_cur into userID;//fetch
    while !done do
        -- while statement
        fetch user_cur into userID;//fetch
    end while;
    close user_cur;
end;
```