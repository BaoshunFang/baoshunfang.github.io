---
layout: post
title:  Mysql常用命令
categories: [Mysql]
tags: [Mysql]
---

### 登陆

1. 输入Mysql -u*UserName* -p
2. 按回车
3. 输入密码

### 增加新用户

格式：**grant 权限 on 数据库.* to 用户名@登陆主机 identified by "密码"** 

示例:

```
# 只在本地登陆
grant select,insert,update,delete on *.* to user1@localhost Identified by "password1";
# 在任何机器都可以登陆
grant select,insert,update,delete on *.* to user1@% Identified by "password1";
# 只允许访问mydb，且不设置密码
grant select,insert,update,delete on mydb.* to user1@localhost Identified by "";
```

### 操作数据库 

#### 显示数据库列表

`show databases;` 

#### 显示数据库中的数据表 

```
use mydb;
show tables;
```

#### 显示数据表的结构 

describe 表名; 

#### 建库与删库 

```
create database 库名;
drop database 库名;
```

#### 建表与删表 

```
use 库名;
CREATE TABLE `mf_fd_cache` (
  `id` bigint(18) NOT NULL AUTO_INCREMENT,
  `dep` varchar(3) NOT NULL DEFAULT '',
  `arr` varchar(3) NOT NULL DEFAULT '',
  `flightNo` varchar(10) NOT NULL DEFAULT '',
  `flightDate` date NOT NULL DEFAULT '1000-10-10',
  `flightTime` varchar(20) NOT NULL DEFAULT '',
  `isCodeShare` tinyint(1) NOT NULL DEFAULT '0',
  `tax` int(11) NOT NULL DEFAULT '0',
  `yq` int(11) NOT NULL DEFAULT '0',
  `cabin` char(2) NOT NULL DEFAULT '',
  `ibe_price` int(11) NOT NULL DEFAULT '0',
  `ctrip_price` int(11) NOT NULL DEFAULT '0',
  `official_price` int(11) NOT NULL DEFAULT '0',
  `uptime` datetime NOT NULL DEFAULT '1000-10-10 10:10:10',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uid` (`dep`,`arr`,`flightNo`,`flightDate`,`cabin`),
  KEY `uptime` (`uptime`),
  KEY `flight` (`dep`,`arr`),
  KEY `flightDate` (`flightDate`)
) ENGINE=InnoDB  DEFAULT CHARSET=gbk;
drop table 表名;
```

#### 插入数据 

```
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
# 如果数据是字符型，必须使用单引号或者双引号，如"value"
```

#### 查询数据 

```
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
```

#### 更新数据 

```
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

#### 删除数据 

````
DELETE FROM table_name [WHERE Clause]
truncate table table_name
````

### 导出和导入数据 

#### 导出导入整个数据库 

```
mysqldump -u root -p dbname > mysql.dbname # 回车后输入密码
mysql -u root -p < mysql.dbname #回车后输入密码
```

#### 导出导入某段数据 

```
SELECT a,b,a+b INTO OUTFILE '/tmp/result.text'
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
FROM test_table;
LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl
  -> FIELDS TERMINATED BY ','
  -> LINES TERMINATED BY '\n';

在写出的时候会出现The MySQL server is running with the --secure-file-priv option so it cannot execute this statement的错误解决方法：

出现这个错误是因为没有给数据库指定写出文件的路径或者写出的路径有问题。

首先使用下面的命令 show variables like '%secure%'; 查看数据库的存储路径。如果查出的 secure_file_priv 是 null 的时候就证明在 my.ini 文件里面没有配置写出路径。

这时候就可以在 mysql.ini 文件的 [mysqld] 代码下增加 secure_file_priv=E:/TEST 再重启 mysql 就可以了。然后在导出的地址下面写上刚才配置的这个地址 eg: select * from tb_test into outfile "E:/TEST/test.txt"；就可以了。
```







