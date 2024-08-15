
# 一、概述

## 1. 全称

Cascading Style Sheet : 层叠样式表

## 2. 发展

# 二、样式位置

## 1. 行内样式

又称内联样式

```html
<h1 style="color:red">一级标题<h1>
```

## 2. 内部样式

```html
<head>
    <title>Document</title>
    <style>
        h1 {
            color: aqua;
        }
    </style>
</head>
```

## 3. 外部样式

```html
<head>
    <title>Document</title>
	<!-- rel： relation 关系， 说明引入的文档与当前文件的关系-->
    <link rel="stylesheet" href="../style.css">
</head>
```

## 4. 样式表的优先级

- 优先级规则：行内样式 > 内部样式 = 外部样式
- 内部样式， 外部样式这两者优先级一致，以后写的为准
- 同一张样式表中，以后写的为准

```html
<style>
	h1 {
		color: aqua;
		font-size: 10px;
	}
	
	/*只会覆盖颜色*/
	
	h1 {
		color: red;/*以红色为准*/
	}
</style>
```

# 三、CSS 选择器

## 1. 基本选择器

### 01 通配选择器

可以选中所有的html元素

```html
<style>
	* {
		color: red;
	 }
</style>
```

### 02 元素选择器

为页面中==某种元素==统一设置样式

```html
<style>
	h1 {
		color: red;
	}
</style>
```

### 03 类选择器

类名不以数字开头

```html
<style>
	.call-me {
		color: red;
	}
</style>

<p class="call-me">呼唤</p>
```

### 04 id选择器

id不以数字开头

```html
<style>
	#call-me {
		color: red;
	}
</style>

<p id="call-me">呼唤</p>
```

## 2. 复合选择器

### 01 交集选择器

```html
<style>
	/* 选择既是p标签又是类名为.ani的，紧紧挨着，必须以元素开始 */
	p.ani {
		color: red;
	}
	.ani.ani2 {
		color: red;
	}
</style>

<p class="ani">小狗</p>
<p class="ani">小猪</p>
<p class="ani2">小羊</p>
```

### 02 并集选择器

```html
<style>
	/* 选择类名为.ani或类名为.ani2的*/
	.ani, 
	.ani2 {
		color: red;
	}
</style>

<p class="ani">小狗</p>
<p class="ani">小猪</p>
<p class="ani2">小狗</p>
```

### 03 后代选择器

```html
<style>
	.call li {
		color: red;
	}
	/* 也可以 */
	ul li {
		color: red;
	}
</style>

<ul class="call">
	<li></li>
	<li></li>
	<li></li>
</ul>
```

### 04 子代选择器

```html
<style>
	div > a {
		color: red;
	}
</style>

<div>
	<a href="#"></a>
	
	<p><a href="#"></a></p>
</div>
```

### 05 兄弟选择器

```html
<style>
	/*div 紧紧相邻的兄弟元素 p*/
	div + p {
		color: red;
	}

	/*div 所有的兄弟元素 p*/
	div ~ p {
		color: red;
	}
</style>

<div>
	<p>小狗</p>
	<div>小猪</div>
	<p>小猫</p>
	<p>小鸟</p>
</div>
```

### 06 属性选择器

```html
<style>
	/*具有title属性的元素*/
	[title] {
		color: red;
	}

	/*具有title属性的，且属性值为dog的元素*/
	[title="dog"] {
		color: red;
	}

	/*具有title属性的，且属性值以字母p开头的元素*/
	[title^="p"] {
		color: red;
	}

	/*具有title属性的，且属性值以字母t结尾的元素*/
	[title$="p"] {
		color: red;
	}

	/*具有title属性的，且属性值包含字母r的元素*/
	[title*="r"] {
		color: red;
	}
</style>

<div>
	<div title="dog">小狗</div>
	<div title="pig">小猪</div>
	<div title="cat">小猫</div>
	<div title="bird">小鸟</div>
</div>
```

## 3. 伪类选择器

### 01 动态伪类

```html
<style>
	/* 选中没被访问过的a标签 */
	a:link {
		color: red;
	}

	/* 选中访问过的a标签 */
	a:visited {
		color: blue;
	}

	/* 选中鼠标悬浮状态的a标签 */
	a:hover {
		color: orange;
	}

	/* 选中激活状态的a标签 */
	/* 激活：按下鼠标不松开 */
	a:active {
		color: gray;
	}

	/* 选中获取焦点的input标签 */
	input:focus {
		color: gray;
		background-color: green;
	}
	/* 选中有输入值的input标签 */
	input:valid {
		color: gray;
		background-color: green;
	}
</style>

<div>
	<a href="#"></a>
	<a href="#"></a>
	<input type="text">
	<input type="password">
</div>
```

### 02 结构伪类

```html
<style>
	/* 选中的是div的第一个子代 p */
	/* last-child 选中的是div的最后一个子代 p */
	div>p:first-child {
		color: red;
	}
</style>

<div>

	<div>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 
		选择不到span标签下的第一个p标签，
		选中的是div的第一个子代p元素，
		并且一定是div的第一个元素
	*/
	div>p:first-child {
		color: red;
	}
</style>

<div>
	<div>
		<span>小猪</span>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>

</div>
```

```html
<style>
	/* 选中的p元素，且p的父级是谁无所谓，
		但p必须是其父亲的第一个儿子 */
	p:first-child {
		color: red;
	}
</style>

<div>

	<div>
		<div>
			<p>小猪</p>
		</div>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 选中的是div的第n个子代p元素*/
	p:nth-child(2) {
		color: red;
	}
</style>

<div>

	<div>
		<p>小猪</p>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 选中的是div的第双数个子代p元素
		偶数：2n or even
		奇数：2n+1 or odd
		前三个：-n+3
	*/
	p:nth-child(2n) {
		color: red;
	}
</style>

<div>

	<div>
		<p>小猪</p>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 
		选中的是div的第一个子代p元素，
		并且一定是在同类型的兄弟元素里选
		nth-of-type同理
	*/
	div>p:first-of-type(2) {
		color: red;
	}
</style>

<div>

	<div>
		<span>小猪</span>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 
		选中的是div中倒数的第n个子代p元素，
		并且是在所有的兄弟元素里选
	*/
	div>p:nth-last-child(2) {
		color: red;
	}
</style>

<div>

	<div>
		<span>小猪</span>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 
		选中的是div中倒数的第n个子代p元素，
		并且是在所有同类型的兄弟元素里选
	*/
	div>p:nth-last-of-type(2) {
		color: red;
	}
</style>

<div>

	<div>
		<span>小猪</span>
		<p>小狗</p>
		<p>小猫</p>
		<p>小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 
		选中的是div中只有子代span元素
	*/
	span:only-child {
		color: red;
	}
</style>

<div>
	<span></span>
	<span></span>
</div>
<div>
	<span>小猪</span>
	<p>小狗</p>
	<p>小猫</p>
	<p>小鸟</p>
</div>
```

