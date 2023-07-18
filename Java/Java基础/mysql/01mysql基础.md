# 一、MySQL概述

1、MySQL是关系型数据库管理系统。所谓关系型数据库就是基于二维表结构的数据库。每一个数据库（Database）中是有很多表格（Table），每一个表格中有很多列/字段（column、field），和很多的行/记录（line、record）。



2、MySQL是基于TCP/IP协议的网络应用程序，是C/S结构，服务器端默认端口号是3306，客户端可以有很多种：

- 命令行客户端
- 可视化工具：SQLyog、Navicat、DBeaver、Workbench等
- Java程序
- 其他程序



# 二、MySQL安装、登录

1、MySQL安装要注意

（1）使用管理员权限安装和操作

（2）避免计算机的用户名/设备名中文

（3）避免安装目录出现中文汉字和中文的标点符号等



2、MySQL客户端登录

无论哪一种客户端，都需要提供这些信息：

MySQL服务在哪个主机下，端口号是什么，用户名和密码是什么。

```cmd
mysql -h localhost -P 3306 -u root -p回车
Enter password：输入密码
```



# 三、SQL分类和规范

1、SQL分类

DDL：用来创建库、表等SQL语句

DML：增删改查，其中查询是SELECT，它非常重要，所以单拎出来称为DQL。

DCL：关于事务控制、权限控制等。

其他：像use、show等命令。



2、规范

- 关于mysql的语法是不区分大小写；关键字习惯上是大写。
- 关于mysql表中的数据是否区分大小写，是要看库和表的编码和校对规则；
- 同一个mysql服务器中数据库名不能重名，同一个数据库中表不能重名，同一个表中字段不能重名。
- 自己给数据库、表、字段等命名时，尽量不要使用关键字、敏感字等
- 标点符号使用英文状态下半角输入，该成对的一定要成对。



# 四、基本的SELECT语句

```mysql
select 常量;
select 变量;
select 表达式;
```

```mysql
select * from 数据库名.数据表名;

use 数据库名;
select * from 数据表名;
```

```mysql
select 字段1,字段2 from 数据表名;
```

```mysql
select 字段1,字段2 from 数据表名 where 条件;
```

```mysql
select 字段1 as 别名1, 字段2 as 别名2 from 数据表名 as 表别名 where 条件;

字段的别名，如果包含空格，可以加“”，当然能不包含空格更好。
表的别名是绝对不可以包含空格，也不能加“”。
as都是可以省略的。
```

```mysql
select distinct 字段1,字段2 from 数据表名 where 条件;

distinct：去重复
```



# 五、MySQL运算符

```mysql
算术运算符：
加：+
	Java中+可以用于表示求和、字符串的拼接。
	MySQL中+只表示求和，不表示拼接。
减：-
乘：*
除：/  正常除
  div  只保留商的整数部分
模：%
```

```mysql
比较运算符：
大于：>
小于：<
大于等于：>=
小于等于：<=
等于：=
	mysql中没有==
不等于： != 、 <>
```

```mysql
区间范围、集合范围的判断
x between a and b 判断x的值是否在[a,b]范围内
x in (值1，值2...) 判断x的值是否在()范围内

x not between a and b 判断x的值不在[a,b]范围内
x not in (值1，值2...) 判断x的值不在()范围内
```

```mysql
模糊查询的匹配判断
like关键字，可以配合两个通配符
%：代表0-n位的字符
_：代表1位字符
```

```mysql
逻辑运算符：
逻辑与：&& 、and
逻辑或：|| 、or
逻辑非：! 、not
逻辑异或：xor
```

```mysql
关于null值的判断和处理
x is null
x is not null
x <=> null
!(x <=> null)

ifnull(x, value)：如果x是null，用value值代替
```





