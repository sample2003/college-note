# 一、Spring

Spring 是 JavaEE 的开发必备技能。
[[Spring 2023-10-21_15_0.excalidraw|Spring图示]]

## 1. 发展历程

## 2. 框架整合

高效整合其它技术，提高企业级应用开发与运行效率

## 3. 简化开发

降低企业级开发的复杂性

## 4. 

# 二、 Spring Framework

Spring Framework，容器 是 Spring 生态圈中最基础的项目

## 1. 核心概念

1. 使得目标充分解耦；

2. 使用IoC容器管理bean（IoC），在IoC容器内将有依赖关系的bean进行关系绑定（DI）

3. 最终使用对象时不仅可以直接从IoC容器中获取，并且获取到的bean已经绑定了所有的依赖关系

## 2. IoC

1. 全称 Inversion of Control ，控制反转。使用对象时，由主动使用new产生对象，转换为由外部提供对象，此过程中对象创建控制权由程序转移到外部。

2. 现在代码书写耦合度偏高，解决方案：使用对象时，在程序中不要主动使用new产生对象，转换为由外部提供对象。

3. Spring技术对IoC思想进行了实现
4. Spring提供了一个容器，称为IoC容器，用来充当IoC思想中的“外部”；
5. IoC容器负责对象的创建、初始化等一系列工作，被创建或被管理的对象在IoC容器中统称为Bean

## 3. DI

全称 Depenency Injection ，**依赖注入**

在容器中建立bean与bean之间的依赖关系的整个过程，被称为依赖注入

## 4. Bean

被创建或被管理的对象在IoC容器中统称为Bean

## 5. IoC入门案例

### 01 思路

1. 管理什么？（Service 与 Dao）；
2. 如何将被管理的对象告知IoC容器？（配置）；
3. 被管理的对象交给IoC容器，如何获取IoC容器？（接口）；
4. IoC容器得到后，如何从容器中获取bean？（接口方法）；
5. 使用Spring导入哪些坐标？（pom.xml)。

### 02 步骤

1. 导入spring坐标；（在pom.xml中）
```xml
<dependencies>  
	<dependency>
		<groupId>org.springframework</groupId>  
        <artifactId>spring-context</artifactId>  
        <version>5.2.10.RELEASE</version>  
    </dependency>
</dependencies>
```

