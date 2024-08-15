# 一、数据库

## 数据库操作

显示所有的数据库：show dbs、show databases
显示当前所在的数据库：db
创建或选择数据库：use 数据库名称
删除当前数据库：db.dropDatabase()

## 基础数据库介绍

admin ：从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限
local：这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
config：当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息

# 二、集合

## 1、新增集合

显示新增：db.createCollection(集合名，[参数])

隐式新增：通过插入文档数据来默认创建
db.集合名.insert({id:1,name:forlan});

```
test> db.createCollection("forlan1")
{ ok: 1 }

test> db.forlan2.insert({id:1,name:"forlan"});
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
{
  acknowledged: true,
  insertedIds: { '0': ObjectId("64a67bcf918d27194254b6a9") }
}
```

命名规范

>不能是空字符串
>不能含有 \0字符（空字符)，这个字符表示集合名的结尾
>不能以 "system."开头，这是为系统集合保留的前缀
>不能含有保留字符。另外千万不要在名字里出现$

## 2、查看集合

显示数据库中所有的集合：show tables、show collections

```shell
test > show tables;
forlan1
forlan2
```

## 3、删除集合

删除当前集合：db.collection.drop()

```
test> db.forlan1.drop()
```

清空一个集合(效率低，直接删集合更快)：db.collection.remove({})

```
test> db.forlan1.remove({}) 
test> db.forlan1.remove({"name":"zhang"})
```

# 三、文档

mongo \_id的生成规则： 时间戳+机器码+PID+计数器

## 1、新增文档

语法：

db.collection.insert()：单文档插入
db.collection.insertMany()：多文档插入
db.collection.insert()：单、多文档插入

例子：

```
db.collection.insert({k1:v1,k2:v2})

test> db.forlanC.insertOne({uid:1,name:"forlan1",city:"广州",age:25})
{
  acknowledged: true,
  insertedId: ObjectId("64a4ef4475b1d2bd73f082e1")
}

```

```
db.collection.insertMany([{k1:v1,k2:v2},{k1:v1,k2:v2}])

test> db.forlanC.insertMany([{uid:2,name:"forlan2",city:"深圳",age:27},{uid:3,name:"forlan3",city:"佛山",age:30}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("64a4ef4c75b1d2bd73f082e2"),
    '1': ObjectId("64a4ef4c75b1d2bd73f082e3")
  }
}
```

```
db.collection.insert([{k1:v1,k2:v2}…])

test> db.forlanC.insert({uid:1,name:"forlan1",city:"广州",age:25})
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
{
  acknowledged: true,
  insertedIds: { '0': ObjectId("64a4efce75b1d2bd73f082e4") }
}

test> db.forlanC.insert([{uid:2,name:"forlan2",city:"深圳",age:27},{uid:3,name:"forlan3",city:"佛山",age:30}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("64a4efe075b1d2bd73f082e5"),
    '1': ObjectId("64a4efe075b1d2bd73f082e6")
  }
}
```

## 2、更新文档

语法：

db.collection.updateOne(filter, update, options)：修改集合中的一个现有文档
db.collection.updateMany(filter, update, options)：修改集合中的多个现有文档
db.collection.replaceOne(filter, replacement, options)：替换集合中的一个现有文档
db.collection.update(query, update, options)：修改或替换集合中的一个或多个现有文档，已弃用

例子：

db.collection.updateOne(条件,更新字段)，更新匹配的第一个文档

```
test> db.forlanC.updateOne({name:"forlan1"},{'$set':{age:26,id:1}});
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

db.collection.updateMany(条件,更新字段)，更新所有匹配的文档

```
test> db.forlanC.updateMany({age:27},{'$set':{id:27}});
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 1,
  upsertedCount: 0
}
```

db.collection.replaceOne(条件,替换内容)，替换匹配的第一个

```
test> db.forlanC.replaceOne({name:"forlan1"},{id:1})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

db.collection.update(条件,更新字段)，更新匹配文档，不加{multi:true}，就相当于updateOne

```
test> db.forlanC.update({age:27},{'$set':{id:28}},{multi:true});
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 1,
  upsertedCount: 0
}
```

## 3、删除文档

语法：

db.collection.deleteOne(filter, options)：删除集合中的一个现有文档
db.collection.deleteMany(filter, options)：删除集合中的多个现有文档
db.collection.remove(query, options)：删除集合中的一个或多个现有文档

例子：

deleteOne删除uid=2的文档

```
test> db.forlanC.deleteOne({uid:2})
```

deleteMany删除uid<=3的文档

```
test> db.forlanC.deleteMany({uid:{$lte:3}})
```

deleteMany删除所有文档

```
test> db.forlanC.deleteMany({})
```

remove删除uid=1的文档，已弃用，会提示

