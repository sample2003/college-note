# 一、概述

## 1. 全称

Hyper Text Markup Language : 超文本标记语言

## 2. 发展历程

# 二、基本结构

## 1. 注释

```html
<!-- 注释不可嵌套 -->
```

## 2. 文档声明

```html
<!DOCTYPE html>
```

## 3. 字符编码

文件 编码 (编码出现问题，则数据无法保存)   -->   浏览器 解码

```html
<head>
	<meta charset="UTF-8">
</head>
```

## 4. 设置语言

```html
<html lang="zh-CN">
</html>
```

## 5. 标准结构

   ```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
</body>
</html>
```

## 6. 浏览器图标

   在存放代码的文件夹下，放favicon.ico图标

## 7. 开发文档

[W3C](https://whatwg-cn.github.io/html/)

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML)

[w3school](https://www.w3school.com.cn/html/html5_intro.asp)

## 8. 全局属性

[HTML 全局属性 (w3school.com.cn)](https://www.w3school.com.cn/tags/html_ref_standardattributes.asp)

![[Pasted image 20230616155444.png]]

## 9. 字符实体

# 三、标签

## 1. 排版标签

```html
<h1>一级标题</h1>

<h6>六级标题</h6>

<p>段落标签，p中不要嵌套div、p、h</p>

水平线标签<hr/>

换行标签<br>

<center>内容居中标签<center>

<pre>预定义（预格式化）标签</pre>
```

## 2. 语义化标签

[语义解释](https://blog.csdn.net/m0_51273200/article/details/120330863)

概念：用特定的标签表达特定的效果。

语义化：标签默认的效果不重要，语义最重要。

1. 代码的可读性强清晰
2. 有利于SEO（搜索引擎优化）爬虫 代码机器人
3. 方便设备解析（屏幕阅读器、盲人阅读器)

## 3. 文本标签

```html
<span></span>
<pre></pre>
<i></i>
<del></del>
<ins></ins>
```

## 4. 图片标签 img

## 5. 超链接 a

```html
<a href="other.html">跳转页面，并打开新标签</a>
<a href="movie.mp4" download="movie">不跳转，并下载文件</a>
<a href="https://www.xxxxx.com#tips">跳转链接的某个锚点</a>

<a name="tips"></a>
<a href="#">回到顶层</a>
<a href="">刷新页面</a>
<a href="javascript:;">执行javaScript脚本</a>

<a href="tel:10086">电话联系</a>
<a href="mailto:1234@qq.com">邮箱联系</a>
<a href="sms:10086">短信联系</a>
```

## 6. 框架标签

### 01 嵌入网页

```html
<iframe 
		src="https://www.taobao.com" 
		width="200" height="200" 
		frameborder="0"
>
</iframe>
```

### 02 嵌入内容

```html
<iframe 
		src="https://www.taobao.com" 
		width="200" height="200" 
		frameborder="0"
>
</iframe>
```

### 03 超链接-[[HTML#012 超链接 a|a]]-target-跳转

```html
<a href="https://www.taobao.com" target="tt">淘宝</a>
<iframe 
		name="tt"
		width="500" height="500" 
		frameborder="0"
>
</iframe>
```

### 04 表单-[[HTML#015 表单 form|from]]-target-跳转

```html
<form 
	  action="https://so.www.toutiao.com/search"
	  target="container"
>
	<input type="text" name="keyword">
	<input type="submit" value="搜索">
</form>
<iframe 
		name="container"
		width="500" height="500" 
		frameborder="0"
>
</iframe>
```

# 四、块级元素、行内元素和行内块元素

[原文链接](https://blog.csdn.net/weixin_46536890/article/details/114876226)

## 1. 块级元素-block

### 01 特点：

- 自动换行
- 独占一行
- 可设置宽高
- 默认宽度为父元素的宽度

### 02 常见块级元素

- div、p、h1~h6、ul、ol、dl、li、dd、table、hr、blockquote、address、table、menu、pre
- HTML5新增的header、section、aside、footer等

### 03 注意规范
- 块级元素可以嵌套任意元素
- 块级文字元素中不能放入其他块级元素，比如： ==p中不要嵌套div、p、h==，h1~h6不能互相嵌套

## 2. 行内元素-inline

### 01 特点

- 无法自动换行
- 一行可放多个
- ==不可设置宽高==
- 默认宽度是本身内容宽度
- 行内元素的paddding可以设置
- margin只能设置水平方向的边距，即：margin-left和margin-right，设置margin-top和margin-bottom无效
- ==无法通过css设置宽高==

### 02 常见行内元素
- span、img、a、lable、input、abbr（缩写）、em（强调）、big
- cite（引用）、i（斜体）、q（短引用）、textarea、select、small
- sub、sup，strong、u（下划线）、button（默认display：inline-block）

### 03 注意规范

行内元素尽量只放行内元素与行内块元素，==链接里边不能再放链接，特殊情况a可以嵌套任意元素==

## 3. 行内块元素 inline-block

### 01 特点：

综合块级元素与行内元素的特性，可设宽高（默认是内容宽高），也可以设置内外边距

### 02 常见行内块元素
img 、input 、td

## 4. 标签之间的转换

- display：inline（转为行内元素）
- display：inline-block（转为行内块元素）
- display：block（转为块元素）
- display：none（隐藏 不显示）

==注意：当元素浮动（float）时会转化成行内块元素特点。==

# 五、列表 list

## 01 有序列表

```html
<ol>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
<ol>
```

## 02 无序列表

```html
<ul>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
<ul>
```

## 03 自定义列表

```html
<dl>
	<dt>名称</dt>
	<dd>内容</dd>
	<dt>名称</dt>
	<dd>内容</dd>
<dl>
```

# 六、表格 table

## 001 表格结构

```html
<table border="1" width="500" height="500" cellspacing="0">
	<caption>表格标题</caption>
	<!-- 表格头部 -->
	<thead height="50" align="center" valign="middle">
		<tr>
			<th></th>
			<th></th>
		</tr>
	</thead>
	<!-- 表格主体 -->
	<tbody height="400" align="left" valign="top">
		<tr>
			<td></td>
			<td></td>
		</tr>
	</tbody>
	<!-- 表格脚注 -->
	<tfoot height="50" align="right" valign="bottom">
		<tr>
			<td></td>
			<td></td>
		</tr>
	</tfoot>
</table>
```

## 002 跨行与跨列

```html
<th colspan="2">指定跨的列数</th>

<td rowspan="2">指定跨的行数</td>
```

# 七、表单 form

## 01 表单结构

```html
<form>
	<label for="card1"></label>
	<input id="card1">
	
	<label><input><lable>
</form>
```
<form 
	  action="https://www.baidu.com/s" 
	  target="_blank" 
	  method="get"
>
	<input type="text" name="wd">
	<button>百度</button>
</form>

## 02 表单控件

### 001 文本框

```html
<input type="text" name="account" value="default" maxlength="6">
```
<input type="text" name="account" value="default" maxlength="6">

### 002 密码框

```html
<input type="password" name="pwd" value="123456" maxlength="6">
```
<input type="password" name="pwd" value="123456" maxlength="6">

### 003 单选框

```html
<lable>
<input type="radio" name="gender" value="male" checked>one</lable>
<lable>
<input type="radio" name="gender" value="female">two</lable>
```
<lable>
<input type="radio" name="gender" value="male" checked>one</lable><lable>
<input type="radio" name="gender" value="female">two</lable>

### 004 复选框

```html
<input type="checkbox" name="hobby" value="1"><input type="checkbox" name="hobby" value="2"><input type="checkbox" name="hobby" value="3">
```
<input type="checkbox" name="hobby" value="1"><input type="checkbox" name="hobby" value="2"><input type="checkbox" name="hobby" value="3">

### 005 隐藏域

```html
<input type="hidden" name="tag" value="111">
```

### 006 按钮

#### 01 提交
```html
<input type="submit" value="ipt-submit">
<button></button>
```
<input type="submit" value="ipt-submit">

#### 02 重置
```html
<input type="reset" value="ipt-reset">
<button type="reset"></button>
```
<input type="reset" value="ipt-reset">

#### 03 普通
```html
<input type="button" value="ipt-button">
<button type="button"></button>
```
<input type="button" value="ipt-button">

### 007 文本域

```html
<textarea name="other" cols="10" rows="10"></textarea>
```
<textarea name="other" cols="10" rows="2"></textarea>

### 008 下拉框

```html
<select name="num">
        <option value="1" selected>one</option>
        <option value="2">two</option>
</select>
```
<select name="place">

        <option value="1" selected>11</option>

        <option value="2">22</option>

    </select>

### 009 禁用表单控件

```html
<input type="text" name="account" value="default" disabled>
```
<input type="text" name="account" value="default" disabled>

### 010 fieldset与legend

```html
<fieldset>
        <legend>main</legend>
        <label for="card">card:</label>
        <input type="text" name="card">
</fieldset>
```
<fieldset>
        <legend>main</legend>
        <label for="card"></label>
        <input type="text" name="card">
</fieldset>

# 八、meta 基本信息

## 01 配置字符编码

```html
<!--配置字符编码-->
<meta charset="UTF-8">
```

## 02 兼容性设置

```html
<!--针对IE浏览器的兼容性设置-->
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```

## 03 移动端的配置

```html
<!--针对移动端的配置-->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## 04 配置网页关键字

```html
<!--配置网页关键字-->
<meta name="keywords" content="8-12个以英文逗号隔开的单词/词语">
```

## 05 配置网页描述信息

```html
<!--配置网页描述信息-->
<meta name="description" content="80字以内的一段话，与网站内容相关">
```

## 06 针对搜索引擎爬虫配置

```html
<!--针对搜索引擎爬虫配置-->
<meta name="robots" content="可选值">
```
可选值
- index 
	允许搜索爬虫索引此页面。
- noindex 
	要求搜索爬虫不索引此页面。
- follow 
	允许搜索爬虫跟随此页面上的链接。
- nofollow
   要求搜索爬虫不跟随此页面上的链接。
- all与index，follow等价
- none与noindex，nofollow等价
- noarchive 
  要求搜索引擎不缓存页面内容。
- nocache noarchive 的替代名称。

## 07 配置网页作者

```html
<meta name="author" content="tony">
```

## 08 配置网页生成工具

```html
<meta name="generator" content="Visual Studio Code">
```

## 09 配置定义网页版权信息

```html
<meta name="copyright"content="2023-20270版权所有“>
```

## 10 配置网页自动刷新

```html

```

## 11 配置浏览器内核

```html
<meta naem="renderer" content="webkit">
```

# 九、HTML5

## 1. 新增布局（语义化）标签

### 01 header

整个页面，或部分区域的头部

### 02 footer

整个页面，或部分区域的底部

### 03 nav 

导航

### 04 article

文章、帖子、杂志、新闻、博客、评论等

### 05 section

页面中的某段文字，或文章中的某段文字 (里面文字通常里面会包含标题)

### 06 aside

侧边栏

### 07 main

文档的主要内容(WHATWG 没有语义，IE 不支持)，几乎不用。

### 08 hgroup

包裹连续的标题，如文章主标题、副标题的组合 ( w3c 将其删除)

### 09 关于 article和 section

1. artical 里面可以有多个 section 。
2. section 强调的是分段或分块，如果你想将一块内容分成几段的时候，可使用 section 元素。
3. article 比 section 更强调独立性，一块内容如果比较独立、比较完整，应该使用 article 元素。

## 2. 新增状态标签

### 01 meter

语义: 定义已知范围内的标量测量。也被称为 gauge (尺度)，双标签，例如: 电量、磁盘用量等；

常用属性如下:
- high 规定高值
- low 规定低值
- max 规定最大值
- min 规定最小值
- optimum 规定最优值
- value 规定当前值

### 02 progress

语义: 显示某个任务完成的进度的指示器，一般用于表示进度条，双标签，例如:工作完成进度等；

常用属性如下:
- max 规定目标值。
- value 规定当前值。

## 3. 新增列表标签

### 01 datalist

```html
<input type="text" list="mydata">

<datalist id="mydata">
	<option value="周冬雨">周冬雨</option>
	<option value="周杰伦">周杰伦</option>
	<option value="温兆伦">温兆伦</option>
	<option value="马冬梅">马冬梅</option>
</datalist>
```

### 02 details

用于搜索框的关键字提示

summary

用于展示问题和答案，或对专有名词进行解释
写在 details 的里面，用于指定问题或专有名词

```html
<details>
	<summary>如何走上人生巅峰?</summary>
	<p>一步一步走呗</p>
</details>
```

## 4. 新增表单控件属性

### 01 placeholder 

提示文字(注意:不是默认值， value 是默认值) ，适用于文字输入类的表单控件。

```html
账号：<input type="text" name="account" placeholder="请输入账号">
```

### 02 required

表示该输入项必填，适用于除按钮外其他表单控件。

```html
账号：<input type="text" name="account" required>
```

### 03 autofocus

自动获取焦点，适用于所有表单控件。

```html
账号：<input type="text" name="account" autofocus>
```

### 04 autocomplete

自动完成，可以设置为 on 或 off ，适用于文字输入类的表单控件；
注意:密码输入框、多行输入框不可用。

```html
<input type="text" name="account" autocomplete="on">
```

### 05 pattern

填写正则表达式，适用于文本输入类表单控件。
注意: 多行输入不可用，且空的输入框不会验证，往往与 required 配合。

```html
账号：<input type="text" name="account" required pattern="/w{6}">

```

## 5. input 新增type属性

### 01 email

```html
账号：<input type="email" name="email" required>
```

### 02 url

```html
账号：<input type="url" name="url" required>
```

### 03 number

```html
账号：<input type="number" name="number" required step="2" max="80" min="20" value="22">
```

### 04 search

```html
账号：<input type="search" name="search" required>
```

### 05 tel

```html
账号：<input type="tel" name="tel" required>
```

### 06 range

```html
账号：<input type="range" name="range" required>
```

### 07 color

```html
账号：<input type="color" name="color">
```

### 08 date

```html
账号：<input type="date" name="date" required>
```

### 09 month

```html
账号：<input type="month" name="month" required>
```

### 10 week

```html
账号：<input type="week" name="week" required>
```

### 11 time

```html
账号：<input type="time" name="time" required>
```

## 06 新增视频标签

## 07 新增音频标签

## 08 HTML5 兼容性调整

### 001 引用JS

```html
<!--[if lt ie 9]>
<script src="./html5shiv.js"></script>
<![endif]-->
```

### 002 meta配置

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="render" content="webkit">
```
