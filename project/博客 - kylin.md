# 一、需求分析

## 现有系统调研

## 系统创新

## 项目介绍

## 项目目标

# 二、设计

## 概要设计



## 系统设计



## 技术选型

java8

mybatis2.2.2

mybatisplus3

mysql8

springcloud 2021.0.3

springcloudalibaba 2021.0.5.0

nacos 2021.0.5.0

kniferj：整合swagger2和openapi2

redis6

rabbitmq

gateway

mail

aliyunoss

nodejs 18

npm 10

vue3 + arco design ui

# 三、业务流程

## 用户流程

用户输入账号或邮箱和密码后，发送到后端，后端若验证通过，存储用户id在ThreadLocal中，
用户访问接口都会受到两个拦截器拦截，一个是验证登录拦截器，若该用户已登录，将用户id存入
一个是验证身份拦截器，根据注解判断，哪个接口是用户能访问的


## 管理员流程



## 站长流程



# 四、功能模块

## 用户

- 用户身份包括普通用户、管理员、站长；
- 用户未登录只能搜寻、查看文章和动态
- 用户登录后能发表一个文章或是一个动态；
- 用户可以进行登录注册，查看自己发布过的文章和动态，用户查看自己的历史浏览记录、关注其他用户、与其他用户聊天（次要功能）、提交工单；
- 管理员可以管理：文章发布、文章封禁、审核文章、处理工单；
- 管理员审核普通用户发送过来的文章，动态，站长管理各项事务；
- 站长可以管理：数据备份、事务管理、网站开闭；

## 文章和动态

- 用户开始撰写时可以选择文章还是动态；
- 文章支持markdown语法，可以插入图片并可以实时预览；
- 作者可以撰写、发表、修改、查看、评论、收藏、分享文章和动态。
- 读者可以查看、评论、收藏、分享、举报文章和动态。
- 作者可以决定文章和动态：是否能评论、是否私密、是否定时发布，是否修改标签；
- 文章里面可以包括链接、文字和图片等，动态包括文字、表情、图片、视频；

## 标签

- 分类标签功能，给文章和动态提供一个能进行不同方向管理和推荐；
- 工单、分组、活动、文章和动态能添加标签。
- 标签一般是一个技术栈或者热点词，如springboot、虚拟机等。

## 评论

- 评论包括一小段文字和emoji，有字数要求；
- 普通用户可以点赞、点踩、举报、评论者和博主可以删除评论；
- 活动、文章和动态都能评论。

## 工单

- 用户可以发起、删除一个工单，说明遇到了什么问题或有什么需要改进的地方；
- 管理员可以审核并回复，工单会自动关闭，工单一般不会被实际删除。

## 分组

- 用户自己创建的文件夹，给文章或动态分组，分组可以设置是否私密；
- 若加入私密分组，私密分组下的文章其他用户不可查看；
- 公开分组下的文章自动变为公开文章；

## 分类

- 管理员或站长添加的类别，用户添加的文章和动态自动根据标签添加分类；
- 分类下有相关的标签，比如后端分类下有springboot、redis等标签，前端分类下有vue、js等标签；

## 活动

- 管理员或站长能选择发布活动，活动包括主题、内容；
- 活动可以选择定时发布，用户可以选择参加该活动，并根据活动发布文章和动态；
- 在该活动下发布的文章会自动加入活动标签；
- 根据收获的浏览数和赞数评选是否获得活动奖章。

# 五、项目开发

## 前端初始化

### 创建脚手架

node -v

npm -v

vue -V

npm install -g @vue/cli

vue create kylin-blog

Vue CLI v5.0.8
- Please pick a preset: **Manually select features**
- Check the features needed for your project: **Babel, TS, Router, Vuex, Linter**
- Choose a version of Vue.js that you want to start the project with **3.x**
- Use class-style component syntax? **No**
- Use Babel alongside TypeScript (required for modern mode, auto-detected
polyfills, transpiling JSX)? **Yes**
- Use history mode for router? (Requires proper server setup for index fallback
in production) **Yes**
- Pick a linter / formatter config: **Prettier**
- Pick additional lint features: **Lint on save**
- Where do you prefer placing config for Babel, ESLint, etc.? **In dedicated**
**config files**
- Save this as a preset for future projects? **No**

### 项目框架搭建

access：定义权限验证的各类方法

assets：静态样式

components：组件文件，一般是通用的

layouts：布局文件，页面布局框架

plugins：存放一些封装的方法

router：路由管理

store：状态管理

views：页面文件，如菜单里的跳转页面

### 导入组件库

