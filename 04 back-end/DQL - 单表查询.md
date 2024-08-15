
# 000 DQL 概述

## 01 全称：Data Query Language

数据查询语言，用来查询数据库中表的记录。

# 001 基本查询

## 01 查询多个字段

```mysql
SELECT * FROM TBName;
SELECT field1, field2, ... FROM TBName;
```

## 02 查询字段并去除重复记录

```mysql
SELECT DISTINCT field FROM TBName;
```

## 003 查询字段并起别名

```mysql
SELECT field AS OName FROM TBName;
```

# 002 条件查询

## 01 语法

```mysql
SELECT * FROM TBName WHERE condition;
```

## 02 条件

### 001 大于 >

```mysql
#查询年龄大于20岁的学员
SELECT * FROM TBName WHERE age > 20;
```
### 002 大于等于 >=

```mysql
#查询年龄大于等于20岁的学员信息
SELECT * FROM TBName WHERE age >= 20;
```
### 003 并且 && --- and

```mysql
#查询年龄大于等于20岁井且 年龄 小于等于 30岁 的学员信息
SELECT * FROM TBName WHERE age >= && age<= 30;
SELECT * FROM TBName WHERE age >= AND age<= 30;
```
### 004 在...之间 between

```mysql
#查询年龄在19到21之间的学员信息
SELECT * FROM TBName WHERE age BETWEEN 19 AND 21;
```
### 005 相等 =

```mysql
#查询年龄等于18岁的学员信息
SELECT * FROM TBName WHERE age = 18;
```
### 006 不等 <> --- !=

```mysql
#查询年龄不等于18岁的学员信息
SELECT * FROM TBName WHERE age != 18;
SELECT * FROM TBName WHERE age <> 18;
```
### 007 或者 or --- in
```mysql
#查询年龄等于18岁 或者 20岁 或者 22岁的学员信息
SELECT * FROM TBName WHERE age = 18 OR age = 20 OR age = 22;
SELECT * FROM TBName WHERE age IN (18, 20 ,22);
```
### 008 值为空 is null --- is not null

```mysql
#查询英语成绩为null的学员信息需要使用 is 和 is not
SELECT * FROM TBName WHERE english IS null;
SELECT * FROM TBName WHERE english IS NOT null;
```
### 009 

```mysql
#查询姓'马'的学员信息
SELECT * FROM TBName WHERE name LIKE '马%';
```
### 010

```mysql
#查询姓名两个字的学员信息
SELECT * FROM TBName WHERE name LIKE '__%';
```
### 011

```mysql
#查询第二个字是花’的学员信息
SELECT * FROM TBName WHERE name LIKE '_花%';
```
### 012

```mysql	
#查询名字中包含‘德’的学员信息
SELECT * FROM TBName WHERE name LIKE '%德%';
```
### 013

```mysql	
#查询名字中最后一个字是‘德’的学员信息
SELECT * FROM TBName WHERE name LIKE '%德';
```

# 003 聚合查询

## 01 语法

```mysql
SELECT 聚合函数名(列名) FROM TBName;
```

## 02 函数名

### 001 统计总数
```mysql
SELECT count(id) FROM TBName;
SELECT count(*) FROM TBName;
```
### 002 查询最大值
```mysql
SELECT MAX(math) FROM TBName;
```
### 003 查询最小值
```mysql
SELECT MIN(math) FROM TBName;
```
### 004 查询总和
```mysql
SELECT SUM(math) FROM TBName;
```
### 005 查询平均值
```mysql
SELECT AVG(math) FROM TBName;
```

# 004 分组查询

## 01 语法

```mysql
SELECT * FROM TBName WHERE 分组前条件 GROUP BY 分组字段名 HAVING 分组后条件;
```

## 02 WHERE 和 HAVING 的区别

### 001 执行时机不同

where 是分组前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤。

### 002 判断条件不同

where不能对聚合函数进行判断，而having可以。

## 03 注意

### 001 执行顺序

where 》聚合函数 》having

### 02 

分组之后，==查询的字段==一般为聚合函数和分组字段，查询其它字段无意义。

## 04 分组

### 001
```mysql
#查询男同学和女同学各自的数学平均分
SELECT sex, AVG(math) FROM 表名 GROUP BY sex;
```
### 002
```mysql
#查询男同学和女同学各自的数学平均分，以及各自人数
SELECT sex, AVG(math), COUNT(*) FROM stu GROUP BY sex;
```
### 003
```mysql
#查询男同学和女同学各自的数学平均分，以及各自人数，要求：分数低于70分的不参与分组
SELECT sex, AVG(math), COUNT(*) FROM stu WHERE math > 70 GROUP BY sex;
```
### 004
```mysql
#查询男同学和女同学各自的数学平均分，以及各自人数，要求：分数低于70分的不参与分组，分组之后人数大于2个的
SELECT sex, avg(math), count(*) FROM stu WHERE math > 70 GROUP BY sex HAVING COUNT(*) > 2;
```

# 005 排序查询

## 01 语法

```mysql
SELECT field FROM TBName
ORDER BY 字段名1 排序方式1, 字段名2 排序方式2, ...;
```

## 02 排序方式

### 001 升序排列
```mysql
#查询学生信息，按照年龄升序排列
SELECT * FROM TBName ORDER BY age;
```
### 002 降序排列
```mysql
#查询学生信息，按照数学成绩降序排列
SELECT * FROM TBName ORDER BY math DESC;
```
### 003 先降序，再升序排列
```mysql
#查询学生信息，按照数学成绩降序排列，若数学成绩一样，再按照英语成绩升序排列
SELECT * FROM TBName ORDER BY math DESC, english ASC;
```

# 006 分页查询

## 01 语法

```mysql
#起始索引 = (查询页码 - 1) * 查询条目数
SELECT field FROM TBName LIMIT 起始索引, 查询条目数;
```

## 02 分页参数

```mysql
从0开始查询，查询3条数据
SELECT * FROM TBName LIMIT 0,3;
SELECT * FROM TBName LIMIT 3;

每页显示3条数据，查询第1页数据
SELECT * FROM TBName LIMIT 0, 3;

每页显示3条数据，查询第2页数据
SELECT * FROM TBName LIMIT 3, 3;

每页显示3条数据，查询第5页数据
SELECT * FROM TBName LIMIT 6, 3;
```

## 03 执行顺序

```mysql
#从上往下依次执行
FROM
	TBName
WHERE
	condition
GROUP BY
	分组字段
HAVING
	分组后条件
SELECT
	字段列表
ORDER BY
	排序字段
LIMIT
	分页参数
```