2. 新建applicationContext.xml文件；(点击resources中的XML中的SpringConfig)
3. 在applicationContext.xml文件中，配置bean；
```xml
<beans ...>
	<!-- id表示给bean起名字，class表示给bean定义类型-->
	<bean id="bookDao" class="com.qitong.dao.impl.BookDaoImpl"/>
	<bean id="bookService" class="com.qitong.service.impl.BookServiceImpl"/>
</beans>
```
4. 获取Ioc容器 ^111111
```java
// 加载类路径下的配置文件
ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
```
[[Spring#^111112|第二种方式]]
5. 获取bean
```java
BookDao bookDao = (BookDao) ctx.getBean("bookDao");
```

## 6. DI入门案例

### 01 思路

1. 基于IoC管理bean；
2. Service中使用new形式创建的Dao对象是否保留？（否）；
3. Service中需要的Dao对象如何进入到Service中？（提供方法）；
4. Service与Dao间的关系如何描述？（配置）。

### 02 步骤

1. 基于Ioc容器管理bean；
2. 删除使用new的形式创建对象的代码；
```java
public class BookServiceImpl implements BookService {  
    private BookDao bookDao;
    public void save(){  
        System.out.println("bookservice save");  
        bookDao.save();  
    }
}
```
3. 提供依赖对象对应的setter方法；
```java
public class BookServiceImpl implements BookService {  
    private BookDao bookDao;
    public void save(){  
        System.out.println("bookservice save");  
        bookDao.save();  
    }  
	public void setBookDao(BookDao bookDao){  
	    this.bookDao=bookDao;  
	}
}
```
4. 配置service 与 dao之间的关系。
```xml
<!-- property标签表示配置当前bean的属性 -->
<!-- name属性表示配置哪一个具体的属性 -->
<!-- ref属性表示参照哪一个bean -->
<bean id="bookDao" class="com.qitong.dao.impl.BookDaoImpl"/>
<bean id="bookService" class="com.qitong.service.impl.BookServiceImpl">  
    <property name="bookDao" ref="bookDao"/>  
</bean>
```

## 6. bean配置

### 01 bean基本配置

![[Pasted image 20231022103359.png|800]]

### 02 bean别名配置

![[Pasted image 20231022103829.png|800]]

### 03 bean配置范围

![[Pasted image 20231208160711.png|800]]
1. spring创建的bean默认为单例对象；
2. 适合交给容器进行管理的bean
   - 表现层对象，如 servlet
   - 业务层对象，如 sevice
   - 数据层对象，如 dao
   - 工具对象
3. 不适合交给容器进行管理的bean
   - 封装实体的域对象

## 8. bean实例化

bean本质上就是对象，创建bean使用构造方法、静态工厂或实例工厂完成；

### 01 构造方法

1. 提供可访问的构造方法
```java
public class BookDaoImpl implements BookDao{
	public BookDaoImpl(){
		System.out.println("book constructor is running");
	} 
	public void save(){
		System.out.println("book dao save");
	}
}
```
2. 配置
```xml
<bean id="bookDao" class="com.qitong.dao.impl.BookDaoImpl"/>
```
3. 无参构造方法如果不存在，将抛出异常==BeanCreationException==

### 02 静态工厂

1. 静态工厂
```java
public class OrderDaoFactory{
	public static OrderDao getOrderDao(){
		return new OrderDaoImpl();
	}
}
```
2. 配置
```xml
<!-- 配置的不仅是工厂对象，还有写出创建对象的方法名 -->
<bean id="orderDao" class="com.qitong.factory.OrderDaoFactory" factory-method="getOrderDao"/>
```

### 03 实例工厂

1. 实例工厂
```java
public class UserDaoFactory{
	public UserDao getUserDao(){
		return new UserDaoImpl();
	}
}
```
2. 配置
```xml
<!-- 配置工厂对象 -->
<bean id="userFactory" class="com.qitong.factory.UserDaoFactory"/>

<!-- 写出工厂对象 -->
<bean id="userDao" factory-bean="userFactory" factory-method="getUserDao"/>
```

### 04 使用FactoryBean实例化bean

```java
public class UserDaoFactoryBean implements FactoryBean<UserDao>{
	// 代替原始实例工厂中创建对象的方法
	public UserDao geObject() throws Exception{
		return new UserDaoImpl();
	}
	// 得到bean的类型
	public Class<?> getObjectType(){
		return UserDao.class;
	}
	// 返回true表示创建的是单例对象，默认为true
	public boolean isSingleton(){
		return true;
	}
}
```

```xml
<bean id="userDao" class="com.qitong.factory.UserDaoFactoryBean"/>
```

## 9. bean生命周期

### 01 什么是bean生命周期

1. 生命周期：从创建到销毁的完整过程
2. bean的生命周期：
   - 初始化容器：
     1. 创建对象（内存分配）
     2. 执行构造方法
     3. 执行属性注入（set操作）
     4. **执行bean初始化方法**
   - 使用bean：执行业务操作
   - 关闭/销毁容器：**执行bean销毁方法**
3. bean生命周期控制：在bean创建后到销毁前做一些事情

### 02 配置方法

1. 提供生命周期控制方法
```java
public class BookDaoImpl implements BookDao{
	public void save(){
		System.out.println("book dao save");
	}
	// bean初始化对应的操作
	public void init(){
		System.out.println("init...")
	}
	// bean销毁前对应的操作
	public void destory(){
		System.out.println("destory...")
	}
}
```
2. 配置生命周期控制方法
```xml
<bean 
	  id="bookDao" 
	  class="com.qitong.dao.impl.BookDaoImpl" 
	  init-method="init" 
	  destory-method="destory"
/>
```

### 03 接口控制

1. 实现InitializingBean，DisposableBean接口
```java
public class BookServiceImpl implements BookService,InitializingBean,DisposableBean{
	public void save(){
		System.out.println("book dao save");
	}
	// bean销毁前对应的操作
	public void destory() throws Exception{
		System.out.println("destory...")
	}
	// bean初始化对应的操作
	public void afterPropertiesSet() throws Exception{
		System.out.println("afterPropertiesSet...")
	}
}
```

```xml
<bean 
	  id="bookService" 
	  class="com.qitong.service.impl.BookServiceImpl"
>  
    <property name="bookDao" ref="bookDao"/>  
</bean>
```

### 04 bean销毁时机

- 容器关闭前触发bean的销毁
- 关闭容器方式
  1. 手工关闭容器
     `ConfigurableApplicationContext`接口 close() 操作
  2. 注册关闭钩子,在虚拟机退出前先关闭容器再退出虚拟机
     `ConfigurableApplicationContext`接口 registerShutdownHook() 操作
```java
public class AppForLifeCycle{
	public static void main(String[] args){
		C... ctx = new C...("applicationContext.xml");
		ctx.close();
		// ctx.registerShutdownHook();
}
```

## DI方式

### 01 DI方式的由来

**向一个类中传递数据的方式有两种**

- 普通方法(set方法)
- 构造方法

**依赖注入描述了在容器中建立bean与bean之间依赖关系的过程,如果bean运行需要的是数字或字符串呢?**

- 引用类型
- 简单类型(基本数据类型与String)

### 02 有哪些依赖注入方式

**setter注入**

1. 简单类型
2. 引用类型

**构造器注入**

1. 简单类型
2. 引用类型

### 03 setter注入

#### **简单类型**

```java
public class BookDaoImpl implements BookDao{
	private int connectionNum;
	private String databaseName;

	public void setConnectionNum(int connectionNum) {
		this.connectionNum = connectionNum;
	}
	public void setDatabaseName(String databaseName) {
		this.databaseName = databaseName;
	}

	public void save() {
		System.out.println("bookDao save .."+databaseName+","+connectionNum);
	}
}
```

```xml
<bean 
	  id="bookDao" 
	  class="com.qitong.dao.impl.BookDaoImpl"
>  
    <property name="databaseName" value="mysql"/>  
    <property name="connectionNum" value="10"/> 
</bean>
```

#### **引用类型**

```java
public class BookServiceImpl implements BookService{
	private BookDao bookDao;
	private UserDao userDao;
	
	public void setBookDao(BookDao bookDao){
		this.bookDao = bookDao;
	}
	public void setUserDao(UserDao userDao){
		this.userDao = userDao;
	}
	
	public void save(){
		System.out.println("bookService save");
		bookDao.save();
		userDao.save();
	}
}
```

```xml
<bean 
	  id="bookService" 
	  class="com.qitong.service.impl.BookServiceImpl"
>  
    <property name="bookDao" ref="bookDao"/>  
    <property name="userDao" ref="userDao"/>  
</bean>
```

### 04 构造器注入

#### **简单类型**

```java
public class BookDaoImpl implements BookDao{
	private int connectionNum;
	private String databaseName;

	public BookDaoImpl(String databaseName, int connectionNum){
		this.databaseName = databaseName;
		this.connectionNum = connectionNum;
	}
	
	public void save() {
		System.out.println("bookDao save .."+databaseName+","+connectionNum);
		bookDao.save();
	}
}
```

```xml
<bean 
	  id="bookDao" 
	  class="com.qitong.dao.impl.BookDaompl"
>
	<!-- name是形参名 -->  
	<constructor-arg name="databaseName" value="mysql"/>  
	<constructor-arg name="connectionNum" value="10"/>  
	<!-- 第二种写法 -->  
	<constructor-arg type="java.lang.String" value="mysql"/>  
	<constructor-arg type="int" value="10"/>  
	<!-- 第三种写法 -->  
	<constructor-arg index="0" value="mysql"/>  
	<constructor-arg index="1" value="10"/>  
</bean>
```

#### **引用类型**

```java
public class BookServiceImpl implements BookService{
	private BookDao bookDao;
	
	public BookServiceImpl(BookDao bookDao){
		this.bookDao = bookDao;
	}

	public void save(){
		System.out.println("bookService save")
	}
}
```

```xml
<bean 
	  id="bookService" 
	  class="com.qitong.service.impl.BookServiceImpl"
>
	<!-- name是形参名，ref是bean -->  
	<constructor-arg name="bookDao" ref="bookDao"/>  
</bean>
```

### 05 依赖注入方式选择

1. 强制依赖使用构造器进行,使用setter注入有概率不进行注入导致null对象出现；
2. 可选依赖使用setter注入进行,灵活性强；
3. Spring框架倡导使用构造器,第三方框架内部大多数采用构造器注入的形式进行数据初始化,相对严谨；
4. 如果有必要可以两者同时使用,使用构造器注入完成强制依赖的注入,使用setter注入完成可选依赖的注入；
5. 实际开发过程中还要根据实际情况分析,如果受控对象没有提供setter方法就必须使用构造器注入；
6. **自己开发的模块推荐使用setter注入**。

### 06 依赖自动装配

IoC容器根据bean所依赖的资源在容器中自动查找并注入到bean中的过程称为自动装配

自动装配方式，
#### 按类型(常用)

必须保障容器中相同的bean唯一
```java
public class BookServiceImpl implements BookService{
	private BookDao bookDao;
	
	public BookServiceImpl(BookDao bookDao){
		this.bookDao = bookDao;
	}

	public void save(){
		System.out.println("bookService save")
	}
}
```

```xml
<bean 
	  id="bookService" 
	  class="com.qitong.service.impl.BookServiceImpl"
	  autowire="byType"
/>
```

#### 按名称

必须保障容器中具有指定名称的bean
```java
public class BookServiceImpl implements BookService{
	private BookDao bookDao;
	
	public BookServiceImpl(BookDao bookDao){
		this.bookDao = bookDao;
	}

	public void save(){
		System.out.println("bookService save")
	}
}
```

```xml
<bean 
	  id="bookDao" 
	  class="com.qitong.dao.impl.BookDaompl"
>
<bean 
	  id="bookService" 
	  class="com.qitong.service.impl.BookServiceImpl" 
	  autowire="byName"
/>
```

#### 按构造方法

### 07 集合注入

```java
public class BookDaoImpl implements BookDao {  
    private int[] array;  
    private List<String> list;  
    private Set<String> set;  
    private Map<String,String> map;  
    private Properties properties;  
  
    public void setArray(int[] array) {  
        this.array = array;  
    }  
  
    public void setList(List<String> list) {  
        this.list = list;  
    }  
  
    public void setSet(Set<String> set) {  
        this.set = set;  
    }  
  
    public void setMap(Map<String, String> map) {  
        this.map = map;  
    }  
  
    public void setProperties(Properties properties) {  
        this.properties = properties;  
    }  
  
    public void save(){  
        System.out.println("bookDao save");  
        System.out.println("遍历数组"+ Arrays.toString(array));  
        System.out.println("遍历List"+list);  
        System.out.println("遍历Set"+set);  
        System.out.println("遍历Map"+map);  
        System.out.println("遍历Properties"+properties);  
    }  
}
```

```xml
<bean id="bookDao" class="com.qitong.dao.impl.BookDaoImpl">

	<property name="array">
		<array>
			<value>1</value>
			<value>2</value>
			<value>3</value>
		</array>
	</property>
	
	<property name="list">
		<list>
			<value>qitong1</value>
			<value>qitong2</value>
			<value>qitong3</value>
		</list>
	</property>
	
	<property name="set">
		<set>
			<value>qitong1</value>
			<value>qitong2</value>
			<value>qitong3</value>
		</set>
	</property>
	
	<property name="map">
		<map>
			<entty key="country" value="china"/>
			<entty key="province" value="henan"/>
			<entty key="city" value="kaifeng"/>
		</map>
	</property>
	
	<property name="properties">
		<props>
			<prop key="country">china</prop>
			<prop key="province">henan</prop>
			<prop key="city">kaifeng</prop>
		</props>
	</property>
	
</bean>
```

### 08 管理DruidDataSource

pom.xml导入druid

```xml
<dependency>  
    <groupId>com.alibaba</groupId>  
    <artifactId>druid</artifactId>  
    <version>1.1.12</version>  
</dependency>
```

配置文件中管理DruidDataSource对象

```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">  
    <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>  
    <property name="url" value="jdbc:mysql://localhost:3306/dbtest1"/>  
    <property name="username" value="root"/>  
    <property name="password" value="123456"/>  
</bean>
```

### 09 加载properties文件

1. 开启context命名空间 ^111113
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context" 
       xsi:schemaLocation="
	       http://www.springframework.org/schema/beans
	       http://www.springframework.org/schema/beans/spring-beans.xsd       
	       http://www.springframework.org/schema/context       
	       http://www.springframework.org/schema/beans/spring-context.xsd">
</beans>
```
2. 使用context命名空间加载properties文件
```xml
<beans ...>
	<!-- system-properties-mode="NEVER"不加载系统环境变量 -->
	<context:property-placeholder location="classpath*:*.properties" system-properties-mode="NEVER"/>
</beans>
```
3. 使用${}读取属性值
```xml
<beans ...>
	<context:property-placeholder location="jdbc.properties"/>
	<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">  
	    <property name="driverClassName" value="${jdbc.driver}"/>  
	    <property name="url" value="${jdbc.url}"/>  
	    <property name="username" value="${jdbc.username}"/>  
	    <property name="password" value="${jdbc.password}"/>  
	</bean>
</beans>
```

## 容器

### 01 创建容器

[[Spring#^111111|第一种方式]]

第二种方式 ^111112
```java
// 从文件系统下加载配置文件
ApplicationContext ctx = new FileSystemXmlApplicationContext("D:\\...\\applicationContext.xml");
```

### 02 获取bean

[[Spring#^111111|第一种方式]]

第二种方式 ^111112
```java
// 使用bean名称获取并指定类型
BookDao bookDao = ctx.getBean("bookDao",bookDao.class);
```

### 03 容器类层次结构

![[Pasted image 20231209112913.png|800]]

### 04 容器相关

- BeanFactory是IoC容器的顶层接口,初始化BeanFactory对象时,加载的bean延迟加载

- ApplicationContext接口是Spring容器的核心接口,初始化时bean立即加载

- ApplicationContext接口提供基础的bean操作相关方法,通过其他接口扩展其功能

- ApplicationContext接口常用初始化类
	ClassPathXmlApplicationContext
	FileSystemXmlApplicationContext

### 05 bean相关

![[Pasted image 20231209113349.png|800]]

### 06 依赖注入相关

![[Pasted image 20231209113442.png|800]]

## 注解开发

### 01 注解开发定义bean

使用@Component定义bean ^1
```java
@Component("bookDao")
public class BookDaoImpl implements BookDao{
	public void save(){
		System.out.println("bookDao save")
	}
}
// or
@Component
public class BookServiceImpl implements BookService{
	public void save(){
		System.out.println("bookService save")
	}
}
```
[[Spring#^111113|开启命名空间]]，并在核心配置文件中通过组件扫描加载bean
```xml
<context:component-scan base-package="com.qitong"/>
```

### 02 衍生注解

Spring提供@Component注解衍生的三个注解：

@Controller：用于表现层bean定义
@Service：用于业务层bean定义
@Repository：用于数据层bean定义

## 纯注解开发

Spring3.0开启了纯注解开发模式，使用Java类代替配置文件，开启了Spring快速开发赛道

### 01 纯注解开发模式

[[Spring#^1|使用@Component定义bean ]]

在com.qitong下新建config，在config下新建SpringConfig.java
```java
@Configuration
@ComponentScan({"com.qitong.service","com.qitong.dao"})
public class SpringConfig{
}
```
入口文件
```java
// 加载配置类初始化容器
public static void main(String[] args){
	ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
	BookDao bookDao = (BookDao) ctx.getBean("bookDao")
}
```

### 02 注解开发bean

使用@Scope定义bean作用范围
使用@PostConstruct、@PreDestroy定义bean生命周期
```java
@Repository
@Scope("prototype") @Scope("singleton")
public class BookDaoImpl implements BookDao{
	public void save() {
		System.out.println("bookDao save")
	}
	@PostConstruct
	public void init(){
		System.out.println("init")
	}
	@PreDestroy
	public void destroy(){
		System.out.println("destroy")
	}
}
```

### 03 注解依赖注入

使用@Autowired注解开启自动装配模式
- 自动装配基于反射设计创建对象并暴力反射对应属性为私有属性初始化数据，因此无需提供setter方法
- 自动装配建议使用无参构造方法创建对象（默认），如果不提供对应构造方法，请提供唯一的构造方法
#### 按类型装配
```java
@Service
public class BookServiceImpl implements BookServie{
	private BookDao bookDao;
	@Autowired
	public void setBookDao(BookDao bookDao){
		this.bookDao = bookDao;
	}
	public void save(){
		System.out.println("bookService save");
		bookDao.save();
	}
}
// or
@Service
public class BookServiceImpl implements BookServie{
	@Autowired
	private BookDao bookDao;
	public void save(){
		System.out.println("bookService save");
		bookDao.save();
	}
}
```

```java
@Repository
public class BookDaoImpl implements BookDao{
	public void save(){
		System.out.println("bookDao save");
	}
}
```

#### 按名称装配
```java
@Service
public class BookServiceImpl implements BookServie{
	@Autowired
	@Qualifier("bookDao1")
	private BookDao bookDao;
	public void save(){
		System.out.println("bookService save");
		bookDao.save();
	}
}
```

```java
@Repository("bookDao1")
public class BookDaoImpl1 implements BookDao{
	public void save(){
		System.out.println("bookDao1 save");
	}
}
@Repository("bookDao2")
public class BookDaoImpl2 implements BookDao{
	public void save(){
		System.out.println("bookDao2 save");
	}
}
```

#### 简单类型

简单值
```java
@Repository("bookDao")
public class BookDaoImpl1 implements BookDao{
	@Value("qitong")
	private String name;
	public void save(){
		System.out.println("bookDao1 save"+name);
	}
}
```
配置文件SpringConfig
```java
@Configuration
@ComponentScan({"com.qitong.service","com.qitong.dao"})
@PropertySource("jdbc.properties")
public class SpringConfig{
}
```
```java
@Repository("bookDao")
public class BookDaoImpl1 implements BookDao{
	@Value("${jdbc.name}")
	private String name;
	public void save(){
		System.out.println("bookDao1 save"+name);
	}
}
```

### 04 第三方bean管理

```java
@Configuration
public class SpringConfig{
	@Bean
	public DataSource dataSource(){
		DruidDataSource ds = new DruidDataSource();
		ds.setDriverClassName("com.mysql.cj.jdbc.Driver");
		ds.setUrl("jdbc:mysql://localhost:3306/dbtest1");
		ds.setUsername("root");
		ds.setPassword("123456");
		return ds;
	}
}
```
或者在config文件夹下新建JdbcConfig
```java
public class JdbcConfig{
	@Bean
	public DataSource dataSource(){
		DruidDataSource ds = new DruidDataSource();
		ds.setDriverClassName("com.mysql.cj.jdbc.Driver");
		ds.setUrl("jdbc:mysql://localhost:3306/dbtest1");
		ds.setUsername("root");
		ds.setPassword("123456");
		return ds;
	}
}
```

```java
@Configuration
@Import({Jdbcconfig.class})
public class SpringConfig{
}
```

### 05 第三方bean注入

简单类型：成员变量 ^2
```java
public class JdbcConfig{
	@Value("com.mysql.jdbc.Driver")
	private String driver;
	@Value("jdbc:mysql://localhost:3306/dbtest1")
	private String url;
	@Value"root")
	private String username;
	@Value("123456")
	private String password;
	@Bean
	public DataSource dataSource(){
		DruidDataSource ds = new DruidDataSource();
		ds.setDriverClassName(driver);
		ds.setUrl(url);
		ds.setUsername(username);
		ds.setPassword(password);
		return ds;
	}
}
```
引用类型：方法形参
```java
public class JdbcConfig{
	@Value("com.mysql.jdbc.Driver")
	private String driver;
	@Value("jdbc:mysql://localhost:3306/dbtest1")
	private String url;
	@Value"root")
	private String username;
	@Value("123456")
	private String password;
	@Bean
	public DataSource dataSource(BookDao bookDao){
		System.out.println(bookDao);
		DruidDataSource ds = new DruidDataSource();
		ds.setDriverClassName(driver);
		ds.setUrl(url);
		ds.setUsername(username);
		ds.setPassword(password);
		return ds;
	}
}
```

```java
@Configuration
@ComponentScan("com.qitong.dao")
@Import({Jdbcconfig.class})
public class SpringConfig{
}
```

### 06 XML配置对比注解配置

![[Pasted image 20231209161929.png|800]]



# 三、 Spring 整合

## 1. MyBatis程序核心对象分析

### 01 初始化sqlSessionFactory

```java
//1. 创建SqLSessionFactoryBuilder对象
SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
// 2. 加载SqLMapConfig.xmL配置文件
InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml");
// 3. 创建SqLSessionFactory对象
SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(inputStream);
```

### 02 获取连接，获取实现

```java
// 4.获取SqLSession
SqlSession sqlSession = sqlSessionFactory.openSession();
// 5. 执行SqLSession对象执行查询,获取结果User
AccountDao accountDao = sqlSession.getMapper(AccountDao.class);
```

### 03 获取数据层接口

```java
Account ac = accountDao.findById(2);
System.out.println(ac);
// 6. 释放资源
sqlSession.close();
```

![[Pasted image 20231209162823.png|800]]

## 2. Spring整合Mybatis

### 01 导入坐标

```xml
<dependencies>  
    <dependency>        
	    <groupId>org.mybatis</groupId>  
        <artifactId>mybatis</artifactId>  
        <version>3.5.5</version>  
    </dependency>    
    <dependency>        
	    <groupId>mysql</groupId>  
        <artifactId>mysql-connector-java</artifactId>  
        <version>8.0.27</version>  
    </dependency>    
    <dependency>        
	    <groupId>org.springframework</groupId>  
        <artifactId>spring-context</artifactId>  
        <version>5.2.10.RELEASE</version>  
    </dependency>    
    <dependency>        
	    <groupId>com.alibaba</groupId>  
        <artifactId>druid</artifactId>  
        <version>1.1.12</version>  
    </dependency>    
    <dependency>        
	    <groupId>org.springframework</groupId>  
        <artifactId>spring-jdbc</artifactId>  
        <version>5.2.10.RELEASE</version>  
    </dependency>    
    <dependency>        
	    <groupId>org.mybatis</groupId>  
        <artifactId>mybatis-spring</artifactId>  
        <version>1.3.0</version>  
    </dependency>