```
test> db.forlanC.remove({uid:1})
DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.
{ acknowledged: true, deletedCount: 1 }
```

## 4、查询文档

### 4.1 统计

语法：

db.collection.count(query, options)：统计

例子：

统计uid=1的文档数

```
test> db.forlanC.count({uid:1})
```

### 4.2 分页、排序

db.collection.find().skip(NUMBER).limit(NUMBER)：分页查询，使用skip()方法来跳过指定数量的数据，limit()方法来读取指定数量的数据，

```
db.forlanC.find().skip(0).limit(5) // 第一页，每页显示5个
db.forlanC.find().skip(5).limit(5) // 第二页，每页显示5个
db.forlanC.find().skip(10).limit(5) // 第三页，每页显示5个
```

db.collection.find().sort({field:NUMBER}) ：排序，1升序、-1降序
skip(), limit(), sort()三个放在一起执行的时候，执行的顺序是先 sort(), 然后是 skip()，最后是显示的 limit()，和命令编写顺序无关

### 4.3 查询

db.collection.find(query, [projection], options)：查询
db.collection.find({},{field1:1,field2:1…})：查询显示特定字段
db.collection.find({字段:/正则表达式/}) ：正则表达式是 js的语法
db.collection.find({field:{$in: [value1,value2]}})：包含
db.collection.find($and:[ {field1:value1}…])：条件
db.collection.find({field1: { operator1: value1 }, … })：比较

### 4.4 比较

大于: 
db.collection.find({"field": { $gt: value }})：field >value
小于: 
db.collection.find({"field": { $lt: value }})：field < value
大于等于: 
db.collection.find({"field": { $gte: value }})：field >= value
小于等于:
db.collection.find({"field": { $lte: value }})： field <= value
不等于: 
db.collection.find({"field": { $ne: value }})：field != value

值在/不在里面
db.collection.find({"field": { $in: [v1,v2,...]}})
db.collection.find({"field": { $nin: [v1,v2,...]}})

db.collection.find({"field": { $size: 3}})

db.collection.find({"field": { $exist: true|false}})

