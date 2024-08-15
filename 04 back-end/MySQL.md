# 一、基础

双版本安装

mysql5

```ini
[mysqld]
# 设置3306端口
port=3306

basedir=D:\SoftWare\resourse\mysql-5.7.37

datadir=D:\SoftWare\resourse\mysql-5.7.37\data

# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
# character-set-server=utf8mb4
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysqL_native_password”插件认证
# default_authentication_plugin=mysql_native_password
# 修改mode
# sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION'
[mysql]
# 设置mysql客户端默认字符集
# default-character-set=utf8mb4
[client]
# 改置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8mb4
```

mysql8
```ini
[mysqld]
# 设置3307端口
port=3307

basedir=D:\SoftWare\resourse\mysql-8.0.27

datadir=D:\SoftWare\resourse\mysql-8.0.27\data

# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
# character-set-server=utf8mb4
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysqL_native_password”插件认证
# default_authentication_plugin=mysql_native_password
# 修改mode
# sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION'
[mysql]
# 设置mysql客户端默认字符集
# default-character-set=utf8mb4
[client]
# 改置mysql客户端连接服务端时默认使用的端口
port=3307
default-character-set=utf8mb4
```

## 00 数据库相关概念

### 001 DB

全称 DataBase，==数据库==，存储==数据的仓库==，数据是有组织的进行存储。

### 002 DBMS

全称 DataBase Management System，==数据库管理系统==，操纵和管理数据库的==大型软件==。

### 003 SQL-Structured Query Language

全称 Structured Query Language，==结构化查询语言==，操作关系型数据库的==编程语言==，定义了一套操作关系型数据库统一标准。

## 01 MYSQL-本地配置

## 02 

## 03 SQL-通用语法

### 001 单行或多行

SOL语句可以单行或多行书写，以分号结尾。

### 002 可读性

SQL语句可以使用空格/缩进来增强语句的可读性。

### 003 大小写

MySQL数据库的SQL语句不区分大小写，关键字建议使用大写。

### 004 注释

单行注释：<kbd>--</kbd>注释内容或<kbd>#</kbd>注释内容（MySQL特有）

多行注释：<kbd>/*</kbd>注释内容<kbd>*/</kbd>

# 二、 DDL

## 1. 概述

