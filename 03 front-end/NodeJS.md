# Node.js概述

## Node.js的诞生

## Node.js的作用

Node.js是一个开源的，跨平台的JavaScript运行环境，用于开发服务器应用，开发工具类应用，开发桌面端应用。

## Node.js的安装

打开[Node.js的官网](https://nodejs.org/en/download)，下载一个长期支持版本，在安装完成之后，在终端输入node -V，若成功显示版本号，则表示nodejs已经安装成功了

## 运行一个js

```shell
node hello.js
```

## 注意事项

nodejs不能使用BOM和DOM的API
nodejs中的顶级对象为global，也可以用globalThis访问顶级对象

# Buffer

## Buffer是什么

中文译为缓冲区，Buffer类的实例类似于整数数组，但Buffer 的大小是固定的、且在V8堆外分配物理内存。Buffer的大小在被创建时确定，且无法调整。

`Buffer` 类在 Node.js 中是一个全局变量

## Buffer方法

==Buffer.alloc()==
```js
let buf = Buffer.alloc(10);
console.log(buf)

// <Buffer 00 00 00 00 00 00 00 00 00 00>
```

==Buffer.allocUnsafe()==
```js
let buf = Buffer.allocUnsafe(10);
console.log(buf)

// <Buffer 00 00 00 00 00 00 00 00 00 00>
```

==Buffer.from()==
```js
let buf = Buffer.from("hello");
console.log(buf)

// <Buffer 68 65 6c 6c 6f>
```

## Buffer与字符串的转换

```js
let buf = Buffer.from([105,108,111,118,101,121,111,117]);
console.log(buf.toString());

// iloveyou
```

## 

# 模块

## fs模块

fs作用：读取文件内容

path：表示文件路径
option：选项配置
callback：回调函数
err：错误信息
data：读取的数据

### 文件读取

读取文件（异步）
==fs,readFile(path[, option], callback(err, data))==
```js
// 引入fs模块
const fs = require("fs")

fs.writeFile("1.txt", "utf8", function(err, data){
	if (err) {
        console.error(err);
        return;
    }
    console.log(data);
});
```

流式读取
==fs.createReadStream(path[,option])==
```js
// 创建读取流对象
const rs = fs.createReadStream('hello.txt','utf8')
// 绑定data事件
rs.on('data', chunk=>{
	console.log(chunk);
})
```

### （创建）文件写入

写入文件（异步）
==fs.writeFile(path, data[,option], callback)==
```js
// 引入fs模块
const fs = require("fs")

fs.writeFile("1.txt", "content", function(err, dataStr){
	if(err) {
		return console.log(err.message);
	}
	console.log(dataStr);
});
```

同步写入
==fs.writeFileSync==
```js
fs.writeFileSync('1.txt','test');
```

追加写入
==fs.appendFile(path, data[,option], callback)==
```js
// 换行
fs.appendFile('1.txt','\r\ntest2',function(){
	if(err) throw err
	console.log('success');
});
```

流式写入
==fs.createWriteStream(path[,option])==
```js
const ws = fs.createWriteStream('hello.txt');
ws.write('hello');
ws.write('world');
ws.close();
```

### 文件复制

readFile
```js
const data = fs.readFileSync('hello.txt');
fs.writeFileSync('copy.txt',data);
```

流式
```js
const rs = fs.createReadStream('hello.txt');
const ws = fs.createWriteStream('copy.txt');
rs.on('data',chunk=>{
    ws.write(chunk);
});
```

### 文件重命名和移动

==fs.rename(path1,path2,callback)==
path1：原文件路径
path2：要修改的文件名
```js
fs.rename('hello.txt', 'test.txt', err => {
	if(err) throw err;
	console.log('success');
});
```

### 文件删除

==fs.unlink(path, callback)==
```js
fs.unlink('hello.txt', err=>{
	if(err) throw err;
	console.log('success');
});
```

==fs.rm(path, callback)==
```js
fs.rm('hello.txt', err=>{
	if(err) throw err;
	console.log('success');
});
```

### 文件夹操作

创建文件夹
==fs.mkdir(path[,options], callback);==
```js
fs.mkdir('./hello', err=>{
	if(err) throw err;
	console.log('success');
});
```

递归创建
==fs.mkdir(path, {recursive:true}, callback);==
```js
fs.mkdir('./a/b/c', {recursive:true}, err=>{
	if(err) throw err;
	console.log('success');
});
```

读取文件夹
==fs.readdir(path, callback)==
得到一个包含目录内文件名的数组
```js
fs.readdir('./hello', (err, data)=>{
	if(err) throw err;
	console.log(data);
});
```

删除文件夹
==fs.rmdir(path, callback)==
```js
fs.rmdir('./hello', err=>{
    if(err) throw err;
    console.log('success');
});
```

递归删除
==fs.rm(path, {recursive:true}, callback)==
```js
fs.rm('./a/b/c', {recursive:true}, err=>{
	if(err) throw err;
	console.log('success');
});
```

### 查看资源状态

==fs.stat(path[,option], callback)==
```js
fs.stat('hello.txt', (err, data)=>{
	if(err) throw err;
	console.log(data);
});
```


==fs.statSync(path[,option])==

### 批量重命名

```js
const files = fs.readdirSync('.\code');
files.forEach(item => {
	let data = item.split('-');
	let [num, name] = data;
	if(Number(num) < 10){
		num = '0' + num;
	}
	let newName = num + '-' + name;
	fs.renameSync(`./code/${item}`,`./code/${newName}`);
});
```

## path模块

### 拼接路径

==path.resolve()==
```js
const path = require('path');

console.log(path.resolve(__dirname, './index.html'));
```

### 获取分隔符

==path.sep==

### 解析路径

==path.parse(str)==

### 获取路径名称

==path.basename(str)==

### 获取路径目录名

==path.dirname(str)==

### 获取路径扩展名

==path.extname(str)==

## http模块