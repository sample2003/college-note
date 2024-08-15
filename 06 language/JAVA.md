# 一、JAVA概述

## 1. java发展历程

### jdk7 的特性

二进制：由0和1组成，代码中以0b开头；
十进制：由0~9组成，前面不加任何前缀；
八进制：由0~7组成，代码中以0开头；
十六进制：由0~9还有a~f组成，代码中以0x开头；

```java
public class HelloWorld{
	public static void main(String[] args){
		System.out.println(17); // 十进制
		System.out.println(017); // 八进制
		System.out.println(0b11); // 二进制
		System.out.println(0x17); // 十六进制
	} 
}
```

## 2. java三个版本

### 01 Java SE

全称Java Standard Edition，Java 标准版，是Java技术的核心和基础，是Java ME和Java EE编程的基础。Java SE是由Sun Microsystems公司于1995年5月推出的Java[程序设计语言](https://baike.baidu.com/item/%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E8%AF%AD%E8%A8%80?fromModule=lemma_inlink)和[Java平台](https://baike.baidu.com/item/Java%E5%B9%B3%E5%8F%B0?fromModule=lemma_inlink)的总称。

### 02 Java ME

称为J2ME（Java Platform，Micro Edition），是为机顶盒、移动电话和PDA之类嵌入式消费[电子设备](https://baike.baidu.com/item/%E7%94%B5%E5%AD%90%E8%AE%BE%E5%A4%87/4393826?fromModule=lemma_inlink)提供的Java语言平台，包括[虚拟机](https://baike.baidu.com/item/%E8%99%9A%E6%8B%9F%E6%9C%BA/104440?fromModule=lemma_inlink)和一系列标准化的Java API。

### 03 Java EE

## 3. java特点

### 01 [[JAVA#九、面向对象|面向对象]]

### 02 健壮性

### 03 跨平台

平台指各类操作系统，如windows、macos、linux等，java编译之后生成文件，可借由jvm在各类操作系统运行

### 04 解释型语言

## 4. jdk

jdk全称java development kit，翻译过来是java开发工具包，包含jvm，核心类库，开发工具

### 01 jvm

jvm全称java virtual machine，翻译过来是java虚拟机

### 02 核心类库

### 03 开发工具

### 04 安装与配置

[jdk17](https://www.oracle.com/java/technologies/downloads/#jdk17-windows)

## 5. jre

jre全称Java runtime environment，翻译过来是java运行环境，包含jvm，核心类库，部分开发工具

# 二、变量

## 1. 字面量 & 常量

字面量就是一个值，比如变量的值或者常量的值（字母、字符串、数字等等）

![[Pasted image 20231004111926.png]]

**常量与变量的区别:**  
常量与变量的储存方式是一样的,只不过常量必须要有初始值,而且值不允许修改,而变量可以无初始值,且可以多次赋值  

**常量与字面量的区别:**  
常量与字面量均不会改变,常量为储存数据的容器,字面量为等号右侧的值,字面量是由字符串、数字等构成的字符串或数值

**常量命名规范：**
单个单词：全部大写
多个单词：全部大写，单词之间用下划线隔开

## 2. 变量

变量是程序的基本组成单位，在程序执行过程中，其值有可能发生改变的数据

## 3. 变量的定义格式

数据类型 变量名 = 数据值

## 4. 标识符命名规则

### 01 硬性要求

### 02 小驼峰命名法（方法、变量）

1. 标识符是一个单词时，全部小写，如 name
2. 标识符由多个单词组成时，第一个单词小写，其他单词首字母大写，如 firstName

### 03 大驼峰命名法（类名）

1. 标识符是一个单词时，首字母大写，如 Student
2. 标识符由多个单词组成时，每个单词首字母大写，如 GoodStudent

## 5. 键盘输入

java自带一个类叫Scanner，这个类可以接受键盘输入的信息。

### 01 第一类

1. nextInt(); nextDouble(); next();
2. 遇到空格，制表符，回车就停止接收，这些符号后面的数据就不会接收了，并把这些数据给下一个键盘录入。

```java
public static void main(String[] args){ 
    Scanner sc = new Scanner(System.in);
    // 接受整数  
    System.out.println("请输入一个整数");  
    int num1 = sc.nextInt();  

	// 接收小数
    System.out.println("请输入一个小数");  
    double num2 = sc.nextDouble(); 

	// 接收字符串
	System.out.println("请输入一个单词");
	String c = sc.next();
}
```

### 02 第二类

1. nextLine();
2. 可以接收空格，制表符，遇到回车才停止接收数据

```java
public static void main(String[] args){ 
    Scanner sc = new Scanner(System.in);
	// 接收字符串
	System.out.println("请输入一行字");
	String c = sc.nextLine();
}
```

### 03 注意事项

1. 键盘录入的两类体系不能混用的；
2. 弊端：先用nextInt，再用nextLine会导致下面的nextLine接收不到数据。

## 6. 使用变量

### 01 输出打印

```java
int a = 50;
System.out.println(a); // 50
```

### 02 参与计算

```java
int a = 50;
int b = 10
System.out.println(a + b); //60
```

### 03 修改变量的值

```java
int a = 50;
System.out.println(a); // 50
a = 10;
System.out.println(a); // 10
```

## 7. 注意事项

1. 只能存一个值
   ```java
   int a = 10;
   // a 的值被覆写了。
   a = 50;
   ```
2. 变量名不允许重复定义
    ```java
   int a = 10;
   // 会报错，系统不知道该用哪个值。
   int a = 50;
   ```
3. 一条语句可以定义多个变量
    ```java
   int a = 10, b = 20, c = 30;
   ```
4. 变量在使用前一定要赋值
    ```java
   int a;
   a = 50;
   System.out.println(a); // 50
   ```

## 8. 成员变量 & 局部变量

|区别|成员变量|局部变量|
|:-:|:-:|:-:|
|类中位置不同|类中，方法外|方法内、方法声明上|
|初始化值不同|有默认初始值|没有默认初始值，使用之前需要赋值|
|内存位置不同|堆内存|栈内存|
|生命周期不同|随着对象的创建而存在，随着对象的消失而消失|随着方法的创建而存在，随着方法的消失而消失|
|作用域|整个类中有效|当前方法中有效|


```java
public class ThisKey {
	// 成员变量
	private int age;
	public void method(){
		// 局部变量
		int age = 10;
		// 离输出语句最近的是局部变量，所以打印的值是10
		System.out.println(age);  // 10
	}
}
```

# 三、数据类型

java语言的数据类型分为：基本数据类型，引用数据类型。

## 1. 基本数据类型

1. 变量中存储的都是真实数据，数据值是存储在自己的（栈）空间中；
2. 赋值给其他变量，也是赋的真实的值。

![[屏幕截图 2023-10-03 102516.png]]

```java
public static void main(String[] args){  
    // byte  
    byte b = 10;  
    System.out.println(b); // 10  
    // short    short s = 20;  
    System.out.println(s); // 20  
    // int    int i = 30;  
    System.out.println(i); // 30  
    // long    // 注意：要在数据值后加一个L作为后缀  
    long l = 9999999999L;  
    System.out.println(l); // 9999999999  
  
    // float    // 注意：要在数据值后加一个F作为后缀  
    float f = 10.1F;  
    System.out.println(f); // 10.1  
    // double    double d = 20.2;  
    System.out.println(d); // 20.2  
  
    // char    char c = '中';  
    System.out.println(c); // 中  
  
    // boolean  
    boolean o = true;  
    System.out.println(o); // true  
}
```

## 2. 引用数据类型

1. 变量中存储的是地址值，引用：使用了其他空间中（堆）自己的数据值；
2. 赋值给其他变量，赋的是地址值。

```java
public static void main(String[] args){  
    Student s1 = new Student();

	s1.name = "张三";

	Student s2 = s1;

	s2.name = "李四";
	sout(s1.name +"..."+ s2.name); // 李四...李四
	
}
```

## 3. 类型转换

[[JAVA#^2f4d20|取值范围]]

![[Pasted image 20231003151645.png]]

### 01 隐式转换（自动类型提升）

1. 把一个取值范围小的数值，转成取值范围大的数据，然后再进行运算；
2. byte、short、char 三种类型的数据在运算时，都会先转换为 int 类型，然后再进行运算。

```java
public static void main(String[] args){
	byte a = 10; // 0000 1010
	int b = a;   // 0000 0000 0000 0000 0000 0000 0000 1010
	System.out.println(b);
}
```

### 02 强制转换

1. 如果把一个取值范围大的数值，赋值给取值范围小的数据，需要加入强制转换，然后再进行运算；
2. 格式：目标数据类型 变量名 = (目标数据类型)被强转的数据

```java
public static void main(String[] args){
	int a = 300;      // 0000 0000 0000 0000 0000 0001 0010 1100
	byte b = (byte)a; // 0010 1100
	System.out.println(b); // 44

	int c = 200;      // 0000 0000 0000 0000 0000 0000 1100 1000
	byte d = (byte)c; // 1100 1000
	System.out.println(d); // -56

	byte x = 10;
	byte y = 20;
	byte z = (byte)(x + y); 
	System.out.println(z);
}
```

### 03 字符串的”+“操作

1. 当”+“操作中出现字符串时，这个”＋“是字符串连接符，而不是算术运算符了，会将前后的数据进行拼接，并产生一个新的字符串；
```java
System.out.println("123" + 123); // 123123
```
2. 连续进行”+“操作时，从左到右逐个执行。
```java
System.out.println(1 + 99 + "是个整数"); // 100是个整数
```
3. 当 字符 + 字符 或 字符 + 数字时，会把字符通过ASCII码表查询到对应的数字再进行计算。


## 4. 注意事项

1. byte的取值范围
   -128 ~ 127
2. 整数和小数的 取值范围 大小关系：
   double > float > long > int > short > byte ^2f4d20
3. long类型变量：需要在数据值后加L；float类型变量：需要在数据值后加F。

# 四、运算符与表达式

## 运算符

对字面量或者变量进行操作的符号，如 + - × ÷。

## 1. 算术运算符

若有小数参与计算，则结果不一定精确

1. <kbd>+</kbd> ：加
2. <kbd>-</kbd> ：减
3. <kbd>*</kbd> ：乘
4. <kbd>/</kbd> ： 除
5. <kbd>%</kbd> ： 取余

## 2. 自增自减运算符

### 01 自增 ++

```java
int a = 1;
a++; // 相当于 a = a + 1;
```

### 02 自减 --

```java
int a = 2;
a--; // 相当于 a = a - 1;
```

### 03 注意事项

![[Pasted image 20231003160822.png]]

```java
public static void main(String[] args){  
    int x = 10;  
    int y = x++;  
    int z = ++x;  
    System.out.println("x：" + x); //12  
    System.out.println("y：" + y); //10  
    System.out.println("z：" + z); //12  
}
```

## 3. 赋值运算符

![[Pasted image 20231003161358.png]]

## 4. 比较运算符（关系运算符）

![[Pasted image 20231003161425.png]]

比较运算符的结果都是boolean类型，要么是true，要么是false。

## 5. 逻辑运算符

![[Pasted image 20231003162307.png]]
![[屏幕截图 2023-10-03 162753.png]]

1. && 第一次判断为假，第二次不再判断；
2. || 第一次判断为真，第二次不再判断。

## 6. 三元运算符（三元表达式）

### 01 格式

关系表达式?表达式1:表达式2;

### 02 计算规则

1. 首先计算关系表达式的值；
2. 如果值为true，表达式1的值就是运算结果；
3. 如果值为false，表达式2的值就是运算结果。

```java
public static void main(String[] args){ 
	// 比较a，b, c的值并打印最大值
	int a = 10;
	int b = 20;
	int c = 30;
	
	int d = a > b? a : b;
	int e = d > c? d : c;
	
	System.out.println(e);
}
```

## 7. 运算符优先级

![[Pasted image 20231003164823.png]]

## 8. 原码、反码、补码

### 01 原码

1. 十进制数据的二进制表现形式，最左边是符号位，0为正，1为负；
2. 如 0000 0111，1000 0111；
3. 利用原码对正数计算不会出现问题；
4. 弊端：计算负数会出现与预期相反的情况。

### 02 反码

1. 正数的原码不变，也为反码；
2. 负数的原码符号位不变，数值取反，0变1，1变0；
3. 弊端：0在补码里有两种形式，0000 0000 与 1111 1111，如果结果不跨0，没有问题，若结果跨0，跟实际结果会有1的偏差。

### 03 补码

1. 正数的反码不变，也为补码；
2. 负数在反码的基础上+1；
3. 补码能多记录一个特殊值-128，该数据在一个字节下，没有原码和反码；
4. 计算机中的存储和计算都是以补码的形式进行的。

# 五、流程控制

## 1. 顺序结构

按照代码的先后顺序，从上至下执行

## 2. if-分支结构

### 01 if语句第一种格式

单条件判断

```java
public static void main(String[] args){
	if (关系表达式) {
		语句体;
	}
	// 另一种写法
	if (关系表达式)
		只有一个语句;
		// int a = 10; // 1.定义变量a 2.赋值a为10
}
```

执行流程

1. 首先计算并判断关系表达式的值；
2. 如果关系表达式的值为true就执行语句体；
3. 如果关系表达式的值为false就不执行语句体；
4. 继续执行后面的其他语句。

### 02 if语句第二种格式

双条件判断

```java
public static void main(String[] args){
	if (关系表达式) {
		语句体1;
	} else {
		语句体2;
	}
}
```

执行流程

1. 首先计算并判断关系表达式的值；
2. 如果关系表达式的值为true就执行语句体1；
3. 如果关系表达式的值为false就执行语句体2；
4. 继续执行后面的其他语句。

### 03 if语句第三种格式

多条件判断

```java
public static void main(String[] args){
	if (关系表达式1) {
		语句体1;
	} else if (关系表达式2){
		语句体2;
	} else if (关系表达式3){
		语句体3;
	}
	  ......
	} else {
		语句体n;
	}
	
}
```

执行流程

1. 首先计算并判断关系表达式1的值；
2. 如果为true就执行语句体1并跳出 if 判断；如果为false就计算并判断语句体2；
3. 如果为true就执行语句体2并跳出 if 判断；如果为false就计算并判断语句体3；
4. ...
5. 如果所有的关系表达式结果都为false，就执行语句体n；
6. 继续执行后面的其他语句。

## 3. switch-分支结构

### 01 switch语句格式

```java
public static void main(String[] args){
	switch (表达式) {
		case 值1 :
			语句体1;
			break;
		case 值2 :
			语句体2;
			break;
		......
		default:
			语句体n;
			break;	
	}
}
```

### 02 格式说明

1. 表达式：（将要匹配的值）取值为byte、short、int、char。JDK5以后可以是枚举，JDK7以后可以是String；
2. case：后面跟的是要和表达式进行比较的值（被匹配的值）；
3. case后面的值只能是[[JAVA#000 字面量|字面量]]，不能是变量；
4. case给出的值不允许重复；
5. break：表示中断，结束的意思，用来结束switch语句。
6. default：表示所有情况都不匹配时，就执行该处的内容。

### 03 执行流程

1. 首先计算表达式的值；
2. 依次和case后面的值进行比较，如果有对应的值，就会执行相应的语句，在执行的过程中，遇到break就会结束；
3. 如果所有的case后面的值和表达式的值都不匹配，就会执行defult'里面的语句体，然后结束整个switch语句。

### 04 注意事项

1. default的位置不一定是最下面的，可以写在任意位置；
2. default可以省略，语法不会报错；
3. case穿透：语句体中没有写break导致的，所以所有的case都会进行解析；如果匹配上了，就会执行对应的语句体，若在该语句体有break，那么结束整个switch语句；若没发现break，则程序继续执行下一个case的语句体，就算没有匹配上，一直遇到break或者大括号。
	```java
public static void main(String[] args){
	Scanner sc = new Scanner(System.in);
	System.out.println("请输入一个整数表示星期几");
	int week = sc.nextInt();
	
	switch (week){
		case 1,2,3,4,5: 
			System.out.println("工作日");
			break;
		case 6,7: 
			System.out.println("休息日");
			break;
		default : 
			System.out.println("错误");
			break;
	}
}
```
4. JDK12的新特性
```java
public static void main(String[] args){
	int num = 1;
	switch(num){
		case 1 -> {
			System.out.println("一");
		}
		case 2 -> {
			System.out.println("二");
		}
		
		/* 简写
		case 1 -> System.out.println("一");
		case 2 -> System.out.println("二");
		*/
		
		default -> System.out.println("无");
	}
}
```

## 4. for-循环结构

### 01 for语句格式

```java
public static void main(String[] args){
	for (初始化语句; 条件判断语句; 条件控制语句){
		循环体语句;
	}
}
```

### 02 格式说明

1. 初始化语句只会执行一次；

### 03 执行流程

1. 执行初始化语句；
2. 执行条件判断语句，若结果为false，循环结束；若结果为true，执行循环体语句；
3. 执行条件控制语句；
4. 回到 2. 继续执行条件判断语句。


## 5. while-分支结构

### 01 while语句格式

```java
初始化语句
while(条件判断语句){
	循环体语句;
	条件控制语句;
}
```

### 02 格式说明

1. 初始化语句只会执行一次；

### 03 执行流程

1. 执行初始化语句；
2. 执行条件判断语句，若结果为false，循环结束；若结果为true，执行循环体语句；
3. 执行条件控制语句；
4. 回到 2. 继续执行条件判断语句。

### 04 for 与 while 的区别

1. for循环中：知道循环次数或者循环的范围；
2. while循环中：不知道循环的次数和范围，只知道循环的结束条件。

```java
public static void main(String[] args){
	/* 需求：给你一个整数x，如果x是一个回文整数，打印true；
	 * 解释：回文数是指正序和倒序都是一样的整数，如，121，12321。
	*/
	int x = 12321;
	int temp = x;
	int num = 0;
	
	while (x != 0){
		int ge = x % 10;
		x = x / 10;
		num = num * 10 + ge;
	}
	if (temp == num){
		System.out.println(true);
	}else {
		System.out.println(false);
	}
}
```

## 6. do...while

### 01 语句格式

```java
public static void main(String[] args){
	初始化语句;
	do{
		循环体语句;
		条件控制语句;
	}while (条件判断语句);
}
```

### 02 执行流程

1. 执行初始化语句；
2. 执行一次循环体语句；
3. 执行一次条件控制语句；
4. 执行条件判断语句，若结果为false，循环结束；若结果为true，执行循环体语句和条件控制语句；
5. 回到 2. 继续执行条件判断语句。

## 7. 无限循环

无限循环之下写代码是没有意义的，因为循环不会停止。

```java
public static void mian(String[] args){
	// 无限for循环
	for(;;){
		System.out.println("hello");
	}

	while(true){
		System.out.println("hello");
	}

	do{
		System.out.println("hello");
	}while(true);
}
```

## 8. 跳转控制语句

### 01 跳过本次循环

```java
public static void main(String[] args){
	if(i == 3){
		// 跳过本次循环，不再执行下列代码。
		continue;
	}
	System.out.println("hello");
}
```

### 02 结束整个循环

```java
public static void main(String[] args){
	if(i == 3){
		// 结束整个循环。
		break;
	}
	System.out.println("hello");
}
```

## 9. 循环嵌套的break选择

1. 给循环起名字
2. 指定循环break

```java
public static void main(String[] args) {  
    ArrayList<Students> list = new ArrayList<>();  
    Scanner sc = new Scanner(System.in);  
  
    loop: while(true){  
        System.out.println("---------欢迎来到学生管理系统---------");  
        System.out.println("1：添加学生");  
        System.out.println("2：删除学生");  
        System.out.println("3：修改学生");  
        System.out.println("4：查询学生");  
        System.out.println("5：退出");  
        System.out.println("请输入序号以选择");  
        int num = sc.nextInt();  
  
        switch (num){  
            case 1 -> {  
                addStu(list);  
            }  
            case 2 -> {  
                delStu(list);  
            }  
            /*case 3 -> {  
                chaStu(list);            }*/            case 4 -> {  
                selStu(list);  
            }  
            case 5 -> {  
                break loop;  
            }  
            default -> {  
                System.out.println("序号无效");  
            }  
        }  
    }  

}
```

# 六、数组

## 1. 数组是什么

数组指的是一种容器，可以用来存储同种[[#三、数据类型|数据类型]]的多个值。

数组容器在存储数据的时候，需要结合[[JAVA#01 隐式转换（自动类型提升）|隐式转换]]考虑。

## 2. 数组生成和初始化

初始化：就是在内存中，为数组容器开辟空间，并将数据存入容器中的过程。

### 01 数组生成

```java
public static void main(String[] args){
	// 格式一：数据类型[] 数组名
	int[] array;

	// 格式二：数据类型 数组名[]
	int array[]
}
```

### 02 静态初始化

初始化时指定数组元素，系统会根据元素个数，计算出数组的长度。

```java
public static void main(String[] args){
	// 完整格式：数据类型[] 数组名 = new 数据类型[] {元素1, 元素2, ...};
	int[] array = new int[]{1, 2, ...};

	// 简写格式：数据类型[] 数组名 = {元素1, 元素2, ...}
	int[] array = {1, 2, ...}
}
```

### 03 动态初始化

初始化时只指定数组长度，由系统为数组分配默认初始值。

数组默认初始值的规律：
1. 整数类型：默认初始值 0；
2. 小数类型：默认初始化值 0.0；
3. 字符类型：默认初始值 '\u0000' 空格；
4. 布尔类型：默认初始值 false；
5. 引用数据类型：默认初始化值 null。

```java
public static void main(String[] args){
	// 格式：
	数据类型[] 数组名 = new 数据类型[数组长度];

	// 例：
	int[] array = new int[5];
	
	System.out.println(array[1]); // 0
}
```

## 3. 数组的地址值

```java
public static void main(String[] args){  
    // int  
    int[] arr1 = new int[]{1, 2, 3};  
    int[] arr2 = {1, 2, 3};  
    System.out.println(arr1); // [I@776ec8df
}
```

1. <kbd>[</kbd>：表示当前是一个数组；
2. <kbd>I</kbd>：表示当前数组里的元素都是Int类型的；
3. <kbd>@</kbd>：表示一个间隔符号，固定格式；
4. 776ec8df：数组真正的地址值，（十六进制）

## 4. 数组元素访问

### 01 格式

```java
public static void main(String[] args){
	// 格式
    数组名[索引];
    // 例：
    System.out.println(arr[1]);
}
```

### 02 索引

也叫角标，下标，从0开始，逐渐加一，连续不间断。

### 03 获取数组元素

```java
public static void main(String[] args){  
    // int  
    int[] arr1 = new int[]{1, 2, 3}; 
    int num = arr1[0];
    System.out.println(num); // 1
}
```

### 04 添加数据至数组

原来的数据会被覆盖。

```java
public static void main(String[] args){  
    // int  
    int[] arr1 = {1, 2, 3};  
    arr[0] = 100;
    System.out.println(arr[0]); // 100
}
```

### 05 数组遍历

```java
public static void main(String[] args){  
    // int   
    int[] arr = {1, 2, 3, 4, 5}; 
    System.out.println(arr.length); // 5
    
    // idea快捷键 arr.fori
    for(int i = 0; i < arr.length; i++){
	    System.out.println(arr[i]);
    } 
}
```

### 06 数组越界

当访问了数组中不存在的索引，会引发数组索引越界异常。

```java
public static void main(String[] args){
    int[] arr = {1, 2, 3, 4, 5}; 
    System.out.println(arr[10]); // error
}
```

## 5. 二维数组

### 01 静态初始化

```java
public static void main(String[] args){
	// 格式
	数据类型[][] 数组名 = new 数据类型[][] {{元素1, 元素2,},{元素1, 元素2}};
	// 简写
	数据类型[][] 数组名 = {{元素1, 元素2,},{元素1, 元素2}};
	
	// 例：
	int[][] arr = new int[][]{{1,2},{3,4}};
	int[][] arr = {{1,2},{3,4}};
	int arr[][] = {{1,2},{3,4}};

	int[][] arr = {  
        {1, 2},  
        {3, 4}  
	};  
	System.out.println(arr[1][1]); // 4
}
```

### 02 动态初始化

```java
public static void main(String[] args){
	// 格式
	数据类型[][] 数组名 = new 数据类型[二维数组长度][一维数组长度];
	
	// 例：
	int[][] arr = new int[1][2];
	int[][] arr = new int[2][];
	int[] arr1 = {1, 2, 3, 4}

	// 给二维数组赋值一个元素
	int[][] arr = {  
        {1, 2},  
        {3, 4}  
	};  
	System.out.println(arr[1][1]); // 4
}
```

### 03 二维数组遍历

```java
public static void main(String[] args){  
    int[][] arr = new int[][]{{1,2},{3,4}};
    
	for (int i = 0; i < arr.length; i++) {  
	    // i：表示二维数组中的每一个索引  
	    for (int j = 0; j < arr.length; j++) {  
	        // j：表示一维数组中的每一个索引  
	        System.out.print(arr[i][j] + " ");  
		}  
		System.out.println();
	}
}
```

## 6. [[JAVA#数组|数组的内存]]

# 七、方法

## 1. 方法是什么

1. 方法的定义：方法（method）是程序中最小的执行单元；
2. 方法的作用：重复的代码、具有独立功能的代码可以抽取到方法中；
3. 方法的好处：可以提高代码的复用性、可维护性

## 2. 方法的定义和调用

### 01 简单方法

```java
public static void 方法名(){
	方法体(就是打包的代码);
}
// 例
// 调用
public static void main(String[] args){
	plan();
}
// 定义
public static void plan(){
	System.out.println("hello");
}
```

### 02 带参数的方法

```java
public static void 方法名(数据类型1 变量1, 数据变量2 变量2){
	方法体(就是打包的代码);
}
// 例
// 调用
public static void main(String[] args){
	getSum(10, 20); // 实参
	int a = 10;
	int b = 10;
	getSum(a, b);   // 实参
}
// 定义
public static void getSum(int num1, int num2){ // 形参
	int sum = num1 + num2;
	System.out.println(sum);
}
```

### 03 带返回值的方法

```java
public static 返回值类型 方法名(数据类型1 变量1, 数据变量2 变量2){
	方法体;
	return 返回值;
}
// 例
// 调用
public static void main(String[] args){
    int sum2 = getSum(1, 3);  
    System.out.println(sum2);
    return; // 结束方法
}
// 定义
public static int getSum(int num1, int num2){ // 形参  
    int sum1 = num1 + num2;  
    return sum1;
}
```

### 04 形参和实参

1. 形参全称形式参数，是指方法定义中的参数；
2. 实参全称实际参数，是指方法调用中的参数。

## 3. 方法重载

### 01 什么是方法重载

1. 重载是同一个类中，方法名相同，参数不同的方法，与方法返回值无关；
2. 在同一个类中，定义了多个 同名 的方法，这些同名的方法具有同种的功能；
3. 每个方法具有不同的参数类型或参数个数，这些同名的方法，就构成了重载关系；
4. 参数不同：个数不同、类型不同、顺序不同。

### 02 java如何分辨方法重载

java虚拟机通过**参数的不同**来区分同名的方法；

## 4. 方法重写

### 01 什么是方法重写

1. 重写发生在父类和子类之间，子类继承父类方法（非构造、private、final、static修饰的方法），并重写父类方法；

### 02 重写规则

1. 重写方法参数列表、名称必须和父类保持一致；
2. 重写方法的访问权限 **必须大于等于** 父类被重写的方法（空着不写 < protected < public )。
3. 重写方法的返回值类型 **必须小于等于** 父类被重写的方法。

### 03 重写注解 @Override

1. @Override是放在重写后的方法上，校验子类重写时语法是否正确；
2. 加上注解后如果有红色波浪线，则语法错误；

## 5. 方法的内存

### 01 方法调用的基本内存原理

当方法执行完毕后，会出栈；

![[Pasted image 20231010171534.png]]

多个方法遵循 “先进后出” 的原则。

![[Pasted image 20231010171719.png]]

### 02 方法传递基本数据类型的内存原理

传递基本数据类型是，传递的是真实的数据，形参的改变，不影响实参的值；

```java
public static void main(String[] args){  
    int number = 100;  
    System.out.println("调用change方法前："+number);  // 100
    change(number);  
    System.out.println("调用change方法后："+number);  // 100
}  
public static void change(int number){  
    number = 200;  
}
```

### 03 方法传递引用数据类型的内存原理

传递引用数据类型是，传递的是地址值，形参改变，影响实参的值；

```java
public static void main(String[] args){  
    int[] arr = {10, 20, 30}  
    System.out.println("调用change方法前："+arr[1]);  // 10
    change(arr);  
    System.out.println("调用change方法后："+arr[1]);  // 200
}  
public static void change(int[] arr){  
    arr[1] = 200;  
}
```

## 6. 方法注意事项

1. 方法不调用就不执行；
2. 方法与方法之间是平级关系，不能互相嵌套；
3. 方法的返回值类型为void，表示该方法没有返回值，没有返回值的方法可以省略return语句不写，如果要写return，后面不能跟具体的数据。
4. return语句下面，不能编写代码，因为永远执行不到，属于无效的代码。

## 7. [[JAVA#02 静态方法|静态方法]]

## 8. 抽象方法

将共性的行为（方法）抽取到父类之后，由于每一个子类执行的内容是不一样的，所以，**在父类中不能确定具体的方法体，该方法就可以定义为抽象方法。**

### 01 抽象方法的定义格式

`public abstract 返回值类型 方法名(参数列表);`

# 八、类

class

## 1. 类的定义

在java中，必须先设计定义类，才能获得对象

```java
public class 类名{
	1. 成员变量（代表属性，一般是名词）
	2. 成员方法（代表行为，一般是动词）
	3. 构造器
	4. 代码块
	5. 内部类
}
// 例
public class Phone{
	
}
```

## 2. 类的五大成员

属性、方法、[[JAVA#6. 构造方法|构造方法]]、[[JAVA#代码块|代码块]]、[[JAVA#内部类|内部类]]

## 3. 注意事项

1. 用来描述一类事物的类，叫做：Javabean类。在Javabean类中，是不写main方法的。
2. 之前编写main方法的类，叫做测试类
3. 一个Java文件可以定义多个class类，且只能一个类是 public 修饰，而且 public 修饰的类名必须是java代码文件名。实际开发中还是一个文件定义一个class类。
4. 成员变量的完整格式是：修饰符 数据类型 变量名称 = 初始值； 一般无需指定初始化值，存在默认值。 
   ```java
   public class Phone(){
		private int id;
   }
   ```
   ![[Pasted image 20231012092201.png]]

## Javabean类

用来描述一类事物的类

 1. 类名需要见名知意，如：Dog、Student、User；
 2. 成员变量使用private修饰；
 3. 至少提供无参和带全部参数的构造方法；
 4. 提供每一个成员变量对应的**set/get**方法；
 5. 如果还有其他行为，也需要写上。

## 测试类

用来检查其他类是否书写正确，带有main方法的类，是程序的入口

## 工具类

帮助做一些事情的，但是不描述任何事物的类，一般为静态类。

1. 类名见名知意；
2. 私有化构造方法，不让外界创建它的对象；
3. 方法定义为静态；

## 静态类

静态类指的是使用[[JAVA#static|static]]关键字修饰的类，其成员变量、方法都必须是静态的。静态类在Java中使用较少，通常用于存放工具类方法或静态变量。

### 01 静态类概述

静态类指的是使用static关键字修饰的类，其成员变量、方法都必须是静态的。静态类在Java中使用较少，通常用于存放工具类方法或静态变量。

### 02 静态类的定义

定义一个静态类，需要在类声明时添加static关键字。下面的代码演示了如何定义一个名为StaticClass的静态类，其中包含一个静态方法staticMethod用于打印传入的参数。

```java
public static class StaticClass {
    public static void staticMethod(String str) {
        System.out.println("Hello " + str);
    }
}
```

在上面的代码中，StaticClass和staticMethod的定义都使用了static关键字。这意味着我们可以直接通过类名调用方法，而不需要创建类的实例。例如：

`StaticClass.staticMethod("world");`

### 03 静态类的特点

静态类有以下一些特点：

**1. 静态类中的成员必须是静态的**

由于静态类没有实例对象，因此它的成员必须是静态的，以便直接通过类名访问。

**2. 静态类不能访问非静态的成员和方法**

由于静态类没有实例对象，无法访问非静态成员和非静态方法。但是非静态类可以访问静态成员和方法。

**3. 静态类不能继承非静态类**

由于静态类没有实例对象，因此无法继承非静态父类。

**4. 静态类只能继承静态类**

静态类只能继承另一个静态类，无法继承非静态类。

### 04 静态类的使用场景

静态类通常用于存放工具类方法或静态变量。例如常用的Math类、Arrays类的方法都是静态的。

下面是一个示例，展示了如何使用静态类来存放常量值：

```java
public static class ConstantClass {
    public static final double PI = 3.14159265358979323846;
    public static final int MAX_VALUE = 100;
}
```

在上面的代码中，我们定义了一个静态类ConstantClass，其中包含两个静态常量PI和MAX_VALUE。这些常量可以在应用程序中的任何地方直接使用，无需创建该类的实例。

### 05 静态类的注意事项

**1. 静态类不能被实例化**

静态类没有实例对象，因此无法通过构造函数来实例化。

**2. 静态类不能被传递为参数**

由于静态类不能被实例化，也无法被传递为参数。

**3. 静态类的成员访问控制**

静态类的成员可以被声明为public、protected、private，但是要注意这些访问控制修饰符对于静态类并不会有影响。因为静态类没有实例对象，所以它的成员无法被实例化后访问，只能通过类名来访问。

## 抽象类

如果一个类中存在抽象方法，那么该类就必须声明为抽象类。

### 01 抽象类的定义格式

`public abstract class 类名{};`

### 02 [[JAVA#8. 抽象方法|抽象方法]]

### 03 注意事项

- 抽象类不能实例化（创建对象）
- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类
- 可以有构造方法
- 抽象类的子类，要么重写抽象类中的所有抽象方法，要么是抽象类

## 内部类

### 什么是内部类

在一个类里再定义一个类，如果在A类的内部定义B类，B类就被称为内部类。

```java
public class Car {  
    String carName;  
    int carAge;  
  
    public void show(){  
	    Engine e = new Engine();
        System.out.println(e.engineName);  
    }  
	// 内部类
    class Engine{  
        String engineName = "v8";  
  
        public void show(){  
            System.out.println(carName);  
        }  
    }  
}
```

内部类的访问特点：
- 内部类可以直接访问外部类的成员，包括私有；
- 外部类要访问内部类的成员，必须创建对象。

### 01 成员内部类

**成员内部类的特点**
1. 写在成员位置的，就是类中方法外，属于外部类的成员；
```java
public class Outer {  
	// 成员内部类
    class Inner{  
    }  
}
```
2. 成员内部类可以被一些修饰符所修饰，如：private、默认、portected、public等；
```java
public class Outer {  
	// 成员内部类
    private class Inner{  
    }  
}
```
3. jdk16 开始，成员内部类里可以使用静态变量
```java
public class Outer {  
	// 成员内部类
    class Inner{  
	    static int a = 10;
    }  
}
```

**创建成员内部类的对象**
1. 在外部类中编写方法，对外提供内部类的对象
   ```java
    public class Outer {  
	    private class Inner{  
	    }  
	    public Inner getInstance(){  
	        return new Inner();  
	    }  
	}
	
	public static void main(String[] args) {  
	     Outer o = new Outer();  
	     Object inner1 = o.getInstance();
	}
   ```
2. 直接创建：外部类名.内部类名 对象名 = 外部类对象.内部类对象
   ```java
	public static void main(String[] args) {  
	     Outer.Inner inner = new Outer().new Inner();  
	}
   ```
   
**成员内部类如何获取外部类的成员变量**
`System.out.println(Outer.this.a);`
```java
public class Outer {  
    private int a = 10;  
    class Inner{  
        private int a = 20;  
        public void show(){  
            int a = 30;  
            System.out.println(a); // 30  
            System.out.println(this.a); // 20  
            System.out.println(Outer.this.a); // 10  
        }  
    }
}
```

### 02 静态内部类

成员内部类中的一种，用static关键字修饰的成员内部类被称为静态内部类。

**静态内部类的特点**
1. 静态内部类只能访问外部类中的静态变量和静态方法；
```java
public class Car {  
    String carName;  
    int carAge;  
	// 静态内部类
    static class Engine{  
        String engineName; 
    }  
}
```
2. 要访问非静态的需要创建外部类的对象

**创建静态内部类的对象**
外部类名.内部类名 对象名 = new 外部类名.内部类名();
`Outer.Inner inner = new Outer.Inner();`

**调用非静态方法**
先创建对象，用对象调用

**调用静态方法**
外部类名.内部类名.方法名();
`Outer.Inner.show();`

### 03 局部内部类

将内部类定义在方法里面就叫局部内部类，类似于方法里面的局部变量。

**局部内部类的特点**
1. 局部内部类 相当于 局部变量
2. 外界无法直接使用局部内部类，需要在方法内部创建对象并使用
3. 该类可以直接访问外部类的成员，也可以访问方法内的局部变量
```java
public class Outer {  
    private int b = 10;  
    
    public void show(){  
        int a = 10;  
        // 局部内部类
        class Inner{  
            String name;  
            int age;  
            public void method(){  
                System.out.println(a);  
                System.out.println(b);  
                System.out.println("局部内部类中的方法");  
            }  
            public static void method2(){  
                System.out.println("局部内部类中的静态方法");  
            }  
        }  
  
        Inner i = new Inner();  
        System.out.println(i.name);  
        System.out.println(i.age);  
        i.method();  
        Inner.method2();  
    }  
}
```

### 04 匿名内部类

匿名内部类本质上是隐藏了名字的内部类

**匿名内部类格式**
```java
new 类名或者接口名(){ // 继承/实现
	重写方法;        // 方法重写
};

// 范例
public static void main(String[] args) {  
    new Swim(){  
        @Override  
        public void swim(){  
            System.out.println("重写了游泳的方法");  
        }  
    };  
}
```

**匿名内部类的由来**

1. 最开始的类名继承接口
```java
public class Student implements Swim {  
    @Override  
    public void swim(){  
        System.out.println("重写了游泳的方法");  
    }  
}
```
2. 去掉类名
```java
{  
    @Override  
    public void swim(){  
        System.out.println("重写了游泳的方法");  
    }  
}
```
3. 新的类实现Swim接口，表示这个没有名字的类需要重写接口中所有的抽象方法
```java
// 接口名();
new Swim() {  
    @Override  
    public void swim(){  
        System.out.println("重写了游泳的方法");  
    }  
};
```

**创建匿名内部类的对象**

```java
public static void main(String[] args) {  
    // 实现接口Swim  
    new Swim(){  
        @Override  
        public void swim(){  
            System.out.println("重写了接口中游泳的方法");  
        }  
    };  
    // 继承类Animal  
    new Animal(){  
        @Override  
        public void eat(){  
            System.out.println("重写了类中游泳的方法");  
        }  
    };  
}
```

**调用匿名内部类的对象**
[[JAVA#接口多态|接口多态]]
```java
public static void main(String[] args) {  
    // 实现接口多态
    Swim s = new Swim(){  
        @Override  
        public void swim(){  
            System.out.println("重写了接口中游泳的方法");  
        }  
    };  
}
```


# 九、面向对象

## 1. 面向对象是什么

Object Oriented，简称OO，是一种编程的思想和方法，面向对象是相对于面向过程来讲的，把相关的数据和方法组织为一个整体来看待，从更高的层次来进行系统，更贴近事物的自然运行模式。

## 2. 对象

万事万物皆对象

### 01 创建类的对象

```java
public class PhoneTest {  
    public static void main(String[] args) {  
        // 创建第一部手机的对象  
        Phone p1 = new Phone();
        // 创建第二部手机的对象  
        Phone p2 = new Phone();  
  
        // 给手机赋值  
        p1.brand = "小米";  
        p1.price = 1999.99;  
  
        // 获取手机对象中的值  
        System.out.println(p1.brand);  
        System.out.println(p1.price);  
  
        // 调用手机中的方法  
        p1.call();  
        p1.playGame();  
    }  
}
```

### 02 使用对象

1. 访问属性：对象名，成员变量;
2. 访问行为：对象名，方法名(...)。

### 03 [[JAVA#九、Java内存分配|对象的内存图]]

## 3. 封装

封装是面向对象三大特征之一

对象代表什么，就得封装对应的数据，并提供数据对应的行为，如，人关门，关门的行为应该写在门这个类里。
```java
public class door(){
	private String brand;
	private String code;
	private double money;
	...
	public void close(){
		sout("关门")
	}
}
```


## 4. 继承

继承是面向对象三大特征之一

### 01 继承的特点

1. 继承的类称为子类（派生类），被继承的类成为父类 **super（基类或超类）**；
2. 子类可以在父类的基础上，增加其他的功能，使子类更强大；
3. java中提供一个关键字extends，可以让一个类跟另一个类建立联系；
4. 继承可以把多个子类中重复的代码抽取到父类中，提高代码的复用性。

```java
public class person{
	private String name;
	private int age;
	...
	public void sleep(){sout("sleep...")}
}

public class Student extends person{
	private int score;
	public void sleep(){sout("study...")}
}

public class teacher extends person{
	private int prize;
	public void sleep(){sout("teach...")}
}
```

### 02 单继承

1. java只支持单继承，一个类只能继承一个直接父类，不支持多继承，但支持多层继承；
2. 多层继承：子类A继承父类B，父类B可以继承父类C；
3. 每一个类都直接或间接继承Object；

### 03 子类能继承父类的哪些内容

1. 父类的所有构造方法都不能继承；
2. 父类的私有成员变量可以继承，但不能使用；
3. 父类的非private、非static、非final的成员方法能继承；

### 04 成员变量的访问特点

就近原则：先在局部位置找，再到本类成员位置找，父类成员位置找，逐级往上；
   ```java
	public class Test(){
		public static void main(String[] args) {  
		    Zi z = new Zi();  
		    z.ziShow();  
	    }
	}
	class Fu{
		String name = "Fu";
	}
	class Zi extends Fu{
		String name = "Zi";
		public void ziShow(){
			String name = "ziShow";
			sout(name);       // "ziShow"
			sout(this.name);  // "Zi"
			sout(super.name); // "Fu"
		}
	}
   ```

### 05 成员方法的访问特点

就近原则
   ```java
	public class Test(){
		public static void main(String[] args) {  
		    Student s = new Student();  
		    s.lunch();  
	    }
	}
	class Person{
		public void eat(){
			sout("吃饭");
		}
		public void drink(){
			sout("喝开水");
		}
	}
	class Student extends Person{
		public void lunch(){
			eat();
			drink();
		}
	}
   ```

### 06 [[JAVA#4. 方法重写|方法重写]]

### 07 构造方法的访问特点

   - 父类中的构造方法不会被子类继承；
   - 子类中所有的构造方法默认先访问父类中的无参构造，在执行自己；
   - 子类初始化之前，一定要调用父类构造方法先完成父类数据空间的初始化；
   - 子类构造方法的第一行语句默认：super()，
   ```java
   public class Test(){
		public static void main(String[] args) {  
		    Student s = new Student();  
	    }
	}
	class Person{
		String name;
		int age;
		
		public Person(){
			sout("父类先调用");
		}
		public Person(String name, int age){
			this.name = name;
			this.age = age;
		}
	}
	class Student extends Person{
		public Student(){
			super();
			sout("子类再调用");
		}
		public Student(String name, int age){
			super(name,age)
		}
	}
   ```

## 5. 多态

多态是面向对象三大特征之一，多态是建立在封装和继承衍生之上的，同类型的对象表现的多种形态。

### 01 多态的前提

- 有继承/实现关系
- 有父类引用指向子类对象
- 有方法重写

### 02 多态调用成员的特点

```java
public class Test {  
    public static void main(String[] args) {  
        Animal a = new Dog();  
        /* 调用成员变量:编译看左边,运行也看左边  
            编译看左边:javac编译代码的时候,会看左边的父类中有没有这个变量,如果有,编译成功,如果没有编译失败。  
	        运行也看左边:java运行代码的时候,实际获取的就是左边父类中成员变量值。  
		*/
        System.out.println(a.name);  
        /* 调用成员方法:编译看左边,运行看右边  
        编译看左边:javac编译代码的时候,会看左边的父类中有没有这个方法,
					如果有,编译成功,如果没有编译失败。  
        运行看右边:java运行代码的时候,实际上运行的是子类中的方法。  */
        a.show(); 
    }  
}  
  
class Animal{  
    String name = "动物";  
  
    public void show(){  
        System.out.println("Animal---show方法");  
    }  
}  
  
class Dog extends Animal{  
    String name = "狗";  
  
    public void show(){  
        System.out.println("Dog---show方法");  
    }  
}
```

### 03 多态的弊端

1. 不能调用子类的特有方法
   - 调用成员方法会检查父类中有没有这个方法，没有则直接报错；

### 04 解决方案：

1. 变回子类类型
    `Animal a = new Dog();` `Dog d = (Dog) a;`
2. 
```java
public class Test1 {  
    public static void main(String[] args) {  
        Animals a = new Cat();  
  
        /*if (a instanceof Dog){  
            Dog d = (Dog) a;            
            d.lookHome();        
        }else if(a instanceof Cat){            
            Cat c = (Cat) a;           
            c.catchMouse();        
        }else{            
		    System.out.println("没有这个类型");  
        }*/        
        
        // jdk14新特性  
        if (a instanceof Dog d){  
            d.lookHome();  
        }else if(a instanceof Cat c){  
            c.catchMouse();  
        }else{  
            System.out.println("没有这个类型");  
        }  
    }  
}  
  
class Animals{  
    public void show(){  
        System.out.println("Animal---show方法");  
    }  
}  
  
class Dog extends Animal{  
    public void show(){  
        System.out.println("Dog---show方法");  
    }  
    public void lookHome(){  
        System.out.println("看家");  
    }  
}  
  
class Cat extends Animal{  
    public void show(){  
        System.out.println("Cats---show方法");  
    }  
    public void catchMouse(){  
        System.out.println("抓老鼠");  
    }  
}
```

## 6. 构造方法

1. 构造方法也叫做构造器、构造函数。
2. 作用：在创建对象的时候，虚拟机会自动调用构造方法，给成员变量进行赋值的。

### 01 构造方法的格式

```java
public class Student {
	修饰符 类名(参数){
		方法体;
	}
	public Student(){
	}
}
```

### 02 构造方法的特点

1. 方法名和类名相同，连大小写也要一致；
2. 没有返回值类型，连void都没有；
3. 没有具体的返回值（不能由retrun带回结果数据）。
4. 创建对象的时候由虚拟机调用，不能手动调用构造方法；
5. 每创建一次对象，就会调用一次构造方法；

### 03 空参和带参构造

```java
public class Student {
	// 1. 空参
	// 如果没有写构造方法，那么虚拟机会加一个空参构造方法
	public Student(){
		sout();
	}
	
	// 2. 带参
	public Student(String name, int age){
		this.name = name;
		this.age = age;
	}
}
```

### 04 调用构造方法

```java
public class StudentTest {
	public static void main(String[] args){
		// 创建对象
		// 调用空参构造
		Student s = new Student();

		// 调用实参构造
		Student s = new Student("zhangsan", 23);
		sout(s.getName()); // zhangsan
		sout(s.getAge()); // 23
	}
}
```

### 05 注意事项

1. 如果没有写构造方法，那么虚拟机会加一个空参构造方；
2. 如果没有写构造方法，那么虚拟机会加一个空参构造方法；
3. 带参构造方法，和无参构造方法，两者方法名相同，但是参数名不同，这叫做构造方法的重载；
4. 无论是否使用，都手动书写无参数的、有全部参数的构造方法。

# 十、字符串String

## 1. String

1. String是Java定义好的一个类。定义在java.lang包中，所以使用的时候不需要导包。
2. java程序中的所有字符串文字（例如 "Hello World"），都被视为此类的对象。
3. 字符串是常量，它们的值在创建之后是不会发生改变的，它的对象在创建后不能被更改。
4. String 类是[[JAVA#final|final]]修饰的。

## 2. 创建String对象

### 01 直接赋值

``String name = "Hellp World";``

### 02 构造方法

|构造方法|说明|
|:-|:-|
|public String()|创建空白字符串，不含任何内容|
|public String(String original)|根据传入的字符串，创建字符串对象|
|public String(char[] chs)|根据传入的字符数组，创建字符串对象|
|public String(byte[] chs)|根据传入的字节数组，创建字符串对象|

### 03 运行结果

```java
public static void main(String[] args) {
	// 直接赋值
    String s1 = "abc";  
    System.out.println(s1);    // abc  

    // 创建空白字符串
    String s2 = new String();  
    System.out.println(s2);    // 

	// 传入字符串
    String s3 = new String("abc");  
    System.out.println(s3);    // abc

	// 传入字符数组
    char[] chs = {'a', 'b', 'c', 'd'};  
    String s4 = new String(chs);  
    System.out.println(s4);    // abcd
}
```

## 3. 比较String

若要比较字符串的内容，就必须要用String里面的方法。

```java
Scanner sc = new Scanner(System.in);
System.out.println("请输入一个字符串");

String s1 = sc.next();   // abc 是new出来的
String s2 = "abc";

System.out.println(s1 == s2); // false
```

```java
String s1 = "abc";
String s2 = "abc";

System.out.println(s1 == s2); // true
```

```java
String s1 = new String("abc"); // 记录的是堆里面的地址值
String s2 = "abc";             // 记录的是串池里的地址值

System.out.println(s1 == s2);  // false
```

### 02 equals()

1. boolean equals方法(要比较的字符串)；
2. 比较的是字符串的值，结果完全一样就是true，否则为false。

```java
String s1 = new String("abc");
String s2 = "abc";

boolean result = s1.equals(s2);
System.out.println(result); // true
```

### 03 equalsIgnoreCase()

1. boolean equalsIgnoreCase方法(要比较的字符串)；
2. 比较的是字符串的值，并忽略大小写。

```java
String s1 = new String("abc");
String s2 = "abc";

boolean result = s1.equalsIgnoreCase(s2);
System.out.println(result); // true
```

## 4. 遍历String

|构造方法|说明|
|:-|:-|
|public char charAt(int index)|根据索引返回字符|
|public int length()|返回此字符串的长度|


```java
public static void main(String[] args) {
    // 遍历数组  
    Scanner sc = new Scanner(System.in);
    System.out.println("请输入一个字符串");
    String str = sc.next(); 
    
    for (int i = 0; i < str.length(); i++) {
        // i 依次表示字符串的每一个索引  
        char c = str.charAt(i);
        System.out.println(c);
    }
}
```

## 5. 拼接String

定义一个方法，把int数组中的数据按照指定格式拼接成一个字符串返回，在控制台输出结果。

```java
public static void main(String[] args) {  
    int[] arr = {1, 2, 3, 4, 5};  
    String s = arrToString(arr);  
    System.out.println(s);  
}  
public static String arrToString(int[] arr){  
    if(arr == null){  
        return "";  
    }else if(arr.length == 0){  
        return "[]";  
    }  
    String result = "[";  
    for (int i = 0; i < arr.length; i++) {  
        if(i != arr.length-1){  
            result = result + arr[i] + ",";  
        }else{  
            result = result + arr[i] + "]";  
        }  
    }  
    return result;  
}
```

## 6. 反转String

 ```java
 public static void main(String[] args) {  
    // 定义一个方法，实现字符串反转。
    String result = reverseStr("abc");  
    System.out.println(result);  
}  
public static String reverseStr(String str){  
    String result = "";  
    for (int i = str.length()-1; i >= 0; i--) {  
        result = result + str.charAt(i);  
    }  
    return result;  
}
```

## 7. 截取String

String substring(开始值, 结束值);

只有返回值才是截取后的结果

包头不包尾

```java
public static void main(String[] args){
	String str = "1234567";

	String result = str.substring(0, 3); // 123
}
```

## 8. 替换String

String replace(旧值, 新值);

只有返回值才是替换后的结果

```java
public static void main(String[] args){
	String say = "呵呵，NTMD";

	// 定义一个敏感值数组
	String[] str = {"NTMD", "CTMD", "SB"};

	for(int i = 0; i < str.length; i++){
		say = say.replace(str[i], "*\**");
	}

	System.out.println(say);
}
```

## 9. StringBuilder

可以看成一个容器，创建之后里面的**内容是可变**的，因为StringBuilder是Java已经写好的类，Java在底层对它做了一些处理，打印对象不是地址值而是属性值，提高字符串的操作效率。

### 01 源码分析

1. 创建一个字节数组，默认容量：16
2. 若超过默认容量，则会自动扩容，新容量 = 旧容量\*2+2
3. 若超过新容量，则以实际容量为准


### 02 构造方法

|方法名|说明|
|:-|:-|
|public StringBuilder()|创建一个空白可变的字符串对象，不含内容|
|public StringBuilder(String str)|根据字符串的内容，来创建可变字符串对象|

### 03 常用方法

|方法名|说明|
|:-|:-|
|public StringBuilder append(任意类型)|添加数据，并返回对象本身|
|public StringBuilder reverse()|反转容器中的内容|
|public int length()|返回长度（字符出现的个数）|
|public int capacity()|返回容量|
|public String toString()|通过toString()就可以实现把StringBuilder转换为String|

### 04 运行结果

1. 创建StringBuilder对象
```java
public static void main(String[] args) {  
    // 创建对象  
    StringBuilder sb = new StringBuilder();  
    StringBuilder sb1 = new StringBuilder("abc");  

    System.out.println(sb);  //   
    System.out.println(sb1);  // abc
}
```
2. 添加元素
```java
public static void main(String[] args) {  
    // 创建对象  
    StringBuilder sb = new StringBuilder("abc");  
  
    sb.append(12);  
    sb.append(2.3);
    sb.append(true);
    System.out.println(sb);  //   abc122.3true
}
```
3. 反转元素
```java
public static void main(String[] args) {  
    // 创建对象  
    StringBuilder sb = new StringBuilder("abc");  
  
    sb.reverse();  
    System.out.println(sb);  //   cba
}
```
4. 获取元素长度
```java
public static void main(String[] args) {  
    // 创建对象  
    StringBuilder sb = new StringBuilder("abc");  
  
    int len = sb.length();  
    System.out.println(len);  //   3
}
```
5. toString
	把StringBuilder变回字符串
```java
public static void main(String[] args) {  
    // 创建对象  
    StringBuilder sb = new StringBuilder("abc");  
  
    sb.append(12);  
    System.out.println(sb);  //   abc12

	String str = sb.toString();
    System.out.println(str); 
}
```

### 05 链式编程

当我们在调用一个方法时，不需要用变量接收它的结果，可以继续调用其它方法。

```java
public static void main(String[] args) {  
	int len=getString().substring(1).replace("A","Q").length();
    System.out.println(len);  //   
}
public static String getString(){
	String str = "ABC";
	return str;
}
```

## 10. StringJoiner

StringJoiner跟StringBuilder一样，可以看成一个容器，创建之后里面的**内容是可变**的。

### 01 构造方法

|方法名|说明|
|:-|:-|
|public StringJoiner(间隔符号)|创建一个StringJoiner对象，指定拼接时的间隔符号|
|public StringJoiner(间隔符号, 开始符号, 结束符号)|创建一个StringJoiner对象，指定拼接时的间隔符号, 开始符号, 结束符号|

### 02 成员方法

|方法名|说明|
|:-|:-|
|public StringJoiner add(添加到内容)|添加数据，并返回对象本身|
|public int length()|返回长度（字符出现的个数）|
|public String toString()|返回一个字符串（该字符串就是拼接后的结果）|

### 03 运行结果

```java
// add
public static void main(String[] args){
	StringJoiner sj1 = new StringJoiner("---");  
	StringJoiner str1 = sj1.add("aaa").add("bbb").add("ccc");
	System.out.println(str1);  // aaa---bbb---ccc


	StringJoiner sj2 = new StringJoiner(", ","[","]");  
	StringJoiner str2 = sj2.add("aaa").add("bbb").add("ccc");  
	System.out.println(str2);  // [aaa,bbb,ccc]
}

// length
public static void main(String[] args) {  
    StringJoiner sj = new StringJoiner(",", "[", "]");  
    sj.add("aaa").add("bbb").add("ccc");  
    
    int len = sj.length();  
    System.out.println(len); // 15 包括了逗号和中括号  
}
```

# 十一、集合ArrayList

## 1. 泛型

限定集合中存储数据的类型

```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	
	ArrayList<String> list = new ArrayList<>();
}
```

## 2. 包装类

在集合中，基本数据类型不能直接存入集合，需要转为对应的包装类；

基本数据类型对应的包装类

1. byte
   `ArrayList<Byte> list = new ArrayList<>();`
2. short
   `ArrayList<Short> list = new ArrayList<>();`
3. char
   **`ArrayList<Character> list = new ArrayList<>();`
4. int
   **`ArrayList<Integer> list = new ArrayList<>();`**
5. long
   `ArrayList<Long> list = new ArrayList<>();`
6. float
   `ArrayList<Float> list = new ArrayList<>();`
7. double
   `ArrayList<Double> list = new ArrayList<>();`
8. boolean
   `ArrayList<Boolean> list = new ArrayList<>();`

## 3. 成员方法

### 01 添加

boolean add(E e)：添加元素，返回值表示是否添加成功；

```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	
	boolean result = list.add("abc");
	System.out.println(result); // 永远会是true
}
```

### 02 删除

1. boolean remove(E e)：删除指定元素，返回值表示是否删除成功；
   
```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	list.add("abc");
	
	boolean result = list.remove("abc");
	System.out.println(result); // true
}
```

2. E remove(int index)：删除指定索引的元素，返回被删除元素；
      
```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	list.add("abc");
	
	int result = list.remove(0);
	System.out.println(result); // "abc"
}
```


### 03 修改

E set(int index, E e)：修改指定索引下的元素，返回原来的元素；
   
```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	list.add("abc");
	
	String result = list.set(0, "aaa");
	System.out.println(result); // "abc"
}
```

### 04 查询

1. E get(int index)：获取指定索引的元素；
      
```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	list.add("abc");
	
	String result = list.get(0);
	System.out.println(result); // "abc"
}
```

2. int size()：集合的长度，也是集合中元素的个数；
      
```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	list.add("abc");
	
	int result = list.size();
	System.out.println(result); // 1
}
```

3. 遍历集合

```java
public static void main(String[] args){
	// JDK7以前的写法
	ArrayList<String> list = new ArrayList<String>();
	list.add("abc");
	
	for(int i = 0; i < list.size(); i++){
		System.out.println(list.get(i));
	}
}
```

# 十二、接口

## 1. 接口

interface，接口是一个规则，是对行为的抽象。

### 01 接口的定义格式

`public interface 接口名{}`

### 02 接口和类的关系

1. 接口和类之间是实现关系，可以单实现，也可以多实现，通过关键字implements关键字表示
	`public class 类名 implement 接口名{}`
2. 接口可以单实现，也可以多实现
   `public class 类名 implements 接口名1, 接口名2{}`

### 03 接口和接口的关系

接口和接口之间是继承关系，可以单继承，也可以多继承
```java
public interface Inter1 {  
    public abstract void method();  
}

public interface Inter2 extends Inter1{  
    public abstract void method2();  
}

public class Test implements Inter2{  
    @Override  
    public void method(){  
        System.out.println("method");  
    }  
    @Override  
    public void method2(){  
        System.out.println("method2");  
    }  
}
```

### 04 实现类

1. 就是实现接口的类，它要么重写接口中的所有抽象方法，要么是抽象类
2. 实现类还可以在继承类的同时实现多个接口
   `public class 类名 extends 父类 implements 接口名1, 接口名2{}`

### 05 接口中的成员

1. 成员变量：只能是常量，默认修饰符 public [[JAVA#static|static]] [[JAVA#final|final]] ；
2. 构造方法：没有；
3. 成员方法：只能是抽象方法，默认修饰符 public abstract ；

### 注意事项

1. jdk7 以前：接口中只能定义抽象方法；
2. jdk8 的新特性：接口中可以定义有方法体的方法（默认、静态）；
3. jdk9 的新特性：接口中可以定义私有方法（private）。

## 2. jdk8 新增的方法

### 01 接口中的默认方法

1. 允许在接口中定义默认方法，需要使用关键字default修饰，**解决接口升级问题；
2. 接口中的默认方法的定义格式：`public default 返回值类型 方法名(参数列表){}`；
3. 接口中的默认方法不是抽象方法，所以不强制重写。但是如果被重写，重写时去掉default关键字；
4. 如果实现了多个接口，多个接口中存在相同名字的默认方法，子类就必须对该方法进行重写。
```java
public class Test {  
    public static void main(String[] args) {  
        InterImpl il = new InterImpl();  
        il.show();  // 重写的默认方法
    }  
}
public interface Inter {  
    public static void show(){  
        System.out.println("接口中的静态方法");  
    }  
}
public class InterImpl implements Inter{  
    @Override  
    public void show(){  
        System.out.println("重写的默认方法");  
    }  
}
```

### 02 接口中的静态方法

1. 允许在接口中定义静态方法，需要使用关键字static修饰；
2. 接口中的静态方法的定义格式：`public static 返回值类型 方法名(参数列表){}`；
3. 接口中的静态方法不能重写；
4. 如果实现了多个接口，多个接口中存在相同名字的静态方法，子类无需对该方法进行重写；
5. 静态方法只能通过接口名调用，不能通过对象调用。

```java
public class Test {  
    public static void main(String[] args) {  
        Inter.show();  // 接口中的静态方法
        Inter1.show();  // 另一个接口中的静态方法
    }  
}
public interface Inter {  
    public static void show(){  
        System.out.println("接口中的静态方法");  
    }  
}
public interface Inter1 {  
    public static void show(){  
        System.out.println("另一个接口中的静态方法");  
    }  
}
```

## 3. jdk9 新增的方法

### 01 普通的私有方法

1. 普通的私有方法，给默认方法服务的；
2. 接口中的默认方法的定义格式：`private 返回值类型 方法名(参数列表){}`；
```java
public interface InterA {  
    public default void show1(){  
        System.out.println("show1方法开始执行了");  
        show3();  
    }  
    public default void show2(){  
        System.out.println("show2方法开始执行了");  
        show3();  
    }  
      
    private void show3(){  
        System.out.println("程序运行中，此处省略100行代码");  
    }  
}
```

### 02 静态的私有方法

1. 静态的私有方法，给静态方法服务的；
2. 静态的私有方法的定义格式：`private static 返回值类型 方法名(参数列表){}`；
```java
public interface InterB {  
    public static void show1(){  
        System.out.println("show1方法开始执行了");  
        show3();  
    }  
    public static void show2(){  
        System.out.println("show2方法开始执行了");  
        show3();  
    }  
  
    private static void show3(){  
        System.out.println("程序运行中，此处省略100行代码");  
    }  
}
```

## 接口多态

当一个方法的参数是接口时，可以传递接口所有实现类的对象，这种方式称为接口多态。

接口类型 j = new 实现类对象();

## 适配器设计模式

当一个接口中抽象方法过多，但只使用其中一部分时，就可以应用适配器设计模式。

```java
public interface Inter {  
    public abstract void method1();  
    public abstract void method2();  
    public abstract void method3();  
}
public class InterAdapter implements Inter{  
    @Override  
    public void method1() {}  
    @Override  
    public void method2() {}  
    @Override  
    public void method3() {}  
}
public class InterImpl extends InterAdapter{  
    @Override  
    public void method3(){  
        System.out.println("只有method3");  
    }  
}
```

# 十三、常用API

## 1. Math

Math是一个工具类，帮助我们进行数学计算，私有化构造方法，所有方法都是静态的。

### 01 abs 相反数

public static int abs(int a)

```java
public static void main(String[] args) {  
    System.out.println(Math.abs(88)); // 88  
    System.out.println(Math.abs(-88)); // 88   
}
```

**如果整数的值没有对应的相反数则返回原值**

public static int absExact(int a)

```java
public static void main(String[] args) {  
    System.out.println(Math.abs(-2147483648)); // -2147483648  
    System.out.println(Math.absExact(-2147483648)); // error
}
```

若传入的值超过范围则报错

### 02 ceil 向上取整

**进一法：往数轴正方向进一**

public static double ceil(double a)

```java
public static void main(String[] args) {  
    System.out.println(Math.ceil(12.01)); // 13.0  
    System.out.println(Math.ceil(12.99)); // 13.0  
    System.out.println(Math.ceil(-12.01)); // -12.0  
}
```

### 03 floor 向下取整

**去尾法：往数轴负方向进一**

public static double floor(double a)

```java
public static void main(String[] args) {  
    System.out.println(Math.floor(12.01)); // 12.0  
    System.out.println(Math.floor(12.99)); // 12.0  
    System.out.println(Math.floor(-12.01)); // -13.0  
}
```

### 04 round 四舍五入

public static long round(double a)

```java
public static void main(String[] args) {  
    System.out.println(Math.round(12.34));  // 12  
    System.out.println(Math.round(12.54));  // 13  
    System.out.println(Math.round(-12.34));  // -12  
    System.out.println(Math.round(-12.54));  // -13  
}
```

### 05 max & min 最值

public static int max / min (int a, int b)

```java
public static void main(String[] args) {  
    System.out.println(Math.max(10,11)); // 11  
    System.out.println(Math.min(10,11)); // 10  
}
```

### 06 pow 次幂

public static double pow (double a, double b)

```java
public static void main(String[] args) {  
    System.out.println(Math.pow(2, 3)); // 8.0
    System.out.println(Math.pow(4, 0.5)); // 2.0
    System.out.println(Math.pow(2, -2)); // 0.25
}
```

### 07 sqrt & cbrt 开根号

public static double sqrt / cbrt (double a)

```java
public static void main(String[] args) {  
    System.out.println(Math.sqrt(4)); // 2.0
    System.out.println(Math.cbrt(8)); // 2.0
}
```

### 07 random 随机数

public static double random()

```java
public static void main(String[] args) {  
	System.out.println(Math.random()); // 0.0 到 1.0 之间  
	System.out.println(Math.floor(Math.random() * 100) +1); // 1.0 到 100.0
}
```

## 2. System

System 也是一个工具类，提供了一些与系统相关的方法

### 01 exit

public static void exit (int status)

**终止当前运行的java虚拟机

```java
public static void main(String[] args) {  
    // 0：表示当前虚拟机正常停止  
    System.exit(0);  
}
```

### 02 currentTimeMillis

public static ling currentTimeMillis()

**返回从时间原点到代码运行的时间的毫秒值形式**

```java
public static void main(String[] args) {  
    long start = System.currentTimeMillis();  
  
    for (int i = 0; i < 100000; i++) {  
        boolean flag = isPrime(i);  
        if(flag){  
            System.out.println(i);  
        }  
    }  
  
    long end = System.currentTimeMillis();  
    System.out.println(end = start);  
}
```

计算机中的时间原点：**1970年1月1日 00:00:00** 中国：**1970年1月1日 08:00:00**

1秒 = 1000毫秒
1毫秒 = 1000微妙
1微秒 = 1000纳秒

### 03 arraycopy

public static void arraycopy(数据源数组, 起始索引, 目的地数组, 起始数组, 数组长度)

```java
public static void main(String[] args) {  
    int[] arr1 = {1,2,3,4,5,6,7,8,9,10};  
    int[] arr2 = new int[10];
    
    System.arraycopy(arr1, 0, arr2, 0, 10);
}
```

如果数据源数组和目的地数组都是基本数据类型，那么两者的类型必须保持一致，否则报错

如果数据源数组和目的地数组都是引用数据类型，那么子类类型可以赋值给父类类型。

```java
public static void main(String[] args){
	Student s1 = new Student("001", "zhangsan");  
	Student s2 = new Student("002", "lisi");  
	Student s3 = new Student("003", "wangwu");  
  
	Student[] arr1 = {s1, s2, s3};  
	Person[] arr2 = new Person[3];  
	
	// 把arr1中对象的地址值赋值给arr2中  
	System.arraycopy(arr1, 0, arr2, 0, 3);  
	for (int i = 0; i < arr2.length; i++) {  
	    Student stu = (Student)arr2[i];  
	    System.out.println(stu.getId()+", "+stu.getName());  
	}
}
```

## 3. Runtime

Runtime表示当前虚拟机的运行环境

### 01 getRuntime

**当前系统的运行环境对象**

构造方法私有，只有一个runtime对象

```java
public static void main(String[] args) {  
    Runtime r1 = Runtime.getRuntime();  
    Runtime r2 = Runtime.getRuntime();  
    System.out.println(r1 == r2); // true  
}
```

### 02 exit

**停止虚拟机**

```java
public static void main(String[] args) {  
    Runtime r = Runtime.getRuntime();  
    r.exit(0);
    // Runtime.getRuntime().exit(0);
}
```

[[JAVA#2. System|System.exit]]调用的底层就是Runtime.getRuntime().exit(status);

```java
public static void exit(int status) {  
	Runtime.getRuntime().exit(status);
}
```

### 03 availableProcessors

**获得CPU的线程数**

System.out.println(Runtime.getRuntime().availableProcessors
```java
public static void exit(int status) {  
	Runtime.getRuntime().exec("notepad");
}
```

### 04 maxMemory

JVM能从系统中获取总内存大小（单位：byte）

```java
public static void exit(int status) {  
System.out.println(Runtime.getRuntime().maxMemory());
}
```

### 05 totalMemory

JVM已经从系统中获取的总内存大小（单位：byte）

```java
public static void exit(int status) {  
System.out.println(Runtime.getRuntime().totalMemory());
}
```

### 06 freeMemory

JVM剩余内存大小（单位：byte）

```java
public static void exit(int status) {  
System.out.println(Runtime.getRuntime().freeMemory());
}
```

### 07 exec

运行cmd命令

```java
public static void exit(int status) {  
	Runtime.getRuntime().exec("notepad");
	// shutdown：关机  
	// -s ：默认1分钟之后关机  
	// -s -t 指定时间 ：指定关机时间(秒)
	// -a ：取消关机操作  
	// -r ：关机并重启  
	Runtime.getRuntime().exec("shutdown -s -t -18000");
}
```

## 4. Object

**Object是Java中的顶级父类，所有类都直接或间接的继承于Object；**
Object类中的方法可以被所有子类访问，所以我们要学习Object类和其中的方法。

### 01 Object的构造方法

public Object()  -> 空参构造

普通类没有一个共有的共性，所以默认空参构造方法；
super()默认访问无参构造方法

### 02 toString -- Object的成员方法

public String toString()

**没有重写 toString 方法，默认使用Object中的，返回对象的字符串表示形式（地址值）  **
**重写 toString 方法： 看到对象内部的属性值**

```java
public static void main(String[] args) {  
    // toString 返回对象的字符串表示形式（地址值）  
    Object obj = new Object();  
    String str1 = obj.toString();  
    System.out.println(str1); // java.lang.Object@776ec8df  
  
    Student student = new Student();  
    String str2 = student.toString();  
    System.out.println(str2); // api_08.object.Student@3b07d329  
  
    // System：类名  
    // out：静态变量  
    // System.out：获取打印的对象  
    // println()：方法  
    // 参数：打印的内容  
    // 核心逻辑：  
    // 当打印一个对象时，底层会调用对象的toString方法，把对象变成字符串  
    System.out.println(student);
}
// 看到对象内部的属性值：重写toString方法  
@Override  
public String toString() {  
    return name + ", " + age;  
}
```

### 03 equals -- Object的成员方法

public boolean equals(Object obj)

**没有重写equals方法，那么默认使用Object中的方法进行比较，比较的时地址值是否相等**
**重写之后的equals方法比较的就是对象内部的属性值**

```java
public static void main(String[] args) {  
    Student s1 = new Student("zhangsan", 23);  
    Student s2 = new Student("zhangsan", 23);  
  
    // 没有重写equals方法，那么默认使用Object中的方法进行比较，比较的时地址值是否相等  
    boolean result = s1.equals(s2);  
    System.out.println(result);  
}
// 重写之后的equals方法比较的就是对象内部的属性值  
@Override  
public boolean equals(Object o){  
    if(this == o)return true;  
    if(o == null || getClass() != o.getClass()) return false;  
    Student student = (Student) o;  
    return age == student.age && Objects.equals(name, student.name);  
}
```

### 04 clone -- Object的成员方法

对象克隆

protected Object clone(int a)

方法在底层会帮我们创建一个对象，并把对象中的数据拷贝过去，浅克隆拷贝的是地址值

1. 重写Object中的clone方法  
2. 让javabean类实现Cloneable接口  
3. 创建对象并调用clone

```java
public class User implements Cloneable{  
    private String userName;  
    private String password;  
    private String cardNum;  
    private String phoneNum;  
    private int[] data;  
  

	......
  
    public String toString() {  
        return "User{userName = " + userName + ", password = " + password + ", cardNum = " + cardNum + ", phoneNum = " + phoneNum + ", data = " + arrToString() + "}";  
    }  
  
    public String arrToString(){  
        StringJoiner sj = new StringJoiner(", ", "[", "]");  
        for (int i = 0; i < data.length; i++) {  
            sj.add(data[i] + "");  
        }  
        return sj.toString();  
    }  
  
    @Override  
    protected Object clone() throws CloneNotSupportedException {  
        // 调用父类中的clone方法  
        return super.clone();  
    }  
}

```

```java
public static void main(String[] args) throws CloneNotSupportedException {  
    int[] arr = {1,2,3,4,5};  
    User u = new User("user1","123","440xx12","123",arr);  
  
    // 方法2在底层会帮我们创建一个对象，并把对象中的数据拷贝过去  
    // 1. 重写Object中的clone方法  
    // 2. 让javabean类实现Cloneable接口  
    // 3. 创建对象并调用clone  
    User u2 = (User) u.clone();  
  
    System.out.println(u);  
    System.out.println(u2);  
}
```

以上的克隆皆为浅克隆[[JAVA#04 对象克隆（浅克隆）|浅克隆]]

**以下为[[JAVA#05 深克隆|深克隆]]**

1. 重写方法
```java
@Override  
protected Object clone() throws CloneNotSupportedException {  
    // 调用父类中的clone方法  
    // 深克隆，先把被克隆对象的数组获取出来  
  
    int[] data = this.data;  
    int[] newData = new int[data.length];  
    for (int i = 0; i < data.length; i++) {  
        newData[i] = data[i];  
    }  
  
    User u = (User) super.clone();  
    u.data = newData;  
    return u;  
}
```

2. 第三方工具类 导包 gson
```java
public static void main(String[] args) throws CloneNotSupportedException {  

    int[] arr = {1,2,3,4,5};  
    User u = new User("user1","123","440xx12","123",arr);  
  
	Gson gson = new Gson();  
	// 把对象变成一个字符串  
	String s = gson.toJson(u);  
	System.out.println(s);  
	// 再把字符串变回对象  
	User user = gson.fromJson(s, User.class);  
	// 打印对象  
	System.out.println(user);
	
}
```


## 5. Objects

Objects是一个工具类，提供了一些方法完成一些功能

### 01 equals -- Objects的成员方法

public static boolean equals(Object a, Object b)

先做非空判断，比较两个对象

```java
public static void main(String[] args) {  
    Student s1 = null;  
    Student s2 = new Student("zhangsan", 26);  
  
    boolean result = Objects.equals(s1, s2);  
    System.out.println(result);  // false
}
```

如果s1不为null，那么就利用s1再次调用equals方法，如果s1是student类型，最终还是调用Student中的equals功能，没重写比的就是地址值

### 02 isNull -- Objects的成员方法

public static boolean isNull(Object obj)

判断对象是否为null，为null返回true，反之返回false

```java
public static void main(String[] args) {  
    Student s1 = null;  
    Student s2 = new Student("zhangsan", 26);  
  
    boolean result = Objects.isNull(s1);  
    System.out.println(result);  // true
}
```

### 03 nonNull -- Objects的成员方法

public static boolean nonNull(Object obj)


```java
public static void main(String[] args) {  
    Student s1 = null;  
    Student s2 = new Student("zhangsan", 26);  
  
    boolean result = Objects.equals(s1);  
    System.out.println(result);  // false
}
```

判断对象是否为null，为null返回false，反之返回true

## 6. BigInteger

在java中，整数有四种类型：byte，short，int，long
在底层占用字节个数：byte 1个字节、short 2个字节、int 4个字节、long 8个字节

若整数超出long的范围，则可以用到BigInteger。

对象一旦创建，内部的值不能发生改变，只要进行计算都会产生一个新的BigInteger对象

### 01 BigInteger的构造方法

public BigInteger(int num, Random rnd) 获取随机大整数，范围：\[0 ~ 2的num次方 - 1]
```java
public static void main(String[] args) {  
    BigInteger bg1 = new BigInteger(4, new Random());  
    System.out.println(bg1); // 0 ~ 2^4 
}
```

public BigInteger(String val) 获取指定的大整数
```java
public static void main(String[] args) {  
    BigInteger bg2 = new BigInteger("100");  
    System.out.println(bg2); // 100
}
```

public BigInteger(String val, int radix) 获取指定进制的大整数
```java
public static void main(String[] args) {  
    BigInteger bg3 = new BigInteger("100", 2);  
    System.out.println(bg3); // 4
}
```

public static BigInteger valueOf(long val) 静态方法获取BigInteger的对象，内部有优化（把-16 ~ 16 先创建好BigInteger的对象，如果多次获取不会重新创建新的）
```java
public static void main(String[] args) {  
    BigInteger bg = BigInteger.valueOf(100);  
    System.out.println(bg); // 100  
}
```

### 02 BigInteger的成员方法

**加法**：public BigInteger add(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	BigInteger add = bg1.add(bg2);  
	System.out.println(add); // 18
}
```
**减法**：public BigInteger subtract(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	BigInteger subtract = bg1.subtract(bg2);  
	System.out.println(subtract); // 14
}
```
**乘法**：public BigInteger multiply(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	BigInteger multiply = bg1.multiply(bg62);  
	System.out.println(multiply); // 32
}
```
**除法，获取商**：public BigInteger divide(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	BigInteger divide = bg1.divide(bg62);  
	System.out.println(divide); // 8
}
```
**除法，获取商和余数**：public BigInteger\[] divideAndRemainder(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	BigInteger[] arr = bg1.divideAndRemainder(bg2);  
	System.out.println(arr[0]+", "+arr[1]); // 8, 0
}
```
**比较是否相同**：public BigInteger equals(object x)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	boolean result = bg1.equals(bg2);  
	System.out.println(result); // false
}
```
**次幂**：public BigInteger pow(int exponent)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(8);  
	BigInteger pow = bg1.pow(2);  
	System.out.println(pow); // 64
}
```
**返回较大值/较小值**：public BigInteger max/min(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(16);  
	BigInteger bg2 = BigInteger.valueOf(2);  
	BigInteger max = bg5.max(bg6);  
	System.out.println(max); // 16
}
```
**转为int类型整数，超出范围有误**：public int intVaule(BigInteger val)
```java
public static void main(String[] args) {  
    BigInteger bg1 = BigInteger.valueOf(2);  
	BigInteger bg2 = BigInteger.valueOf(8);  
	BigInteger multiply = bg5.multiply(bg6);  
	System.out.println(multiply); // 16
}
```

## 7. BigDecima

## 8. 正则表达式

作用一：校验字符串
作用二：在一段文本中获取想要的内容

字符类（只匹配一个字符）
[abc] 只能是abc
[\^abc] 除了a,b,c之外的任何字符
[a-zA-Z] a到z与A到Z，包括azAZ
[a-d[m-p]] a到d，或m到p
[a-z&&[def]] a-z和def的交集。为：d，e，f
[a-z&&[\^bc]] a-z和非bc的交集。（等同于[ad-z])
[a-z&&[\^m-p]] a到z和除了m到p的交集。（等同于[a-lq-z]）

预定义字符（只匹配一个字符）
. 任何字符
\\d 一个数字：[0-9]
\\D 非数字：[\^0-9]
\\s 一个空白字符：[\\t\\n\\x0B\\f\\r]
\\S 非空白字符 [\^\\s]
\\w [a-zA-Z_0-9]英文、数字、下划线
\\W [\^\\W]一个非单词字符

数量词
X? X，一次或零次
X\* X，零次或多次
X+ X，一次或多次
X{n} X，正好n次
X{n,} X，至少n次
X{n,m} X，至少n但不超过m次

# Java内存分析

## 数组

### 01 java内存分配

1. 栈：方法运行时使用的内存，比如main方法运行，进入方法栈中运行；
2. 堆：存储对象或数组，new来创建，有地址值，都存储在堆内存；
3. 方法区：存储可以运行的class文件；
4. 本地方法栈：JVM在使用操作系统功能的时候使用，和我们开发无关；
5. 寄存器：给CPU使用，和我们开发无关。

### 02 数组的内存图

![[Pasted image 20231009105205.png]]

1. 只要是new出来的一定是在堆里面开辟了一个小空间；
2. 如果new了多次，那么在堆里面有多个小空间，每个小空间中都有各自的数据

![[Pasted image 20231009110134.png]]

1. 当两个数组指向同一个小空间时，其中一个数组进行修改过后，另一个数组访问时也是已经修改过后的。

### 03 二维数组的内存图

![[屏幕截图 2023-10-12 082242.png]]

![[屏幕截图 2023-10-12 083245.png]]

![[屏幕截图 2023-10-12 083319.png]]

## 对象

### 01 一个对象的内存图

![[屏幕截图 2023-10-16 085411.png]]

### 02 两个对象的内存图

![[Pasted image 20231016090528.png]]

### 03 两个引用指向同一个对象

![[Pasted image 20231016091047.png]]

## this关键字

![[Pasted image 20231016094138.png]]

![[屏幕截图 2023-10-16 094025.png]]

### 04 对象克隆（浅克隆）

基本数据类型记录具体值，引用数据类型记录是跟被克隆对象的地址值

![[Pasted image 20231108111843.png]]

### 05 深克隆

基本数据类型记录具体值，引用数据类型记录是一个新的地址值，但字符串拿的是串池的地址值

![[Pasted image 20231108112211.png]]

## 字符串

### 01 直接赋值

当用双引号直接赋值时，系统会检查该字符串在串池中是否存在。若不存在则创建新的，若存在则会复用。

![[Pasted image 20231019150514.png]]

### 02 构造方法

![[屏幕截图 2023-10-19 150448.png]]

### 03 字符串拼接

1. 等号右边没有变量
   ![[Pasted image 20231025094247.png]]
2. 等号右边有变量
   每一行拼接的代码，都会在内存中创建新的字符串，浪费内存。
   ![[Pasted image 20231025094725.png]]
   ![[Pasted image 20231025094705.png]]
3. java优化
```java
public static void main(String[] args){
	String s1 = "abc"; // 记录串池中的地址值
	String s2 = "a" + "b" + "c"; // 复用串池中的字符串
	// 在编译的时候，就会将"a" + "b" + "c"拼接为"abc"
	
	System.out.println(s1 == s2); // true
}
```

### 04 StringBuilder

所有要拼接的内容都会往StringBuilder中放，不会创建很多无用的空间，节约内存

![[Pasted image 20231025095429.png]]

## static内存图

![[Pasted image 20231030091214.png]]

![[Pasted image 20231030100416.png]]

## 继承

### 成员变量

![[Pasted image 20231030110658.png]]

### 私有化成员变量

![[Pasted image 20231030111039.png]]

### 成员方法

![[Pasted image 20231030111857.png]]

## 多态


![[Pasted image 20231031092853.png]]

## 内部类

![[Pasted image 20231103171734.png]]

# 关键字

## private

1. 是一个权限修饰符；
2. 可以修饰成员（成员变量和成员方法）；
3. 被 private 修饰的成员只能在本类中才能访问；
4. 针对 private 修饰的成员变量，如果需要被其他类使用，提供相应的操作；
5. 提供 ”setXxx(参数)“ 方法，用于给成员变量赋值，方法用 public 修饰；
6. 提供 ”getXxx()“ 方法，用于获取成员变量的值，方法用 public 修饰。

```java
public class Friend {  
    private int age;  

	// set方法：给成员变量age赋值的；
    public void setAge(int age) {  
        if (age >= 0 && age <= 100){  
            this.age = age;  
        }else{  
            System.out.println("年龄超出范围");  
        }  
    }  
	// get方法：对外提供成员变量age的值
    public int getAge() {  
        return age;  
    }  
}
```

```java
public static void main(String[] args) {  
    Friend f1 = new Friend();
    // 赋值
    f1.setAge(18);  
  
    System.out.println("年龄："+f1.getAge()); // 18  
}
```

## static

static表示静态，是java中的一个修饰符，可以修饰成员方法，成员变量；

### 01 静态变量

1. 被static修饰的成员变量，叫做静态变量；
2. 被该类的所有对象共享；
3. 不属于对象，属于类；
4. 随着类的加载而加载，优先于对象存在。
```java
public class Student{
	private String name;
	private int age;

	public static String teacherName;
}
```

### 02 静态方法

1. 被static修饰的成员方法，叫做静态方法；
2. 多用在测试类和工具类中，javabean类中很少会用；
3. 静态方法只能访问静态变量和静态方法；
4. 非静态方法可以访问静态变量和静态方法，也可以访问非静态变量和非静态方法；
5. 静态方法中是没有this关键字的；

### 03 [[JAVA#静态类|静态类]]

## this & 就近原则

### 01 this

this：可以理解为一个局部变量，表示当前方法调用者的地址值；

```java
public class ThisKey {  
	// 成员变量
    private int age;  
    public void method(){  
        int age = 10;  
        System.out.println(this.age);  // 0
    }  
}
```

### 02 就近原则

```java
public class ThisKey {  
    private int age;  
    public void method(){  
        int age = 10;  
        System.out.println(age);  // 10
    }  
}
```

### 03 this.()构造方法

```java
public class Person{
	String name;
	int age;
	
	public Person(){
		// 虚拟机不会再添加super()
		this(null,12);
	}
	public Person(String name, int age){
		this.name = name;
		this.age = age;
	}
}
```

## super

代表父类存储空间

## final

最终的、不可改变的

### 01 修饰方法

表明该方法是最终方法，不能被重写
```java
public final void show(){
	System.out.println("父类的方法");
}
```

### 02 修饰类

表明该类是最终类，不能被继承
```java
public final class Father{
	private String name;
}
```

### 03 修饰变量

final修饰的变量是基本类型：那么变量存储的字面量是不可改变的；
```java
final int a = 10;
```
final修饰的变量是引用类型：那么变量存储的地址值是不可改变的，内部的属性值还是可以改变的；
```java
final Student S = new Student("zhangsan", 23); 
```

## volatile
## synchronixed

## 包与导包

### 01 包

包就是文件夹，用来管理各种不同功能的java类，方便后期代码维护；

包名规则：全部英文小写，公司域名反写，如：qitong.com -> com.qitong

全类名：包名 + 类名

`com.qitong.demo.Student s = new com.qitong.demo.Student();`

### 02 导包

- 使用同一个包中的类时，不需要导包；
- 使用java.lang包中的类时，不需要导包；
- 其它情况都需要导包；
- 如果同时使用两个包中的同名类，需要用全类名。

## 权限修饰符

1. private：同一个类中可用；
2. 空着不写：同一个包里其他类可用；
3. protected：不同包的子类可用；
4. public：所有类可用；

## 代码块

### 01 局部代码块

```java
public static void main(String[] args){
	{
		int a = 10;
	}
	// 当代码执行到这，变量a就从内存中消失了
	// System.out.println(a)
}
```

### 02 构造代码块

- 写在成员位置的代码块；  
- 作用：可以把多个构造方法中重复的代码抽取出来；  
- 执行时机：我们在创建本类对象的时候会先执行构造代码块再执行构造方法  

```java
public class Student{
	private String id;  
    private String name;  
  
    {  
        System.out.println("开始创建对象");  
    }  
  
    public Student() {  
        System.out.println("空参构造");  
    }  
  
    public Student(String id, String name) {  
        System.out.println("带参构造");  
        this.id = id;  
        this.name = name;  
    }
}
```

### 03 静态代码块

格式：static{}
特点：需要通过static关键字修饰，随着类的加载而加载，并且自动触发，只执行一次；
使用场景：在类加载时，做一些数据初始化的时候使用。

```java
public class Login {  
    static ArrayList<User> list = new ArrayList<>();  
    static {  
        // 添加一个初始用户信息  
        list.add(new User("user1", "123", "12345678910111213x", "1234578910"));  
    }  
    public static void main(String[] args) {}
}
```