组件库：(https://arco.design/vue)

官方文档：(https://arco.design/vue/docs/start)

安装arco design
```sh
# npm
npm install --save-dev @arco-design/web-vue
# yarn
yarn add --dev @arco-design/web-vue
```

导入main.ts
```ts
import { createApp } from "vue";  
import App from "./App.vue";  
import router from "./router";  
import store from "./store";  
import ArcoVue from "@arco-design/web-vue";  
import "@arco-design/web-vue/dist/arco.css";  
  
createApp(App).use(ArcoVue).use(store).use(router).mount("#app");
```

新建一个布局文件，在app.vue中引入

选用arco design的一个layout组件

### 统一管理

axios官方文档：(https://www.axios-http.cn/docs/intro)

安装axios
```sh
npm install axios
```

导入main.ts
```ts
import { createApp } from "vue";  
import App from "./App.vue";  
import router from "./router";  
import store from "./store";  
import ArcoVue from "@arco-design/web-vue";  
import "@arco-design/web-vue/dist/arco.css";  
import "@/plugins/axios";  
import "@/access";
  
createApp(App).use(ArcoVue).use(store).use(router).mount("#app");
```

新建一个plugins/axios.ts配置文件
```ts
import axios from "axios";  
// 添加请求拦截器  
axios.interceptors.request.use(  
  function (config) {  
    // 在发送请求之前做些什么  
    return config;  
  },  
  function (error) {  
    // 对请求错误做些什么  
    return Promise.reject(error);  
  }  
);  
  
// 添加响应拦截器  
axios.interceptors.response.use(  
  function (response) {  
    // 2xx 范围内的状态码都会触发该函数。  
    // 对响应数据做点什么  
    return response;  
  },  
  function (error) {  
    // 超出 2xx 范围的状态码都会触发该函数。  
    // 对响应错误做点什么  
    return Promise.reject(error);  
  }  
);
```

### router路由管理

新建router/routers.ts文件，提取通用路由到routes.ts文件
```ts
// routes.ts
import { RouteRecordRaw } from "vue-router";  
import AdminView from "@/views/AdminView.vue";  
import UserLayout from "@/layouts/UserLayout.vue";  
import UserLoginView from "@/views/user/UserLoginView.vue";  
import UserRegisterView from "@/views/user/UserRegisterView.vue";  
import ExampleView from "@/views/ExampleView.vue";  
  
export const routes: Array<RouteRecordRaw> = [  
  {  
    path: "/user",  
    name: "用户",  
    component: UserLayout,  
    meta: {  
      hideInMenu: true,  
    },  
    children: [  
      {  
        path: "/user/login",  
        name: "用户登录",  
        component: UserLoginView,  
      },  
      {  
        path: "/user/register",  
        name: "用户注册",  
        component: UserRegisterView,  
      },  
    ],  
  },  
  {  
    path: "/",  
    name: "主页",  
    component: ExampleView,  
  },  
  {  
    path: "/hide",  
    name: "隐藏页面",  
    component: AdminView,  
    meta: {  
      hideInMenu: true,  
    },  
  },  
  {  
    path: "/admin",  
    name: "管理员",  
    component: AdminView,  
    meta: {  
      access: ACCESS_ENUM.ADMIN,  
    },  
  },  
  {  
    path: "/noAuth",  
    name: "暂无权限",  
    component: NoAuth,  
  },  
  {  
    path: "/about",  
    name: "about",  
    component: () =>  
      import(/* webpackChunkName: "about" */ "../views/AboutView.vue"),  
  },  
];
```

菜单组件读取路由，动态渲染菜单
绑定跳转事件
同步路由到菜单项

### vuex状态管理

将不同功能的模块抽取成一个文件

state：存储用户信息
actions（支持异步）：执行异步操作，并且触发mutation的更改（actions调用mutation）
mutations（尽量同步）：定义了对变量进行增删改查的方法

权限管理

能够直接以一套通用的机制，去定义哪个页面需要那些权限
在路由配置文件中定义某个路由的访问权限

控制路由的显隐

前端接口调用代码的自动生成（通用的一个代码生成插件）

前后端联调

根据权限隐藏菜单

### 全局权限管理

定义一个全局的权限验证拦截方法
创建checkAccess.ts文件

全局项目入口

## 后端初始化

### 项目框架搭建

创建一个springboot模块

依赖导入

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<project xmlns="http://maven.apache.org/POM/4.0.0"  
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">  
    <modelVersion>4.0.0</modelVersion>  
    <parent>        
	    <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-parent</artifactId>  
        <version>2.7.6</version>  
        <relativePath/>
    </parent>  
    <groupId>com.sample</groupId>  
    <artifactId>kylin-blog</artifactId>  
    <version>1.0.0</version>  
    <name>kylin-blog</name>  
    <properties>        
	    <java.version>1.8</java.version>  
    </properties>    
    <dependencies>        
	    <dependency>            
		    <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-starter-freemarker</artifactId>  
        </dependency>        
        <!-- web -->  
        <dependency>            
	        <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-starter-web</artifactId>  
        </dependency>          
        <!-- aop切面 -->  
        <dependency>            
	        <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-starter-aop</artifactId>  
        </dependency>          
        <!-- mybatis -->  
        <dependency>            
	        <groupId>org.mybatis.spring.boot</groupId>  
            <artifactId>mybatis-spring-boot-starter</artifactId>  
            <version>2.2.2</version>  
        </dependency>        
        <!-- mybatis-plus -->  
        <dependency>  
            <groupId>com.baomidou</groupId>  
            <artifactId>mybatis-plus-boot-starter</artifactId>  
            <version>3.5.2</version>  
        </dependency>        
        <!-- redis -->  
        <dependency>  
            <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-starter-data-redis</artifactId>  
        </dependency>          
        <!-- redis session -->  
        <dependency>            
	        <groupId>org.springframework.session</groupId>  
            <artifactId>spring-session-data-redis</artifactId>  
        </dependency>        
        <!-- elasticsearch-->  
        <dependency>  
            <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-starter-data-elasticsearch</artifactId>  
        </dependency>   
        <!-- knife4j接口测试 -->  
        <dependency>  
            <groupId>com.github.xiaoymin</groupId>  
            <artifactId>knife4j-openapi2-spring-boot-starter</artifactId>  
            <version>4.4.0</version>  
        </dependency>
        <!-- commons -->  
        <dependency>  
            <groupId>org.apache.commons</groupId>  
            <artifactId>commons-lang3</artifactId>  
        </dependency>        
        <!-- https://github.com/alibaba/easyexcel -->  
        <dependency>  
            <groupId>com.alibaba</groupId>  
            <artifactId>easyexcel</artifactId>  
            <version>3.1.1</version>  
        </dependency>        
        <!-- https://hutool.cn/docs/index.html#/-->  
        <dependency>  
            <groupId>cn.hutool</groupId>  
            <artifactId>hutool-all</artifactId>  
            <version>5.8.8</version>  
        </dependency>               
        <!-- devtools -->  
        <dependency>            
	        <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-devtools</artifactId>  
            <scope>runtime</scope>  
            <optional>true</optional>  
        </dependency>          
        <!-- mysql -->  
        <dependency>            
        <groupId>mysql</groupId>  
            <artifactId>mysql-connector-java</artifactId>  
            <scope>runtime</scope>  
        </dependency>        
        <dependency>            
        <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-configuration-processor</artifactId>  
            <optional>true</optional>  
        </dependency>          
        <!-- lombok -->  
        <dependency>            
        <groupId>org.projectlombok</groupId>  
            <artifactId>lombok</artifactId>  
            <optional>true</optional>  
        </dependency>          
        <!-- test -->  
        <dependency>            
        <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-starter-test</artifactId>  
            <scope>test</scope>  
        </dependency>    
    </dependencies>  
    <build>        
	    <plugins>            
		    <plugin>                
			    <groupId>org.springframework.boot</groupId>  
		        <artifactId>spring-boot-maven-plugin</artifactId>  
	            <configuration>                    
		            <excludes>                       
			            <exclude>                          
				            <groupId>org.projectlombok</groupId>  
		                    <artifactId>lombok</artifactId>  
		                </exclude>                    
		            </excludes>                
                </configuration>            
            </plugin>        
        </plugins>    
    </build>  
</project>
```

配置resources下的配置文件

controller，用于接收请求

service，业务逻辑处理

mapper，操作数据库

新建aop切面文件夹，用于处理登录或身份验证拦截

新建annotation文件夹，存放自定义注解

新建common文件夹，存放公用的类

新建model文件夹，存放实体类

新建quantify文件夹，存放定义常量之类

新建exception文件夹，存放异常处理类

新建config文件夹，存放三方工具配置类

新建utils文件夹，存放工具类

新建job文件夹，定义单次任务，定时任务，

### 数据库创建

### docker编写

## 前后端联调

编写调用后端的代码

传统模式下，每个请求都要单独编写代码

现在使用openapi自动生成

[ferdikoomen/openapi-typescript-codegen](https://github.com/ferdikoomen/openapi-typescript-codegen)

下载openapi
```shell
npm install openapi-typescript-codegen --save-dev
```

从后端引入接口
```shell
openapi --input http://localhost:8101/api/v2/api-docs --output ./generated --client axios
```

自定义请求参数
可以修改 ./generated/core/openapi.ts 的文件信息
也可以直接定义axios请求库的全局参数，比如全局请求响应拦截器

## 前端

### 核心：markdown文本编辑器、语法支持

一套通用的文本编辑器

阅读官方文档，下载编辑器主题，以及gfm（表格插件），highlight（代码高亮插件）

引入

npm i @bytemd/vue-next
npm i @bytemd/plugin-gfm @bytemd/plugin-highlight

> 若报错，在vue.config.js文件中添加require('events').EventEmitter.defaultMaxListeners = 20;

定义components/MdEditor.vue组件文件
```vue
<template>  
  <Editor :value="value" :plugins="plugins" @change="handleChange" />  
</template>  
  
<script setup lang="ts">  
import gfm from "@bytemd/plugin-gfm";  
import highlight from "@bytemd/plugin-highlight";  
import { Editor, Viewer } from "@bytemd/vue-next";  
import { ref, withDefaults, defineProps } from "vue";  
  
const plugins = [  
  gfm(),  
  highlight(),  
];  
  
// 定义组件属性类型  
interface Props {  
  value: string;  
  handleChange: (v: string) => void;  
}  
  
// 给组件指定初始值  
const props = withDefaults(defineProps<Props>(), {  
  // 初始值  
  value: () => "",  
  // 初始事件  
  handleChange: (v: string) => {  
    console.log(v);  
  },  
});  
</script>
```

使用组件
```vue
<template>  
  <div id="example">  
    <MdEditor :value="mdValue" :handle-change="onMdChange" />  
    <CodeEditor :value="codeValue" :handle-change="onCodeChange" />  
  </div>
</template>  
  
<script setup lang="ts">  
import { ref } from "vue";  
import MdEditor from "@/components/MdEditor.vue";  
import CodeEditor from "@/components/CodeEditor.vue";  
  
const mdValue = ref();  
const onMdChange = (v: string) => {  
  mdValue.value = v;  
  console.log(v);  
};  
const codeValue = ref();  
const onCodeChange = (v: string) => {  
  codeValue.value = v;  
  console.log(v);  
};  
</script>
```

### 核心：monaco-editor代码编辑器

引入
npm i monaco-editor
npm i monaco-editor-webpack-plugin

vue.config.js
```js
const { defineConfig } = require("@vue/cli-service");  
const MonacoEditorWebpackPlugin = require("monaco-editor-webpack-plugin");  
  
module.exports = defineConfig({  
  transpileDependencies: true,  
  chainWebpack(config) {  
    config.plugin("monaco").use(new MonacoEditorWebpackPlugin());  
  },  
});
```

npm install --save-dev @babel/plugin-transform-class-static-block

在babel.config.js文件添加
```js
module.exports = {  
  presets: ["@vue/cli-plugin-babel/preset"],  
  plugins: ["@babel/plugin-transform-class-static-block"],  
};
```

monaco-editor读写值时，要使用toRaw（编辑器示例）的语法来执行操作，否则会卡死



## 后端

为了防止用户按照id爬取题目，主键字段添加id的生成规则，为Assign_ID

dto：前端往后端传的数据，vo：后端给前端展示的数据，entity：数据库对应字段，


## 用户登录

### 自动登录

1. 在store\user.ts编写获取远程登录信息
2. 触发登录函数的执行，应该在一个全局位置
3. 路由拦截，全局页面入口app.vue，全局通用布局（所有页面都共享的组件）

把原有的路由拦截，权限校验逻辑放在独立的文件中
只要不引入，就不会开启权限校验

编写权限管理和自动登录逻辑

如果没登陆过，自动登录

如果用户访问的页面不需要登录，不要强制跳转到登录页

### 多套布局

在

## 微服务开发

# 六、测试与优化

## 问题解决

### 1. 放行knife4j文档接口

```java
@Configuration  
@EnableWebMvc  
@RequiredArgsConstructor  
public class WebConfig implements WebMvcConfigurer {  
  
    private final LoginInterceptor loginInterceptor;  
  
    @Override  
    public void addInterceptors(InterceptorRegistry registry) {  
        registry  
                .addInterceptor(loginInterceptor)  
                .excludePathPatterns("/api/user/login", "/api/user/register", "/swagger-ui.html", "/swagger-resources/**", "/webjars/**", "/swagger-ui/**", "/v2/api-docs/**", "/doc.html");  
  
    }  
  
    @Override  
    public void addResourceHandlers(ResourceHandlerRegistry registry) {  
  
        registry.addResourceHandler("/**").addResourceLocations("classpath:/static/");  
  
        /** 配置knife4j 显示文档 */  
        registry.addResourceHandler("doc.html")  
                .addResourceLocations("classpath:/META-INF/resources/");  
  
        /** 公共部分内容 */  
        registry.addResourceHandler("/webjars/**")  
                .addResourceLocations("classpath:/META-INF/resources/webjars/");  
    }  
	...
}
```

### 2. 解决 npm install 报错

在vue.config.js文件中添加
```js
require("events").EventEmitter.defaultMaxListeners = 0;
```

## 测试

## 优化

# 七、部署上线

## 本地部署

## docker部署

## 服务器上线

## 访问