```html
<style>
	/* 
		选中的是div中子代没有同类型的span元素
	*/
	span:only-of-type {
		color: red;
	}
</style>

<div>
	<span></span>
	<span></span>
</div>
<div>
	<span>小猪</span>
	<p>小狗</p>
	<p>小猫</p>
	<p>小鸟</p>
</div>
```

```html
<style>
	/* 
		选中的是html根元素
	*/
	:root {
		background-color: red;
	}
</style>

<div>
	<span></span>
</div>

```

```html
<style>
	/* 
		选中的是没有任何元素的div
	*/
	div:empty {
		background-color: red;
	}
</style>

<div>
	
</div>

```

### 03 否定伪类

```html
<style>
	/* 
		选中的是div中的子代p元素，
		但是排除类名为fail
	*/
	div>p:not(.fail) {
		color: red;
	}
</style>

<div>

	<div>
		<p>小猪</p>
		<p>小狗</p>
		<p>小猫</p>
		<p class="fail">小鸟</p>
	</div>
	
</div>
```

```html
<style>
	/* 
		选中的是div中的子代p元素，
		但是排除第一个子代p元素
	*/
	div>p:not(:first-child) {
		color: red;
	}
</style>

<div>

	<div>
		<p>小猪</p>
		<p>小狗</p>
		<p>小猫</p>
		<p class="fail">小鸟</p>
	</div>
	
</div>
```

### 04 UI伪类

```html
<style>
	/* 
		选中的是勾选的复选框或单选框按钮
	*/
	input:checked {
		width: 100px;
		height: 100px;
	}

	/* 
		选中的是被禁用的input元素
	*/
	input:disable {
		width: 100px;
		height: 100px;
	}
</style>

<div>
	<input type="checkbox">
	<input type="radio" name="gender">
	<input type="radio" name="gender">
</div>
```

### 05 目标伪类

```html
<style>
	/* 选中的是锚点指向的元素 */
	div:target {
		background-color: red;
	}
</style>
<a href="#one"></a>
<a href="#two"></a>
<div id="one">第一个</div>
<div id="two">第二个</div>
```

### 06 语言伪类

```html
<style>
	/* 选中的是语言为en的元素 */
	div:lang(en) {
		background-color: red;
	}
</style>
<div id="one" lang="en">第一个</div>
<div id="two">第二个</div>
```

### 07 伪元素选择器

伪元素是元素中的一些特殊位置

```html
<style>
	/* 选中的是div中的第一个文字 */
	div::first-lettet {
		color: red;
		font-size: 40px;
	}

	/* 选中的是div中的第一行文字 */
	div::first-line {
		background-color: red;
	}

	/* 选中的是div中被选中的文字 */
	div::selection {
		color:orange
	}

	/* 选中的是input中提示的文字 */
	input::placeholder {
		background-color: red;
		color:orange
	}

	/* 选中的是p元素最开始的位置，随后创建一个子元素 */
	p::before {
		content: "￥";
	}

	/* 选中的是p元素最后的位置，随后创建一个子元素 */
	p::after {
		content: ".00"
	}
</style>
<div id="two">hello world</div>

<input type="text" placeholder="请输入">

<p>199</p>
<p>299</p>
```

## 选择器优先级

### 01 基本选择器优先级