全称：Data Definition Language，数据定义语言，用来定义==数据库对象==（数据库，表，字段)，是对表中的结构进行操作，不涉及到数据的查询，如对表的结构与字段进行[[DDL#03 表修改|修改]]。

## 2. 数据库操作

### 01 数据库查询

**查询所有数据库**

```mysql
SHOW DATABASES;
```

**查询当前数据库**

```mysql
SELECT DATABASE();
```

### 02 数据库创建

```mysql
CREATE DATABASE IF NOT EXISTS 
DBName
DEFAULT CHARSET utf8mb4;
```

### 03 数据库删除

```mysql
DROP DATABASE IF EXISTS DBName;
```

### 04 数据库使用

```mysql
USE DBName
```

## 3. 表操作

### 01 表查询

**查询当前数据库所有表**

```mysql
SHOW TABLES;
```

**查询表结构**

```mysql
DESC TABLE TBName;
```

**查询指定表的建表结构**

```mysql
SHOW CREATE TABLE TBName;
```

### 02 表创建

```mysql
CREATE TABLE TBName(
	id int COMMENT '注释',
	name varchar(5) COMMENT '注释'
)CHARACTER SET utf8mb4 COLLATE UTF8_BIN ENGINE = MyISAM COMMENT '注释';
```

### 03 表修改

**表-添加字段**

```mysql
ALTER TABLE TBName ADD 字段 新数据类型(长度) COMMENT '注释' 约束;
```

**表-修改数据类型**

```mysql
ALTER TABLE TBName MODIFY 字段 数据类型(长度);
```

**表-修改字段名和数据类型**

```mysql
ALTER TABLE TBName CHANGE 旧字段名 新字段名 数据类型(长度) COMMENT '注释' 约束;
```

**表-删除字段**

```mysql
ALTER TABLE TBName DROP 字段;
```

**表-修改表名**

```mysql
ALTER TABLE TBName RENAME TO NewTBName;
```

**表-修改字段位置**

```mysql
#移动到某一字段前面
ALTER TABLE TBName MODIFY COLUMN 字段1 数据类型(长度) AFTER 字段2

#移动到表最前面
ALTER TABLE TBName MODIFY COLUMN 字段 数据类型(长度) FIRST;
```

**表-修改存储引擎**

```mysql
ALTER TABLE TBName ENGINE = MyISAM;
```

**表-删除主键或外键**

```mysql
#删除主键
ALTER TABLE TBName DROP PRIMARY KEY;
#删除外键
ALTER TABLE TBName DROP FOREIGN KEY KeyName;
```

### 04 表删除

**表-删除**

```mysql
DROP TABLE IF EXISTS TBName;
```

**表-删除表并重新创建表结构**

```mysql
TRUNCATE TABLE TBName;
```

# 三、[[DML]]

## 1. 概述

全称：Data Manipulation Language，数据操作语言，用来对数据库==表中的数据==进行增删改查。

## 2. 表添加数据

**给指定字段添加数据**

```mysql
INSERT INTO TBName(field1, field2, ...) VALUES(val1, val2, ...);
```

**给全部字段添加数据**

```mysql
INSERT INTO TBName VALUES(val1, val2, ...);
```

**批量添加数据**

```mysql
INSERT INTO TBName(field1, field2, ...) 
VALUES(val1, val2, ...), (val1, val2, ...), ...;
```

```mysql
INSERT INTO TBName
VALUES(val1, val2, ...), (val1, val2, ...), ...;
```

## 3. 表修改数据

```mysql
UPDATE TBName SET 
	field1 = val1, field2 = val2, ... 
WHERE 条件;
```

## 4. 表删除数据

### 01 删除数据

```mysql
#若没有条件则删除全部数据
DELETE FROM TBName
WHERE 条件;
```

### 02 删除某一字段的值

```mysql
UPDATE TBName
SET field = null
WHERE field = val;
```

# 四、[[DQL - 单表查询]]

全称：Data Query Language，数据查询语言，用来==查询数据库中表==的记录。

# 五、[[DQL - 多表查询]]

# 六、DCL

全称：Data Control Language，数据控制语言，用来创建数据库用户、控制数据库的访问权限。

# 七、约束

保证了数据库中数据的正确性、有效性和完整性

## 1. 非空约束 --- NOT NULL

保证列中所有数据不能有null值 **not null**；

## 2. 唯一约束 --- UNIQUE

保证列中所有数据各不相同 **unique**；

## 3. 主键约束 --- PRIMARY KEY

主键是一行数据的唯一标识，要求非空且唯一 **primary key**；

## 4. 检查约束 --- CHECK

保证列中的值满足某一条件 **check**

## 5. 默认约束 --- DEFAULT

保存数据时，未指定值则采用默认值 **default**；

## 6. 外键约束 --- FOREIGIN

外键用来让两个表的数据之间建立链接，保证数据的一致性和完整性

### 01 创建表时添加外键约束

```mysql
CREATE TABLE TBName(
	列名 数据类型,
	...
	CONSTRAINT 外键名称 FOREIGN KEY(外键列名) REFERENCES 主表(主表列名)
);
```
### 02 建完表后添加外键约束

```mysql
ALTER TABLE TBName ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名称) REFERENCES
主表名称(主表列名称)
```

### 03 删除约束

```mysql
#删除外键
ALTER TABLE TBName DROP FOREIGN KEY KeyName;
```

### 04 外键删除更新行为

1. NO ACTION
	当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与RESTRICT一致)
2. RESTRICT
	当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与NOACTION一致)
3. CASCADE
	当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录。
4. SET NULL
	当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为nul（这就要求该外键允许取nu)）。
5. SET DEFAULT
	父表有变更时，子表将外键列设置成一个默认的值（Innodb不支持)

## 006 语句

```mysql
ALTER TABLE TBName ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名称) REFERENCES
主表名称(主表列名称) ON UPDATE CASCADE ON DELETE CASCADE;
```

# Like

## 01 查看

### 001 当前系统的默认字符集

```mysql
show variables like '%character%';
```

### 002 所有的字符集和字符集默认的校对规则

```mysql
desc information_schema.character_sets;
```

### 003 所有可用的字符集

```mysql
show character set;
```

### 001 查看数据库编码

```mysql
show character set;
```

### 002 查看数据库存储路径

```mysql
show variables like '%datadir%';
```

### 003 数据库的字符集

```mysql
show variables like 'character_set_database';
```

### 004 字符集默认的校对规则

```mysql
show variables like 'collation_database';
```


## 02 修

### 001 修改数据库的存储位置

[链接](https://blog.csdn.net/wjr1229/article/details/127997181)

1. 查看数据库存储路径
   `show variables like '%datadir%';`

2. 停止服务
   `net stop MySQL80`

3. 修改安装目录下的my.ini 文件
   datadir=D:/Data

4. 重启服务
   `net start MySQL80`

## 03 备份

[MySQL数据库备份的命令](https://blog.csdn.net/weixin_51079220/article/details/128436362)

## 001

1. 如果有10个不同的实体集，它们之间存在着12个不同的==二元联系==（二元联系是指两个实体集之间的联系），其中3个1:1联系，4个1:N联系，==5个M:N联系==，那么根据ER模型转换成关系模型的规则，这个ER结构转换成的关系模式个数至少有多少个？为什么？
   - 答：10个实体类型+5个M:N联系类型=15个，至少是15个；10个实体类型+12个二元关系=22个，至多是22个；所以范围是15个到22之间。

2. dd