</dependencies>
```
### 02 [[Spring#^2|添加jdbcConfig文件]]

### 03 添加mybatisConfig文件

```java
public class MybatisConfig{
	@Bean
	public SqlSessionFactoryBean sqlSessionFactoryBean(DataSource,dataSourc){
		SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();
		ssfb.setTypeAliasesPackage("com.qitong.domain");
		ssfb.setDataSource(dataSourc);
		return ssfb;
	}
	@Bean
	public MapperScannerConfigurer mapperScannerConfigurer(){
		MapperScannerConfigurer msc = new MapperScannerConfigurer();
		msc.setBasePackage("com.qitong.dao");
		return msc;
	}
}
```
```java
@Configuration
@ComponentScan("com.qitong")
@PropertySource("jdbc.properties")
@Import(JdbcConfig.class,MybatisConfig.class)
public class SpringConfig{
}
```

## 3. Spring整合Junit

### 01 导入坐标

```xml
<dependencies>  
	...
    <dependency>        
	    <groupId>junit</groupId>  
        <artifactId>junit</artifactId>  
        <version>4.12</version>  
        <scope>test</scope>
    </dependency>
    <dependency>        
	    <groupId>org.springframework</groupId>  
        <artifactId>spring-test</artifactId>  
        <version>5.2.10.RELEASE</version>  
    </dependency>
    ...