db.collection.find({$or:[{"name":"张三"},{"name":"李四"}])

### 4.5 实例

查找uid=1的文档

```
test> db.forlanC.find({uid:1})
```

查找以name是以forlan开头的文档

```
test> db.forlanC.find({name:/^forlan*/})
```

查找uid=1，同时name=forlan1的文档

```
test> db.forlanC.find({$and:[{uid:1},{name:"forlan1"}]})
```

查找指定字段uid和name

```
test> db.forlanC.find({},{uid:1,name:1});
```

## 5、聚合

聚合(aggregate)是基于数据处理的聚合管道，每个文档通过一个由多个阶段（stage）组成的管道，可以对每个阶段的管道进行分组、过滤等功能。

db.集合名.aggregate({管道:{表达式}})
### 5.1 常用管道

#### $group
将集合中的文档分组，可用于统计结果

\_id表示分组的依据，使用某个字段的格式为’$字段’

返回sex有哪些值
db.test.aggregate(
	{$group:{
		\_id:"$sex"
		}
	}
)

//统计男生、女生分别的总人数
db.test.aggregate(
	{$group:
		{
		\_id:"$sex",
		count:{$sum:1}
		}
	}
)

//统计男、女分别的平均年龄
db.test003.aggregate(
	{$group:
		{
		\_id:"$sex",
		count:{$sum:1},
		avg_age:{\$avg:"$age"}
		}
	}
)

注意：
\_id:null：将集合中所有文档分为一组

//示例--求总人数、平均年龄
db.test.aggregate(
	{$group:
		{
		\_id:null,
		count:{$sum:1},
		avg_age:{\$avg:"$age"}
		}
	}
)

总结：
$group对应的字典中有几个键，结果中就有几个键

分组依据需要放到_ id后面

取不同的字段的值需要使用$，如：$hometown、$age、$sex

取字典嵌套的字典中值的时候$_id.字段名

同时取多个键进行分组：{$group:{_id:{字段名1:"$字段名1",字段名2:"字段名2"}}}；输出结果：{_id:{字段名1:"",字段名2:""}

#### $project

修改输入文档的结构，如重命名、增加、删除字段、创建计算结果；简单来说就是修改输入输出的值

//查询姓名、年龄
db.test.aggregate({$project:{\_id:0, name:1, age:1}})

//查询男、女人数，输出人数

>db.test.aggregate(
	{\$group:
		{
			\_id:'\$sex', 
			count:{$sum:1}
		}
	},
	{$project:
		{
			\_id:0, 
			count:1
		}
	}
)

#### $match

用于过滤数据，只输出符合条件的文档

使用MongoDB的标准查询操作

match是管道命令，能将结果交给后一个管道，但是find不可以

//查询年龄大于20的
db.test.aggregate(
	{\$match:{age:{$gt:20}}}
)

//查询年龄大于等于18的男生、女生人数
\db.test.aggregate(
	{\$match:{age:{$gte:18}}},
	{\$group:{\_id:'\$sex',count:{$sum:1}}}
)

#### $sort

将输入文档排序后输出

//查询信息，按年龄升序
db.test.aggregate({$sort:{age:1}})

//查询男生、女生人数，按人数降序
db.test.aggregate(
	{\$group:{\_id:'\$sex',count:{$sum:1}}},
	{$sort:{count:-1}}
)


#### $limit
限制聚合管道返回的文档数量

//查询2条信息
db.test.aggregate({$limit:2})

#### $skip
跳过指定数量的文档，并返回余下的文档

//查询从第3条开始的信息
db.test.aggregate({$skip:2})

//跳过前2个文档，然后返回接下来的1个文档
db.test.aggregate(
	{$skip:2},
	{$limit:1}
)

注意：两者都用时，先写skip, 再写limit。

#### $unwind

将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值

语法格式：db.集合名称.aggregate({\$unwind:'$字段名称’})

 db.test.insert({\_id:1, item:'t-shirt', size:['S','M','L']})

db.test.aggregate({\$unwind: '$size'})
{ "\_id" : 1, "item" : "t-shirt", "size" : "S" }
{ "\_id" : 1, "item" : "t-shirt", "size" : "M" }
{ "\_id" : 1, "item" : "t-shirt", "size" : "L" }


属性preserveNullAndEmptyArrays值为true表示保留属性值为空的⽂档；值为false表示丢弃属性值为空的⽂档
db.test.aggregate({
	$unwind:{
		path:'$字段名称',
		preserveNullAndEmptyArrays:\<boolean>
	}
})

### 5.2 表达式

\$sum：计算总和，$sum:1同count表示计数
$avg：计算平均值
$min：获取最小值
$max：获取最大值
$push：在结果文档中插入值到一个数组中，相当于拼接字段
$first：根据资源文档的排序获取第一个文档数据
$last：根据资源文档的排序获取最后一个文档数据

```
db.集合名.aggregate( 
	{$group: 
		{
			_id:'$字段名', 别名:{$聚合函数:'$字段名'} 
		} 
	}
);
```


统计同年龄的人数 
```
db.yunfan_test.aggregate( 
	{$group:
		{
			_id:'$age',
			count_age:{$sum:1} 
		} 
	} 
); 

```

统计所有人平均年龄 
```
db.yunfan_test.aggregate( 
	{$group: 
		{ 
			_id:null, 
			总人数:{$sum:1}, 
			avg_age:{$avg:"$age"}, 
			min_age:{$min:"$age"}, 
			max_age:{$max:"$age"} 
		} 
	} 
);
```


# 四、索引

## 1、介绍

索引主要是帮助MongoDB高效获取数据的数据结构

如果没有索引，MongoDB必须执行全集合扫描，即扫描集合中的每个文档，以选择与查询语句匹配的文档。这种扫描全集合的查询效率是非常低的，特别在处理大量的数据时，查询可能要花费几十秒甚至几分钟，这对网站的性能是非常致命的

MongoDB索引使用B树数据结构（确切的说是B-Tree，MySQL是B+Tree），多叉树

## 2、类型

单字段索引：对文档单个字段创建索引
复合索引：对文档多个字段创建索引

## 3、管理操作

### 3.1 创建索引

语法：db.collection.createIndex(keys, options, commitQuorum)

例子：
创建单索引，按uid字段升序
```
test> db.forlanC.createIndex({uid:1})
uid_1
```
创建复合索引，按uid字段降序，name散列
```
test> db.forlanC.createIndex({uid:-1,name:"hashed"})
uid_-1_name_hashed
```

### 3.2 查看索引

语法：db.collection.getIndexes()

```
test> db.forlanC.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { uid: 1 }, name: 'uid_1' },
  {
    v: 2,
    key: { uid: -1, name: 'hashed' },
    name: 'uid_-1_name_hashed'
  }
]
```

### 3.3 删除索引

删除指定索引

使用索引名称删除：db.collection.dropIndex(indexName)
使用索引文档删除：db.collection.dropIndex({field:value})

```
test> db.forlanC.dropIndex("uid_-1_name_hashed")
{ nIndexesWas: 3, ok: 1 }

test> db.forlanC.dropIndex({uid: 1 })
{ nIndexesWas: 2, ok: 1 }
```

删除所有索引，处理主键索引_id：db.collection.dropIndexes()

```
test> db.forlanC.dropIndexes()
{
  nIndexesWas: 3,
  msg: 'non-_id indexes dropped for collection',
  ok: 1
}
```