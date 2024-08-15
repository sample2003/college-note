
# 000 概述

## 01 概述

从多张表中查询数据。

## 02 笛卡尔积

笛卡尔乘积是指在数学中，两个集合A集合和B集合的所有组合情况。（在多表查询时，需要消除无效的笛卡尔积)

# 001 多表关系

## 01 一对一

### 001 关系
一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其它详情字段放在另一张表中，以提升操作效率。

### 002 实现
在任意一方建立外键，关联另外一方的主键，并设置外键为唯一的。

## 02 一对多

### 001 关系
一个部门对应多个员工，一个员工对应一个部门。

### 002 实现
在多的一方建立外键，指向一的一方的主键。

## 03 多对多

### 001 关系
一个学生可以选修多门课程，一门课程也可以供多个学生选择。

### 002 实现
建立第三张中间表，中间表至少包含两个外键，分别关联两方主键。

# 002 内连接

## 01 查询部分

查询A、B交集部分数据

## 02 隐式内连接

### 001 语法
```mysql
SELECT field FROM TBName1, TBName2 WHERE 条件;
```

### 002 实例
```mysql
SELECT t1.name, t2.name FROM TBName1 t1, TBName2 t2 WHERE t1.id = t2.id;
```

## 03 显示内连接

### 001 语法
```mysql
#INNER 可省略
SELECT field FROM TBName1 INNER JOIN TBName2 ON 条件;
```

### 002 实例
```mysql
SELECT t1.name, t2.name FROM TBName1 t1 JOIN TBName2 t2 ON t1.id = t2.id;
```

# 003 外连接

## 01 左外连接

### 001 查询部分

查询左表的所有数据，以及两张表交集部分数据

### 002 语法
```mysql
#OUTER 可省略
SELECT field FROM TBName1 LEFT OUTER JOIN TBName2 ON 条件;
```

## 02 右外连接

### 001 查询部分

查询右表的所有数据，以及两张表交集部分数据

### 002 语法
```mysql
SELECT field FROM TBName1 RIGHT OUTER JOIN TBName2 ON 条件;
```

# 004 自连接

## 00 概述

- 自连接查询，可以是内连接查询，也可以是外连接查询

- 当前表与自身的连接查询，自连必须使用表别名

## 01 语法
```mysql
SELECT field FROM TBName1 JOIN TBName1 别名 ON 条件;
```

# 005 联合查询

## 01 UNION

### 语法
```mysql
SELECT field FROM TBName1 ...
UNION 
SELECT field FROM TBName2 ...;
```

## 02 UNION ALL

### 语法
```mysql
SELECT field FROM TBName1 ...
UNION ALL
SELECT field FROM TBName2 ...;
```

## 03 注意

对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致。

# 006 子查询

## 00 概述

- SQL语句中嵌套SELECT语句，称为嵌套查询，又称子查询
- 子查询外部的语句可以是INSERT / UPDATE / DELETE / SELECT 的任何一个

## 01 据查询结果不同，分为

### 001 [[DQL - 多表查询#02 标量子查询|标量子查询]]

子查询结果为==单个值==

### 002 [[DQL - 多表查询#03 列子查询 | 列子查询]]

子查询结果为==一列==（可以是多行）

### 003 [[DQL - 多表查询#04 行子查询 | 行子查询]]

子查询结果为==一行==

### 004 [[DQL - 多表查询#05 表子查询 | 表子查询]]

子查询结果为==多行多列==

## 02 标量子查询

### 001 操作符

- =, <>, >, >=, <, <=

### 002 语句

```mysql
SELECT * FROM TBName1 t1 
WHERE id = (SELECT * FROM TBName2 t2 WHERE id = 1);
```

## 03 列子查询

### 001 操作符

#### 01 IN
在指定的集合范围之内，多选一

#### 02 NOT IN
不在指定的集合范围之内

#### 03 ANY 
子查询返回列表中，有任意一个满足即可

#### 04 SOME
与ANY等同，使用SOME的地方都可以使用ANY

#### 05 ALL
子查询返回列表的所有值都必须满足

### 002 语句

```mysql
# IN
SELECT * FROM TBName1 t1 
WHERE id in (SELECT * FROM TBName2 t2 WHERE id = 1 or id = 2);

# ALL
SELECT * FROM TBName1 t1 
WHERE price > ALL (SELECT price FROM TBName1 t1
				   WHERE id = (SELECT id FROM TBName2 t2 
				   WHERE Name = "zhangsan"));

# SOME ANY
SELECT * FROM TBName1 t1
WHERE price > ANY (SELECT price FROM TBName1 t1
				   WHERE id = (SELECT id FROM TBName2 t2 
				   WHERE Name = "zhangsan"));
```

## 04 行子查询


### 001 操作符

- =, <>, IN, NOT IN

### 002 语句

```mysql
SELECT * FROM TBName1 t1 
WHERE id = (SELECT * FROM TBName2 t2 WHERE id = 1);
```


## 05 表子查询