</dependencies>
```

### 02 整合Junit专用的类运行器

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes=SpringConfig.class)
public class AccountServiceTest{
	@Autowired
	private AccountService accountService;

	@Test
	public void testFindById(){
		System.out.println(accountService.findById(2));
	}
}
```

# 四、AOP

## 1. AOP简介

AOP（Aspect Oriented Programming）面向切面编程，一种编程范式，指导开发者如何组织程序结构；
作用：在不惊动原始设计的基础上为其进行功能增强；

## 2. AOP核心概念

![[屏幕截图 2023-12-09 174029.png|800]]

- 连接点(JoinPoint):程序执行过程中的任意位置,粒度为执行方法、抛出异常、设置变量等
	- 在SpringAOP中，理解为方法的执行

- 切入点(Pointcut):匹配连接点的式子
	- 在SpringAOP中，一个切入点可以只描述一个具体方法,也可以匹配多个方法
		- 一个具体方法：com.itheima.dao包下的BookDao接口中的无形参无返回值的save方法
		- 匹配多个方法：所有的save方法,所有的get开头的方法，所有以Dao结尾的接口中的任意方法,所有带有一个参数的方法；
- 通知(Advice)：在切入点处执行的操作,也就是共性功能
	- 在SpringAOP中，功能最终以方法的形式呈现
- 通知类：定义通知的类
- 切面(Aspect)：描述通知与切入点的对应关系

## 3. AOP案例

案例设定：测定接口执行效率

1. 导入坐标（pom.xml）
```xml
<dependencies>
	<dependency>
		
	</dependency>
</dependencies>
```
2. 制作连接点方法（原始操作，Dao接口与实现类）

3. 制作共享功能

4. 定义切入点

## 4. 

# 五、 

## 1. 

## 2. 

## 3. 

## 4. 

# 六、 

## 1. 

## 2. 

## 3. 

## 4. 

# 七、 

## 1. 

## 2. 

## 3. 

## 4. 

# 八、 

## 1. 

## 2. 

## 3. 

## 4. 