!important > 行内样式 > [[CSS#04 id选择器|ID选择器]] > [[CSS#03 类选择器|类选择器]] > [[CSS#02 元素选择器|元素选择器]] > [[CSS#01 通配选择器|通配选择器]]

### 02 复合选择器优先级

**权重计算**

格式：(a, b, c)
1. a：ID选择器的个数
2. b：类、伪类、属性选择器的个个数
3. c：元素、伪元素选择器的个数
4. 从a到c开始比较，当比较到一个数字大的则停止比较，数字大的胜出。
5. 当 (a, b, c) 相同，则以后写的为准
  
**!important**

```html
<style>
	p{
		color: red !important;
	}
</style>
```

# 四、CSS 三大特性

## 1. 层叠性

## 2. 继承性

### 01 继承最近属性

### 02 可继承属性

字体属性、文本属性（除了vertical-align）、文字颜色等

### 03 可继承属性

边框、背景、内边距、外边距、宽高、溢出方式等

## 3. 优先级

!important > 行内样式 > [[CSS 选择器#04 id选择器|ID选择器]] > [[CSS 选择器#03 类选择器|类选择器]] > [[CSS 选择器#02 元素选择器|元素选择器]] > * >继承的样式

# 五、像素 与 颜色

## 1. 像素

pixel，简称px

## 2. 颜色
color
### 01 RGB

rgb(red, green, blue)

```css
h1{
	color: rgb(138, 43, 226)
}
h2{
	color: rgb(100%, 0%, 0%)
}
```

### 02 RGBA

rgb(red, green, blue, alpha)

```css
h1{
	color: rgb(138, 43, 226, 0.5)
}
h2{
	color: rgb(100%, 0%, 0%, .5)
}
```

### 03 HEX

#(red green blue)

00 为最小值，等同RGB的0；ff为最大值，等同RGB的255。

```css
h1{
	color: #ffccdd;
}
h2{
	color: #fcd
}
```

### 04 HEXA

#(red green blue alpha)

```css
h1{
	color: #ffccdd00;
}
h2{
	color: #fcd0
}
```

### 05 HSL

hsl(色相（角度），饱和度（百分比），亮度（百分比）)

```css
h1{
	color: hsl(hue, saturation, lightness)
}
h2{
	color: hsl(0deg, 50%, 50%)
}
```

### 06 HSLA

hsla(色相（角度），饱和度（百分比），亮度（百分比），透明度)

```css
h1{
	color: hsl(hue, saturation, lightness, alpha)
}
h2{
	color: hsl(0deg, 50%, 50%, 50%)
}
```

# 六、文字

## 1. 字体大小
font-size
```css
h1{
	font-size: 24px;
}
```

1. 由于==字体设计==原因，文字最终呈现的大小，并不一定与font-size的值一致，可能大，也可能小。
2. 通常情况下，文字相对字体设计框，并不是垂直居中的，通常都靠下一些。
3. ![[屏幕截图 2023-07-01 103917.png]]

## 2. 字体族
font-family
### 01 衬线字体

如楷体

### 02 非衬线字体

如微软雅黑

### 03 等宽字体

如 JetBrains Mono

```css
/* 默认微软雅黑 */
/* 若前边字体不存在或错误，则向电脑申请 非衬线字体 */
h1{
	font-family: "JetBrains Mono", "Microsoft YaHei", sans-serif;
}
```

## 3. 字体风格
font-style
```css
/* 默认微软雅黑 */
h1{
	font-style: normal;
	font-style: italic;
	font-style: oblique;
}
```

## 4. 字体粗细
font-weight
```css
/* 默认微软雅黑 */
h1{
	font-weight: lighter;
	font-weight: 100;
	font-weight: normal;
	font-weight: bold;
	font-weight: bolder;
}
```

## 5. 字体复合属性
font
```css
/* 默认微软雅黑 */
/* 
	字体族，字体大小必须写
	最后一位一定为字体族，倒数第二位一定为字体大小
*/
h1{
	font:  100px "微软雅黑";
}
```


## 6. 文字颜色

==行内元素==或==行内块元素==在父元素里可当作文本处理

```css
/* 默认微软雅黑 */
h1{
	color: red;
}
```

## 7. 文本间距

```css
/* 默认微软雅黑 */
h1{
	/* 字母间距 */
	letter-spacing: 10px;

	/* 单词间距 */
	word-spacing: -10px;
}
```

## 8. 文本修饰

```css
/* 默认微软雅黑 */
h1{
	/* 上划线 */
	text-decoration: overline;

	/* 下划线 */
	text-decoration: underline;

	/* 下划的绿色虚线 */
	text-decoration: underline dotted green;

	/* 删除线 */
	text-decoration: line-through;

	/* 单词间距 */
	text-decoration: none;
}
```

## 9. 文本缩进

```css
/* 默认微软雅黑 */
h1{
	font-size: 40px;
	text-indent: 80px;
}
```

## 10. 文本对齐

### 01 水平对齐

```css
/* 默认微软雅黑 */
h1{
	text-align: left;
	text-align: center;
	text-align: right;
}
```

### 02 垂直对齐

顶部：默认就是顶部对齐

居中（单行文字）：让height = line-height即可

底部（单行文字）：让line-height = （height × 2）- font-size即可

## 11. 行高

### 01 语法

```css
/* 默认微软雅黑 */
h1{
	/* 值为像素 */
	line-height: 40px;
	
	/* 值为字母 */
	line-height: normal;
	
	/* 值为倍数 常用*/
	line-height: 1.2;
	
	/* 值为百分比 */
	line-height: 120%;
	
}
```

### 02 注意点

当设置行高line-height过小时，文字产生重叠，且最小值为0，不能为负数。

### 03 行高具有继承性

为了减少计算量，最好写数值

### 04 height 与 line-height 关系

1. 设置了height，那么高度就是height的值

2. 不设置height，那么高度为line-height * 行数

# 七、元素属性

## 01 列表属性


```css
ul{
	/* 列表符号 */
	list-style-type:decimal;
	
	/* 列表符号的位置 */
	list-style-position: inside;
	
	/* 自定义列表符号 */
	list-style-image: url("../photo.jpg");
}
```

## 02 表格属性

```css
table {
	border: 2px red solid;

	/* 控制表格的列宽 */
	table-layout: fixed;
	
	/* 控制单元格间距 */
	border-spacing: 0px;
	
	/* 合并相邻单元个的边框 */
	border-collapse: collapse;
	
	/* 隐藏没有内容的单元格 */
	empty-cells: hide;
}
td, th {
	border: 2px orange solid;
}
```

## 03 背景属性

```css
div {
	/* 设置背景颜色 */
	background-color: red;
	
	/* 控设置背景图片 */
	background-image: url("../photos.jpg");
	
	/* 设置背景图片的重复方式 */
	background-repeat: no-repeat;
	background-repeat: repeat-x;
	background-repeat: repeat-y;
	
	/* 设置背景图片的位置 */
	background-position: left top;
	background-position: 10px 10px;

	/* 复合属性 */
	background: ;
}
```

## 04 鼠标属性

```css
div {
	cursor: pointer;
	cursor: url("../photos.jpg"), pointer;
}
```

# 八、长度单位

## 01 px 

像素

```css
/* 默认微软雅黑 */
h1{
	font-size: 30px;
}
```

## 02 em 

相对于当前元素的font-size的倍数

```css
/* 默认微软雅黑 */
h1{
	width: 10em;
	height: 10em;
	font-size: 20px;
}
```

## 03 rem 

相对于根元素的font-size的倍数

```css
/* 默认微软雅黑 */
h1{
	font-size: 2em;
}
```

## 04 % 

相对于父元素的font-size的倍数

```css
/* 默认微软雅黑 */
h1{
	font-size: 30%;
}
```

# 九、盒模型

## 1. content

```css
div {
	min-width: 600px;
	max-width: 1000px;

	min-height: 300px;
	max-height: 600px;
}
```

## 2. padding

```css
div {
	/* 左侧内边距 */
	padding-left:20px;
	/*、上内边距：*/
	padding-top: 30px;
	/*右侧内边距：*/
	padding-right:40px;
	/*底内边距*/
	padding-bottom: 50px;
	/*写一个值，含义：四个方向的内边距是一样的*/
	padding:20px;
	/* 写两个值，含义：上下、左右 */
	padding: 10px 20px;
	/* 写三个值；含义：上、左右、下 */
	padding:10px 20px 30px;
	/* 写四个值；含义：上、右、下、左 */
	padding:10px 20px 30px 40px;
}
```

## 3. border

```css
div {
	border: 10px red solid;
	border-left: 10px red solid;
	border-top: 10px red solid;
	border-right: 10px red solid;
	border-bottom: 10px red solid;
}
```

## 4. margin

### 01 语法

```css
div {
	/* 左侧外边距 */
	/* 会影响自身位置 */
	margin-left:20px;
	/* 上外边距 */
	/* 会影响自身位置 */
	margin-top: 30px;
	
	/* 右侧外边距 */
	/* 会影响兄弟元素位置 */
	margin-right:40px;
	/* 底外边距 */
	/* 会影响兄弟元素位置 */
	margin-bottom: 50px;

	/* 写一个值，含义：四个方向的内边距是一样的 */
	margin:20px;
	/* 写两个值，含义：上下、左右 */
	margin: 10px 20px;
	/* 写三个值；含义：上、左右、下 */
	margin: 10px 20px 30px;
	/* 写四个值；含义：上、右、下、左 */
	margin: 10px 20px 30px 40px;
}
```

### 02 注意点

子元素的外边距是相对于父元素的content计算的；

上margin、左margin会影响自身位置， 下margin、右margin会影响兄弟元素位置；

块级元素，行内块元素，四个方向都可以设置margin，对于行内元素来说，上下margin不起作用；

margin的值也可以是auto，给一个块级元素设置左右margin都为auto，则在父元素水平居中；

### 03 margin塌陷问题

[margin塌陷及解决方法](https://blog.csdn.net/qq_35727582/article/details/122189322)

#### 解决办法

1. 设置宽度不为0的padding；
2. 设置宽度不为0的border；
3. 给父元素添加属性overflow: hide;

### 04 margin合并问题

[margin重合(外边距重叠)及解决方法](https://blog.csdn.net/liuye066/article/details/124967167)

#### 01 哪些元素会发生外边距重叠问题

外边距的重叠只产生在普通流文档的上下外边距之间， 只有 块元素 会发生外边距重叠，行内元素 和 行内块元素 都不会发生外边距重叠问题

#### 02 什么情况下会发生外边距重叠呢

1. 相邻兄弟元素的marin-bottom和margin-top的值发生重叠，发生边界重叠，只会挑选最大边界范围留下

2. 父级和第一个/最后一个子元素的margin合并，当同时设父元素和子元素的margin-top都为50px时，父元素和子元素都距离边界50px

#### 03 解决方法：

1. 给父元素加overflow：hidden；

这种方法解决了我们外边距重叠问题，但是这个方法只适用于 “子元素的高度加上外边距高度小于父元素高度(childHeight +margin-top<parentHeight)” ，不然子元素部分内容就会被隐藏掉

2. 给父元素加边框 border（可以加个透明的边框）

3. 给父级或者子级设置display:inline-block;

既然只有块元素会产生外边距重叠，那么我们就让它不是块元素，把它设置为行内块元素

4. 给父级或者子级设置float

5. 给父级或者子级设置position: absolute;

6. 给父元素添加padding

## 5. 隐藏内容

### 01 overflow

```css
div {
	overflow: hidden;
}
```

### 02 visibility

```css
div {
	visibility: show;
	visibility: hidden;
}
```

### 03 display

```css
div {
	display: none;
}
```

# 十、布局

**行内元素、行内块元素，可以被父元素当做文本外理。**
即：可以像处理文本对齐一样，去处理：行内、行内块在父元素中的对齐。
例如：text-align、line-height、text-indent等。

## 1. 水平居中

若子元素为块元素，给父元素加上：margin: 0 auto；
若子元素为行内元素、行内块元素，给父元素加上：text-align：center。

## 2. 垂直居中

若子元素为块元素，给子元素加上：margin-top，值为：（父元素content -子元素盒子总高)/2

若子元素为行内元素、行内块元素：
让父元素的height = line-height，每个子元素都加上：vertical-align: middle;

补充：若想绝对垂直居中，父元素font-size设置为0。

## 3. 空白问题

### 01 行内块元素的空白

1. 行内块设置vertical，值不为baseline
2. 设置为display： block；
3. 给父元素设置font-size：0；

```css
父元素 {
	
}

img {
	display: block;
}
```

### 02 元素之间的空白

行内元素、行内块元素，彼此之间的换行会被浏览器解析为一个空白字符。

解决：给父元素设置font-size：0；

# 十一、浮动

## 1. 浮动后的特点

1. 脱离标准文档流，不占位置；
2. 浮动元素不会压住父元素的边框、内容和图片，只会围绕着浮动元素；
3. 浮动的元素顶对齐；
4. 浮动的元素设置宽高生效，具有行内块的特点，不会像行内块一样被当作文本处理；
5.  不能用text-align: center;因为脱标了所以盒子不能居中；
6. 不管浮动前是什么元素，浮动后，默认宽高都是被内容撑开的。

## 2. 浮动后的影响

元素浮动，后面标准流会上来把没浮动元素之前的位置占了，浮动元素会压住后面上来的标准流，不会对前面的标准流造成影响，如果不[清除浮动](https://blog.csdn.net/xxx857857857/article/details/126860306?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168828921416800213011517%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168828921416800213011517&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-126860306-null-null.142^v88^control_2,239^v2^insert_chatgpt&utm_term=%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8&spm=1018.2226.3001.4187)的话，常常出现**高度塌陷**现象；即：

对兄弟元素的影响：后面的兄弟元素，会占据浮动元素之前的位置，再浮动元素的下面；对前边的兄弟无影响。

对父元素的影响：不能撑起父元素的高度，导致父元素高度塌陷；但父元素的宽度依旧束缚浮动的元素。

## 3. 解决浮动后的影响

[清除浮动影响](https://blog.csdn.net/xxx857857857/article/details/126860306?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168828921416800213011517%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168828921416800213011517&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-126860306-null-null.142^v88^control_2,239^v2^insert_chatgpt&utm_term=%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8&spm=1018.2226.3001.4187)

# 十二、定位

## 1. 相对定位

### 01 设置相对定位

给元素设置 ==position: relative;== 即可实现相对定位。
可以使用 left 、 right 、 top 、 bottom 四个属性调整位置。

### 02 相对定位的参考点

相对自己原来的位置（包括计算了float）

### 03 相对定位的特点:

1. 不会脱离文档流，元素位置的变化，只是视觉效果上的变化，不会对其他元素产生任何影响。
2. 定位元素的显示层级比普通元素高，无论什么定位，显示层级都是一样的。默认规则是:定位的元素会盖在普通元素之上。都发生定位的两个元素，后写的元素会盖在先写的元素之上。
3. left 不能和 right 一起设置， top 和 bottom 不能一起设置。
4. 相对定位的元素，也能继续浮动，但不推荐这样做。
5. 相对行为的元素，也能通过 margin 调整位置，但不推荐这样做。
6. 绝大多数情况下，相对定位，会与绝对定位配合使用。

## 2. 绝对定位

### 01 设置绝对定位

给元素设置 ==position: absolute;== 即可实现绝对定位
可以使用 left 、 right 、 top 、 bottom 四个属性调整位置。

### 02 绝对定位的参考点

参考它的包含块。
什么是包含块?
包含块就是父元素对于没有脱离文档流的元
包含块是第拥有定位属性的祖先元素 (如果所有祖先都没定位，那包对于脱离文档流的元素2含块就是整个页面)

### 03 绝对定位元素的特点

1. 脱离文档流，会对后面的兄弟元素、父元素有影响。
2. left 不能和 right 一起设置， top 和 bottom 不能一起设置。
3. 绝对定位、浮动不能同时设置，如果同时设置，浮动失效，以定位为主。
4. 绝对定位的元素，也能通过 margin 调整位置，但不推荐这样做。
5. 无论是什么元素 (行内、行内块、块级) 设置为绝对定位之后，都变成了定位元素。
6. 何为定位元素?- 默认宽、高都被内容所撑开，且能自由设置宽高。

## 3. 固定定位

### 01 设置为固定定位

给元素设置 ==position: fixed;== 即可实现固定定位。
可以使用 left 、 right 、 top 、 bottom 四个属性调整位置

### 02 固定定位的参考点

参考它的视口
什么是视口?-- 对于 PC 浏览器来说，视口就是我们看网页的那扇“窗户”

### 03 固定定位元素的特点

1. 脱离文档流，会对后面的兄弟元素、父元素有影响。
2. left 不能和 right 一起设置，top 和 bottom 不能一起设置,固定定位和浮动不能同时设置，如果同时设置，浮动失效，以固定定位为主。
3. 固定定位的元素，也能通过 margin 调整位置，但不推荐这样做.
4. 无论是什么元素(行内、行内块、块级)设置为固定定位之后，都变成了定位元素。

## 4. 粘性定位

### 01 设置为粘性定位

给元素设置 position:sticky 即可实现粘性定位。
可以使用 left、 right 、 top 、 bottom 四个属性调整位置，不过最常用的是 top 值.

### 02 粘性定位的参考点

离它最近的一个拥有“滚动机制”的祖先元素，即便这个祖先不是最近的真实可滚动祖先。

### 03 粘性定位元素的特点

1. 不会脱离文档流，它是一种专门用于窗口滚动时的新的定位方式。
2. 最常用的值是 top 值。
3. 粘性定位和浮动可以同时设置，但不推荐这样做。
4. 粘性定位的元素，也能通过 margin 调整位置，但不推荐这样做。
5. 粘性定位和相对定位的特点基本一致，不同的是:粘性定位可以在元素到达某个位置时将其固定。

## 5. 定位层级

1. 定位元素的显示层级比普通元素高，无论什么定位，显示层级都是一样的。
2. 如果位置发生重叠，默认情况是: 后面的元素，会显示在前面元素之上。
3. 可以通过 css 属性 -index 调整元素的显示层级
4. z-index 的属性值是数字，没有单位，值越大显示层级越高。
5. 只有定位的元素设置 z-index 才有效
6. 如果 z-index 值大的元素，依然没有覆盖掉 z-index 值小的元素，那么请检查其包含块的层级

## 6. 定位特殊应用

### 01 让定位元素的宽充满包含块

块宽想与包含块一致，可以给定位元素同时设置 left 和 right 为 0。高度想与包含块一致，top 和 bottom 设置为 。

### 02 让定位元素在包含块中居中

```css
div {
	width: 100px;
	height: 100px;
	position: absolute;
	left: 0;
	right :0;
	top: 0;
	bottom: 0;
	margin: auto ;
}
```

该定位的元素必须有宽高

### 03 定位特点

1. 定位无视padding，因为定位是相对盒子的，padding在盒子里。
2. 注意:发生固定定位、绝对定位后，元素都变成了定位元素，默认宽高被内容撑开，且依然可以设置宽高。
3. 发生相对定位后，元素依然是之前的显示模式。
4. 以下所说的特殊应用，只针对 绝对定位 和 固定定位 的元素，不包括相对定位的元素。

# 十三、CSS3

## 1. 新增长度单位

### 01 vw

是[[CSS#02 固定定位的参考点|视口]]宽度的百分比；

```css
div {
	width: 40vw;
	height: 20vw
}
```

### 02 vh

是[[CSS#02 固定定位的参考点|视口]]高度的百分比

```css
div {
	width: 40vh;
	height: 20vh;
}
```

### 03 vmax

是[[CSS#02 固定定位的参考点|视口]]宽度或高度的百分比，选用最大的；

```css
div {
	width: 40vmax;
	height: 20vmax;
}
```

### 04 vmin

是[[CSS#02 固定定位的参考点|视口]]宽度或高度的百分比，选用最小的。

```css
div {
	width: 40vmin;
	height: 20vmin;
}
```

## 2. 新增盒子属性

### 01 box-sizing

1. 默认值content-box
2. 可选值border-box

```css
div {
	width: 200px;
	height: 20opx;
	box-sizing: border-box;
}
```

### 02 resize

1. 默认值none
2. 可选值vertical，horizontal，vertical
3. 与overflow配合使用

```css
div {
	width: 200px;
	height: 20opx;
	resize: both;
	overflow: hidden;
}
```

### 03 box-shadow

#### 1 语法:

box-shadow: h-shadow v-shadow blur spread color inset;

#### 2 值的含义

1. h-shadow：必填，水平阴影的位置，可以为负值
2. v-shadow：必填，垂直阴影的位置，可以为负值
3. blur：可选，模糊距离
4. spread：可选，阴影的外延值
5. color：可选，阴影的颜色
6. inset：可选，将外部阴影改为内部阴影

#### 3 默认值

box-shadow: none 表示没有阴影

```css
div {
	width: 200px;
	height: 20opx;
	/* 写两个值，含义：水平位置 垂直位置 */
	box-shadow: 10px 10px;

	/* 写三个值，含义：水平位置 垂直位置 阴影颜色 */
	box-shadow: 10px 10px gray;
	
	/* 写三个值，含义：水平位置 垂直位置 模糊程度 */
	box-shadow: 10px 10px 20px;
	
	/* 写四个值，含义：水平位置 垂直位置 模糊程度 阴影颜色 */
	box-shadow: 10px 10px 20px gray;

	/* 写五个值，含义：水平位置 垂直位置 模糊程度 外延程度 阴影颜色 */
	box-shadow: 10px 10px 20px 10px gray;
	
	/* 写五个值，含义：水平位置 垂直位置 模糊程度 外延程度 阴影颜色 内阴影*/
	box-shadow: 10px 10px 20px 10px gray inset;
}
```

### 04 opacity 不透明度

1. 默认值1
2. 可选值0到1

```css
div {
	width: 200px;
	height: 20opx;
	opacity: 0.8;
}
```

## 3. 新增背景属性

### 01 background-origin

相对于内容框来定位背景图像

1. 默认值padding-box：背景图像相对于内边距框来定位。
2. 可选值border-box：背景图像相对于边框盒来定位。
3. 可选值content-box：背景图像相对于内容框来定位。

```css
div {
	width: 200px;
	height: 20opx;
	background-origin: content-box;
}
```

### 02 background-clip

规定背景的绘制区域

1. 默认值border-box：背景被裁剪到边框盒。
2. 可选值content-box：背景被裁剪到内容框。
3. 可选值padding-box：背景被裁剪到内边距框。

```css
div {
	width: 200px;
	height: 200px;
	background-clip: content-box;
}
```

### 03 background-size

设置背景的尺寸

1. 用长度值指定背景图片大小，不允许负值。
2. 用百分比指定背景图片大小，不允许负值。
3. 默认值auto：背景图片的真实大小。
4. 可选值contain : 将背景图片等比缩放，使背景图片的宽或高，与容器的宽或高相等，再将完整背景图片包含在容器内，但要注意:可能会造成容器里部分区域没有背景图片。
5. 可选值cover: 将背景图片等比缩放，直到完全覆盖容器，图片会尽可能全的显示在元素上，但要注意:背景图片有可能显示不完整。

```css
div {
	width: 200px;
	height: 20opx;
	background-size: cover;
}
```

### 04 background-复合属性

```css
div {
	width: 200px;
	height: 20opx;
	background: color url repeat position size origin clip;
}
```

## 4. 新增边框属性

### 01 border-radius 边框圆角

```css
div {
	border: 10px;
	border-top-left-radius: 10px;
	border-top-right-radius: 10px;
	border-bottom-left-radius: 10px;
	border-bottom-left-radius: 10px;
	/* 椭圆角 */
	border-top-left-radius: 100px 50px;
}
```

### 02 outline 边框外轮廓

outline-width
outline-color
outline-style
outline-offset

## 5. 新增文本单位

### 01 text-shadow 文本阴影

类似[[CSS#03 box-shadow|box-shadow]]

### 02 white-space 文本换行

1. 属性指定元素内的空白怎样处理。
2. 默认值normal
3. 可选值pre：表示按原文显示
4. 可选值pre-line：表示按原文显示并将超出区域元素换行
5. 可选值nowrap：文本不会换行，文本会在在同一行上继续，直到遇到```<br>```标签为止。
6. 可选值inherit：规定应该从父元素继承 white-space 属性的值。

### 03 text-overflow 文本溢出

```css
div {
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}
```

### 04 text-decoration 文本修饰

text-decoration-line：
text-decoration-style：
text-decoration-color：

### 05 text-stroke 文本描边

text-stroke-color

## 6. 新增渐变

### 01 线性渐变

#### 1 默认情况（从上到下）

```css
div {
	background-image: linear-gradient(red, yello, blue);
}
```

#### 2 关键词修改渐变方向（从左下到右上）

```css
div {
	background-image: linear-gradient(to right top, red, yello, blue);
}
```

#### 3 角度修改渐变方向（从左下到右上）

```css
div {
	background-image: linear-gradient(30deg, red, yello, blue);
}
```

#### 4 渐变颜色的区域（从上到下）

```css
div {
	background-image: linear-gradient(red 50px, yello 100px, blue 150px);
}
```

### 02 径向渐变

#### 1 默认情况（从里到外）

```css
div {
	background-image: radial-gradient(red, yello, blue);
}
```

####  2 关键词调整渐变圆心（从里到外）

```css
div {
	background-image: radial-gradient(at right top, red, yello, blue);
}
```

#### 3 像素值调整渐变圆心（从里到外）

```css
div {
	background-image: radial-gradient(at 100px 50px, red, yello, blue);
}
```

#### 4 circle调整渐变为正圆（从里到外）

```css
div {
	background-image: radial-gradient(circle, red, yello, blue);
}
```

#### 5 像素值调整渐变为正圆（从里到外）

```css
div {
	background-image: radial-gradient(200px 200px, red, yello, blue);
}
```

#### 6 渐变颜色的区域（从上到下）

```css
div {
	background-image: radial-gradient(red 50px, yello 100px, blue 150px);
}
```

### 03 重复渐变

```css
div {
	background-image: repeating-radial-gradient(red 50px, yello 100px, blue 150px);
}
```

## 7. 2D变换

### 01 2D位移

```css
div {
	/* 向右位移 */
	transform: translateX(50px);

	/* 向右位移 */
	transform: translateX(50%);
	
	/* 向下位移 */
	transform: translateY(50px);

	/* 向下位移 */
	transform: translateX(50px) translateY(50px);
	
	/* 向右位移 */
	transform: translate(50px);
	
	/* 向右下位移 */
	transform: translate(50px, 50px);
}
```

相对定位对的百分比值，参考的是其父元素；定位的百分比值，参考的是自身。
位移对行内元素无效


### 02 2D缩放

```css
div {
	/* 横向放大 */
	transform: scaleX(1.5);
	
	/* 横向镜像 */
	transform: scaleX(-1);

	/* 同时设置水平和垂直缩放 */
	transform: scale(1.5);
	
	/* 水平缩放，垂直缩放 */
	transform: scale(1.5, 1.5);
}
```

### 03 2D旋转

```css
div {
	/* 顺时针旋转 */
	transform: rotateZ(30deg);
	
	/* 逆时针旋转 */
	transform: rotateZ(-30deg);
}
```

### 04 2D扭曲

```css
div {
	/* 横向扭曲 */
	transform: skewX(30deg);
	
	/* 纵向扭曲 */
	transform: skewY(30deg);

	/* 一个值代表skewX */
	transform: skewY(30deg);
}
```

### 05 多重变换

```css
div {	
	transform: translate(50px, 50px)
				scale(0.8)
				rotate(30deg);
}
```

### 06 变换原点

```css
div {
	width: 200px;
	height: 200px;
	
	transform-origin: left top;
	
	transform-origin: 50px 50px;
}
```

## 8. 3D变换

### 01 空间与景深

```css
/* 给父元素开启3D空间和景深 */
div {
	width: 200px;
	height: 200px;
	
	/* 开启3D空间 */
	transform-style: preserve-3d;
	
	/* 开启景深 */
	perspective: 500px;
}
```

### 02 透视点位置（观察者的位置）

```css
/* 给父元素开启3D空间和景深 */
div {
	width: 200px;
	height: 200px;
	
	/* 开启3D空间 */
	transform-style: preserve-3d;
	
	/* 开启景深 */
	perspective: 500px;

	/* 设置透视点位置 */
	perspective-origin: 300px 100px;
}
```

### 03 3D位移

```css
/* 给父元素开启3D空间和景深 */
div1 {
	width: 200px;
	height: 200px;
	
	/* 开启3D空间 */
	transform-style: preserve-3d;
	
	/* 开启景深 */
	perspective: 500px;

	/* 设置透视点位置 */
	perspective-origin: 300px 100px;
}

div2 {
	width: 200px;
	height: 200px;
	
	transform: translateZ(200px);
	transform: translate3d(x, y, z);
	transform: translate3d(100px, 100px, 100px);
}
```

### 04 3D旋转

```css
div {
	/* 从元素右边看，顺时针旋转 */
	transform: rotateX(30deg);
	
	/* 逆时针旋转 */
	transform: rotateY(30deg);
}
```

### 05 3D缩放

### 06 多重变换

## 9. 过渡

### 01  过渡的属性

```css
div {
	/* 设置哪个属性需要过渡效果 */
	transition-property: width, height;

	/* 让所有能过渡的属性都过渡 */
	transition-property: all;
}
```

### 02  过渡时间

```css
div {
	/* 设置过渡时间 */
	transition-duration: 1s, 2s;
}
```

### 03 过渡延时

```css
div {
	/* 设置过渡延时 */
	transition-delay: 1s;
}
```

### 04  过渡效果

```css
div {
	/* 设置过渡效果 */
	transition-timing-function: ease;
	transition-timing-function: linear;
	transition-timing-function: ease-in;
	transition-timing-function: ease-out;
	transition-timing-function: ease-in-out;
	transition-timing-function: step-start;
	transition-timing-function: step-end;
	transition-timing-function: steps(20, start);
	transition-timing-function: cubic-bezier(.8, 1.02, 1.3, .7);
}
```

### 05  过渡复合属性

```css
div {
	transition: 1s all 0.5s linear;
}
```
## 10. 动画

### 01  定义关键帧

```css
/* 定义一组关键帧 */
@keyframes toright{
	from {
	}
	to {
		transform: translate(100px);
		background-color: red;
	}
}

@keyframes toright{
	0% {
	}
	100% {
		transform: translate(100px);
		background-color: red;
	}
}
```

### 02 应用动画

```css
div {
	/* 应用动画 */
	animation-name: toright;
}
```

### 03 动画时间

```css
div {
	/* 设置动画时间 */
	animation-duration: 1s, 2s;
}
```

### 04 动画延时

```css
div {
	/* 设置动画延时 */
	animation-delay: 1s;
}
```

### 05 动画方式

```css
div {
	/* 设置动画方式 */
	animation-timing-function: linear;
}
```

### 06 动画播放次数

```css
div {
	/* 设置动画播放次数 */
	animation-iteration-count: 1;

	/* 无限循环 */
	animation-iteration-count: infinite;
}
```

### 07 动画方向

```css
div {
	/* 正常方向 */
	animation-direction: normal;

	/* 反方向 */
	animation-direction: reverse;

	/* 先正常方向再反方向运行，并持续交替 */
	animation-direction: alternate;

	/* 先反方向再正常方向运行，并持续交替 */
	animation-direction: alternate-reverse;
}
```

### 08 动画以外的状态

```css
div {
	/* 动画结束时的状态 */
	animation-fill-mode: forwards;

	/* 动画开始时的状态 */
	animation-fill-mode: backwards;
}
```

### 09 动画播放状态

```css
div {
	/* 暂停 */
	animation-play-state: pause;

	/* 播放 */
	animation-play-state: running;
}
```

### 10 动画复合属性

```css
div {
	/**/
	animation: name duration delay func count direct mode state;
}
```

## 11. 列布局

### 01 指定列数

```css
div {
	/*直接指定列数 */
	column-count: 5;

	/* 指定每一列的宽度，会自动计算列数 */
	column-width:220px ;

	/* 复合属性，能同时指定列宽和列数(不推荐使用) */
	columns: 4;
}
```

### 02 调整列间距

```css
div {
	/* 调整列间距 */
	column-gap: 20px;
}
```

### 03 调整列边框

```css
div {
	column-rule-width: 2px;
	column-rule-style: dashed;
	column-rule-color: red;
	
	column-rule: 2px dashed red;
}
```

### 04 跨列

```css
h1 {
	column-span: none;

	/* 跨所有列 */
	column-span: all;
}
```

### 05 多列图片

```css
div {
	column-count: 5;
}

img {
	width: 100%;
}
```

# 十四、伸缩盒模型

## 1. 伸缩盒模型简介

- 2009年,W3C 提出了一种新的盒子模型 -- Flexible Box
- 它可以轻松的控制:元素分布方式、元素对齐方式、元素视觉顺序
- 伸缩盒模型的出现,逐渐演变出了一套新的布局方案 -- **flex布局**。

## 2. 伸缩容器 & 伸缩项目

### 01 伸缩容器

开启**flex**的元素，就是伸缩容器

1. 给元素设置：display:flex 或 display:inline-flex，该元素就变为了伸缩容器。
2. display:inline-flex很少使用，因为可以给多个伸缩容器的父容器，也设置为伸缩容器。
3. 一个元素可以同时是：伸缩容器、伸缩项目。
```css
/* 将div变为伸缩容器 */
.father{
	display: flex;
}
```

### 02 伸缩项目

伸缩容器所有子元素自动成为了伸缩项目。

1. 仅伸缩容器的子元素成为了伸缩项目,孙子元素、重孙子元素等后代,不是伸缩项目。
2. **无论原来是哪种元素(块、行内块、行内),一旦成为了伸缩项目,全都会“块状化”。**

伸缩项目沿着主轴排列，主轴默认是水平的，默认方向是与主轴垂直的就是侧轴。

## 3. 主轴

伸缩项目沿着主轴排列，主轴默认是水平的，默认方向是：从左到右（左边是起点，右边是终点）

### 01 主轴方向

属性名: flex-direction
常用值如下
1. row : 主轴方向水平从左到右 -- 默认值:
2. row-reverse：主轴方向水平从右到左
3. column：主轴方向垂直从上到下
4. column-reverse：主轴方向垂直从下到上

### 02 主轴换行

属性名: flex-wrap
常用值：
1. nowrap：不换行--默认值
   ![[Pasted image 20231126154900.png|400]]
2. wrap：自动换行
   ![[Pasted image 20231126154839.png|400]]
3. wrap-reverse：反向换行
   ![[Pasted image 20231126155305.png|400]]

### 03 主轴对齐

属性名：justify-content

**主轴的起始位置**
justify-content: flex-start;
![[Pasted image 20231126155522.png|400]]

**主轴的结束位置**
justify-content: flex-end;
![[Pasted image 20231126155610.png|400]]

**主轴的中间位置**
justify-content: center;
![[Pasted image 20231126155740.png|400]]

**伸缩项目之间的距离是相等的，且是项目距边缘的二倍**
justify-content: space-around; 
![[Pasted image 20231126160019.png|400]]

**伸缩项目之间的距离是相等的，且项目距边缘没有距离**
justify-content: space-between;
![[Pasted image 20231126155921.png|400]]

**伸缩项目之间的距离是相等的，且等于项目距边缘距离**
justify-content: space-evenly;
![[Pasted image 20231126160057.png|400]]

## 4. 侧轴

与主轴垂直的就是侧轴，侧轴默认是垂直的，默认方向是：从上到下（上边是起点，下边是终点）

### 01 侧轴方向

侧轴方向跟主轴相关，时刻与主轴垂直

### 02 侧轴单行对齐

属性值：align-item

**侧轴的起始位置**
align-item: flex-start;
![[Pasted image 20231126160708.png|400]]

**侧轴的结束位置**
align-item: flex-end;
![[Pasted image 20231126160732.png|400]]

**侧轴的中间位置**
align-item: center;
![[Pasted image 20231126160800.png|400]]

**项目均匀的分布在一行中**
align-item: baseline; 


**当[[CSS#02 伸缩项目|伸缩项目]]没有高度时，伸缩项目高度就是[[CSS#01 伸缩容器|伸缩容器]]高度，这是默认值**
align-item: stretch;
![[Pasted image 20231126161255.png|400]]
**当[[CSS#02 伸缩项目|伸缩项目]]有高度时**
align-item: stretch;
![[Pasted image 20231126160708.png|400]]

### 03 侧轴多行对齐

属性名：align-content
![[Pasted image 20231126163116.png|400]]

**侧轴的起始位置**
align-content: flex-start;
![[Pasted image 20231126161935.png|400]]

**侧轴的结束位置**
align-content: flex-end;
![[Pasted image 20231126162027.png|400]]

**侧轴的中间位置**
align-content: center;
![[Pasted image 20231126162105.png|400]]

**伸缩项目之间的距离是相等的，且是项目距边缘的二倍**
align-content: space-around; 
![[Pasted image 20231126162304.png|400]]

**伸缩项目之间的距离是相等的，且项目距边缘没有距离**
align-content: space-between;
![[Pasted image 20231126162731.png|400]]

**伸缩项目之间的距离是相等的，且等于项目距边缘的距离**
align-content: space-evenly;
![[Pasted image 20231126162357.png|400]]

**当[[CSS#02 伸缩项目|伸缩项目]]没有高度时，伸缩项目高度就是[[CSS#01 伸缩容器|伸缩容器]]高度，这是默认值**
align-content: stretch;
![[Pasted image 20231126163603.png|400]]

**当[[CSS#02 伸缩项目|伸缩项目]]有高度时**
align-content: stretch;
![[Pasted image 20231126163116.png|400]]

## 5. 伸缩盒模型居中

### 01 主侧轴对齐

```html
<style>
.father{
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>

<div class="father">
	<div class="son"></div>
</div>
```

### 02 边距

```html
<style>
.father{
	display: flex;
}
.son{
	margin: auto;
}
</style>

<div class="father">
	<div class="son"></div>
</div>
```

## 6. 主轴基准长度

### 01 flex-basis

flex-basis 设置的是伸缩项目在主轴方向的基准长度，若主轴是横向的，则宽度失效；若主轴是纵向的，则高度失效。

### 02 作用
浏览器根据这个属性设置的值，计算主轴上是否有多余空间，默认值 auto，即：伸缩项目的宽或高

## 7. 伸缩性

### 01 flex-grow (伸)

flex-grow 定义伸缩项目的放大比例，默认为0，即: 纵使主轴存在剩余空间，也不拉伸(放大)

拉伸项目的计算举例：
1. 若所有伸缩项目的 flex-grow 值都为 1，则: 它们将等分剩余空(如果有空间的话)
2. 若三个伸缩项目的 flex-grow 值分别为: 1、2、3，则: 分别瓜分到: 1/6 、2/6 、3/6 的空间。

### 02 flex-shrink (缩)

 flex-shrink 定义了项目的压缩比例，默认为 1，即: 如果空间不足，该项目将会缩小。
 
 收缩项目的计算举例:

三个收缩项目，
宽度分别为: 200px 、300px 、200px，
它们的 flex-shrink 值分别为:1、2、3，
若想刚好容纳下三个项目，需要总宽度为 700px，
但目前容器只有 400px ，还差 300px ，
所以每个人都要收缩一下才可以放下，具体收缩的值，这样计算:
1. 计算分母: (200x1) + (300x2) + (200x3) = 1400
2. 计算比例:
3. 
项目一:(200x1) / 1400 = 比例值1
项目二: (300x2) / 1400 = 比例值2
项目三: (200x3) / 1400 = 比例值3

项目一需要收缩：比例值1 x 300
项目二需要收缩：比例值2 x 300
项目三需要收缩：比例值3 x 300

## 8. 复合属性

flex 是复合属性，复合了：[[CSS#01 flex-grow (伸)|flex-grow]]、[[CSS#02 flex-shrink (缩)|flex-shrink]]、[[CSS#01 flex-basis|flex-basis]] 三个属性，默认值为 0 1 auto。

flex:1 1 auto ，可简写为: flex :auto
flex:1 1 0 ，可简写为: flex:1
flex: 0 0 auto ，可简写为: flex:none
flex: 0 1 auto ，可简写为: flex: 0 auto -- 即 flex 初始值

## 9. 项目排序 & 单独对齐

### 01 项目排序

order属性定义项目的排列顺序。数值越小，排列越靠前，默认为 0。

### 02 单独对齐

align-self 属性，可以单独调整某个伸缩项目的侧轴对齐方式，默认值为 auto，表示继承父元素的 align-items 属性。

# 十五、响应式布局

## 1. [grid布局](https://blog.csdn.net/weixin_41192489/article/details/115588135)

容器：采用网格布局的区域
项目：容器内采用网格定位的子元素（不包含项目的子元素）

### 01 启用网格布局

块级容器（宽度撑满整行）时
```css
display: grid;
```

行内容器（宽度随内容自适应）时
```css
display: inline-grid;
```

使用网格布局后，项目的float、display: inline-block、display: table-cell、vertical-align和column-\*等设置都将失效。

### 02 划分列

grid-template-columns

**绝对值 px**
在容器内划分出3列，每列宽度为100px
```css
grid-template-columns: 100px 100px 100px;
```

**百分比值 %**
将容器等分为3列，每列宽度为容器总宽度/3
```css
grid-template-columns: 33.33% 33.33% 33.33%;
```

**比例值 fr**
将容器划分为2列，第1列的宽度 ：第2列的宽度 = 1：2
```css
grid-template-columns: 1fr 2fr;
```


**minmax() 函数值**
minmax() 函数产生一个长度范围，表示长度就在这个范围之中。它接受两个参数，分别是最小值和最大值
```css
grid-template-columns: 1fr 1fr minmax(100px, 1fr);
```

**repeat() 函数值**
repeat() 接受两个参数，第一个参数是重复的次数，第二个参数是要重复的值
```css
grid-template-columns: repeat(3, 1fr);
grid-template-columns: repeat(3, 1fr 2fr 3fr);
```
无法确定列数、重复次数时，使用关键字auto-fill 或 auro-fit

**fit-content() 函数**
让尺寸适应内容，但不超过设定的尺寸
```css
grid-template-columns: fit-content(100px) fit-content(100px) 40px auto;
```
fit-content()函数只支持数值和百分比值，fr值是不合法的

**min-content**

**max-content**

**auto**

### 02 划分行

grid-template-rows

使用方法与列相同

### 03 给网格线命名

\[]

```css
grid-template-columns: [c1] 100px [c2] 100px [c3];
grid-template-rows: [r1] 100px [r2] 100px [r3];
```

### 04 行/列的间距

**设置行间距**
row-gap
```css
row-gap: 20px;
```
支持数值和百分比值

**设置列间距**
column-gap
```css
column-gap: 30px;
```
支持数值和百分比值

**gap**
是column-gap和row-gap合并的简写形式
```css
gap: 20px 30px;
```
支持数值和百分比值和calc()函数

### 05 指定项目位置

grid-column-start属性：左边框所在的垂直网格线
grid-column-end属性：右边框所在的垂直网格线
grid-row-start属性：上边框所在的水平网格线
grid-row-end属性：下边框所在的水平网格线

```css
grid-column-start: 1;
grid-column-end: 3;
grid-row-start: 1;
grid-row-end: 3;

/*等同于*/
grid-column: 1 / 3;
grid-row: 1 / 3;

/*等同于*/
grid-column: 1 / span 2;
grid-row: 1 / span 2;
```
