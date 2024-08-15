# 一、Vue概念

Vue是一个用于构建用户界面的渐进式框架，[Vue.js - 渐进式 JavaScript 框架 | Vue.js (vuejs.org)](https://cn.vuejs.org/)

## 1. 构建用户界面

基于数据动态渲染页面

## 2. 渐进式

声明式渲染 -- 组件系统 -- 客户端路由（VueRouter） -- 大规模状态管理（Vuex） -- 构建工具（Webpack/Vite）

## 3. 框架

一套完整的项目解决方案，提升开发效率

## 4. 响应式

响应式：数据变化，视图自动更新

## 5. 导入Vue.js

1. 开发版本：有警告
2. 生产版本：删除了错误警告，体积更小

```html
<!-- 本地导入 -->
<script type="text/javascript" src="../js/vue.js"></script>
<!-- url导入 -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

# 二、Vue开始

## 1. 初识Vue

   1. 想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象；  
   2. root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法；  
   3. root容器里的代码被称为【Vue模板】；  
   4. Vue实例和容器是一一对应的；  
   5. 真实开发中只有一个Vue实例，并且会配合着组件一起使用；  
   6. {{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；  
   7. 一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新；

	[[VueCode#^788cef|Vue代码]]

## 2. Vue模板语法

### 01 {{}} -- 插值语法

功能：用于解析标签体内容；          
写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。  

### 02 指令语法

功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）；
举例：v-bind:href="xxx" 或  简写为 :href="xxx"，xxx同样要写js表达式，  且可以直接读取到data中的所有属性；
备注：Vue中有很多的指令，且形式都是：v-????。  

## 3. Vue数据绑定  

### 01 v-bind -- 单向绑定

数据只能从data流向页面。  

### 02 v-model -- 双向绑定

数据不仅能从data流向页面，还可以从页面流向data。  

### 03 注意事项

1. 双向绑定一般都应用在表单类元素上（如：input、select等）  
2. v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。  

## 4. el 与 data的写法

### 01 el有2种写法  

1. new Vue时候配置el属性。
2. 先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。  

### 02 data有2种写法  

1. 对象式  
2. 函数式  
3. 如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。  

### 03 注意事项

由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。

## 5. [[Vue 2023-11-07_09.excalidraw|MVVM模型]]

1. M：模型(Model) ：data中的数据  
2. V：视图(View) ：模板代码  
3. VM：视图模型(ViewModel)：Vue实例  

data中所有的属性，最后都出现在了vm身上，vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。

## 6. 数据代理

### 01 Object.defineProperty方法

```javaScript
Object.defineProperty(person,'age',{  
   // value:18,  
   // enumerable:true, //控制属性是否可以枚举，默认值是false  
   // writable:true, //控制属性是否可以被修改，默认值是false  
   // configurable:true //控制属性是否可以被删除，默认值是false  
  
   //当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值  
   get(){  
      console.log('有人读取age属性了')  
      return number  
   },  
  
   //当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值  
   set(value){  
      console.log('有人修改了age属性，且值是',value)  
      number = value  
   }  
  
})
```

### 02 数据代理

通过一个对象代理对另一个对象中属性的操作（读/写）

### 03 Vue中的数据代理

1. Vue中的数据代理：通过vm对象来代理data对象中属性的操作（读/写）  
2. Vue中数据代理的好处：更加方便的操作data中的数据  
3. 基本原理：  
	- 通过Object.defineProperty()把data对象中所有属性添加到vm；
	- 为每一个添加到vm上的属性，都指定一个getter/setter；
	- 在getter/setter内部去操作（读/写）data中对应的属性。

## 7. 事件处理

1.使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；  
2.事件的回调需要配置在methods对象中，最终会在vm上；  
3.methods中配置的函数，不要用箭头函数！否则this就不是vm了；  
4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；  
5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；

### 02 Vue中的事件修饰符

1. prevent：阻止默认事件（常用）；  
2. stop：阻止事件冒泡（常用）；  
3. once：事件只触发一次（常用）；  
4. capture：使用事件的捕获模式；  
5. self：只有event.target是当前操作的元素时才触发事件；  
6. passive：事件的默认行为立即执行，无需等待事件回调执行完毕；

### 03 键盘事件

1. Vue中常用的按键别名：  
   - 回车 => enter         
   - 删除 => delete (捕获“删除”和“退格”键)  
   - 退出 => esc         
   - 空格 => space         
   - 换行 => tab (特殊，必须配合keydown去使用)  
   - 上 => up         下 => down         左 => left         右 => right  
2. Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为- kebab-case（短横线命名）  
3. 系统修饰键（用法特殊）：ctrl、alt、shift、meta  
   - 配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。  
   - 配合keydown使用：正常触发事件。  
  
4. 也可以使用keyCode去指定具体的按键（不推荐）  
  
5. Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名

## 8. 计算属性 computed

### 01 定义

要用的属性不存在，要通过已有属性计算得来。  

### 02 原理

底层借助了Objcet.defineproperty方法提供的getter和setter。  

### 03 get 执行时机

1. 初次读取时会执行一次。  
2. 当依赖的数据发生改变时会被再次调用。  

### 04 set 调用时机

给计算属性一个修改的途径，当计算属性被修改时调用set

### 05 注意事项  

1. 计算属性最终会出现在vm上，直接读取使用即可；
2. 如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变；
3. 与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。  

## 9. 监视属性 watch

### 01 监视中

1. 当被监视的属性变化时, 回调函数自动调用, 进行相关操作  
2. 监视的属性必须存在，才能进行监视！！  
3. 监视的两种写法：  
1).new Vue时传入watch配置  
2).通过vm.$watch监视

### 02 深度监视

1. Vue中的watch默认不监测对象内部值的改变（一层）。  
2. 配置deep:true可以监测对象内部值改变（多层）。  
	(1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！  
    (2).使用watch时根据数据的具体结构，决定是否采用深度监视。
      
computed和watch之间的区别：  
1. computed能完成的功能，watch都可以完成。  
2. watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。  
3. 两个重要的小原则：  
   - 所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。  
   - 所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，这样this的指向才是vm 或 组件实例对象。  

## 10. 绑定样式

### 01 class样式  

1. 写法
```html
<div :class="xxx"></div> 
```
2. xxx可以是字符串、对象、数组。  
3. 字符串写法适用于：类名不确定，要动态获取。 
4. 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定。
5. 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。  

### 02 style样式 

1. 写法
   ```html
<div class="xxx" :style="{fontSize: xxx}"></div> 
   ```
2. 其中xxx是动态值。  
3. 对象写法
4. 数组写法

## 11. 条件渲染

### 01 v-if  

**写法**

1. v-if="表达式"   
2. v-else-if="表达式"  
3. v-else="表达式"  

**特点：不展示的DOM元素直接被移除。**
**适用于：切换频率较低的场景;**
注意：v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。  
  
### 02 v-show

**写法**

v-show="表达式"  

**特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉 。
**适用于：切换频率较高的场景。  

### 03 注意事项

使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。

## 12. 列表渲染

### 01 v-for指令:  

**写法**

v-for="(item, index) in xxx" :key="yyy"  

1. 用于展示列表数据  
2. 可遍历：数组、对象、字符串、指定次数

### 02 key作用与原理

**虚拟DOM中key的作用**

- key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】,   随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：  

**对比规则**

- 旧虚拟DOM中找到了与新虚拟DOM相同的key：  
  1. 若虚拟DOM中内容没变, 直接使用之前的真实DOM
  2. 若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
- 旧虚拟DOM中未找到与新虚拟DOM相同的key
- 创建新的真实DOM，随后渲染到到页面。  

**用index作为key可能会引发的问题** 

- 对数据进行：逆序添加、逆序删除等破坏顺序操作:  
- 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。  
- 如果结构中还包含输入类的DOM：  会产生错误DOM更新 ==> 界面有问题。 

**开发中如何选择key**

- 最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。  
- 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，  使用index作为key是没有问题的。

### 03 列表过滤

### 04 列表排序

### 05 **在Vue操作元素所用方法**

1. 使用这些API：set()、push()、pop()、shift()、unshift()、splice()、sort()、reverse()  
2. Vue.set() 或 vm.\$set()   特别注意：Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！

### 06 Vue监测数据改变的原理

**Vue会监视data中所有层次的数据**
  
**如何监测对象中的数据**

通过setter实现监视，且要在new Vue时就传入要监测的数据。  
1. 对象中后追加的属性，Vue默认不做响应式处理  
2. 如需给后添加的属性做响应式，请使用如下API：  
   Vue.set(target，propertyName/index，value) 或                               vm.$set(target，propertyName/index，value)  
  
**如何监测数组中的数据**

通过包裹数组更新元素的方法实现，本质就是做了两件事：  
1. 调用原生对应的方法对数组进行更新。  
2. 重新解析模板，进而更新页面。  

## 13. 收集表单数据

### 01 文本框 -- input

```html
<input type="text" v-model.trim="user.name"/>
```

v-model收集的是value值，用户输入的就是value值。  

### 02 单选框 -- input

```html
<input type="radio" v-model="user.sex" value="male"/>
```

则v-model收集的是value值，且要给标签配置value值。  

### 03 复选框 -- input

```html
<input type="checkbox" v-model="user.hobby" value="study"/>
```

配置input的value属性:  
v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值） 
v-model的初始值是数组，那么收集的的就是value组成的数组  

### 04 阻止表单跳转

给表单绑定 @submit.prevent="demo" 方法

### 05 v-model的三个修饰符

lazy：失去焦点再收集数据
number：输入字符串转为有效的数字 
trim：过滤输入首尾空格

## 14. 过滤器 filter

### 01 定义

对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。  

### 02 注册过滤器

1. 全局过滤器：Vue.filter(name,callback)
2. 局部过滤器：new Vue{filters:{}} 

### 03 使用过滤器

实现：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名" 
传参：{{xxx | 过滤器名('YY_MM_DD')}}
连续：{{xxx | 过滤器名 | 过滤器名}}

### 04 注意事项

1. 过滤器也可以接收额外参数、多个过滤器也可以串联  
2. 并没有改变原本的数据, 是产生新的对应的数据

## 15. 内置指令

### 01 v-text

1. 作用：向其所在的节点中渲染文本内容。  
2. 与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。

### 02 v-html

1. 作用：向指定节点中渲染包含html结构的内容。  
2. 与插值语法的区别：  
   - v-html会替换掉节点中所有的内容，{{xx}}则不会。  
   - v-html可以识别html结构。  
3. 注意：v-html有安全性问题
   - 在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。  
   - 一定要在可信的内容上使用v-html，永不要用在用户提交的内容上使用

### 03 v-cloak

1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。  
2. 使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。

### 04 v-once

1. v-once所在节点在初次动态渲染后，就视为静态内容了。 
2. 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

### 05 v-pre

1. 跳过其所在节点的编译过程。  
2. 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。

## 16. 自定义指令 directives

### 01 局部指令 -- 函数式

big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。

element指的是v-big所在的元素，binding指的是v-big的值
```html
<span v-big="n"></span>
<script>
new Vue({  
    directives{
	   指令名:回调函数
	   big(element, binding){
		   console.log('big',this) //注意此处的this是window
		   element.innerText = binding.value * 10
	   }
	}  
})
</script>
```

### 02 局部指令 -- 对象式

配置对象中常用的3个回调：  

1. bind：指令与元素成功绑定时调用。  
2. inserted：指令所在元素被插入页面时调用。  
3. update：指令所在模板结构被重新解析时调用。

```html
<input type="text" v-fbind:value="n">
<script>
new Vue({                 
    directives:{
	    指令名:配置对象
	    fbind:{
		    //指令与元素成功绑定时（一开始）  
			bind(element,binding){  
			   element.value = binding.value  
			},  
			//指令所在元素被插入页面时  
			inserted(element,binding){  
			   element.focus()  
			},  
			//指令所在的模板被重新解析时  
			update(element,binding){  
			   element.value = binding.value  
			}
	    }
	}     
})
</script>
```

### 03 全局指令 -- 对象式

```html
<input type="text" v-fbind:value="n">
<script>
Vue.directive(指令名,配置对象) 

Vue.directive('fbind',{  
   bind(element,binding){      
	   element.value = binding.value  
	},
   inserted(element,binding){
	   element.focus()  
	}, 
   update(element,binding){
	   element.value = binding.value   
	}})
</script>
```


# 三、Vue进阶

## 1. 生命周期

### 01 什么是生命周期

1. 又名：生命周期回调函数、生命周期函数、生命周期钩子。  
2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。  
3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。  
4. 生命周期函数中的 this 指向是 vm 或 组件实例对象。

### 02 生命流程
 
![[生命周期.png]]
### 03 生命周期钩子

```javascript
new Vue({
	data:{
		
	}
	beforeCreate() {  
	   console.log('beforeCreate')  
	},  
	created() {  
	   console.log('created')  
	},  
	beforeMount() {  
	   console.log('beforeMount')  
	},  
	mounted() {  
	   console.log('mounted')  
	},  
	beforeUpdate() {  
	   console.log('beforeUpdate')  
	},  
	updated() {  
	   console.log('updated')  
	},  
	beforeDestroy() {  
	   console.log('beforeDestroy')  
	},  
	destroyed() {  
	   console.log('destroyed')  
	}
})
```

### 04 注意事项

**常用的生命周期钩子**

1. mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。  
2. beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。  
  
**关于销毁Vue实例**

1. 销毁后借助Vue开发者工具看不到任何信息。  
2. 销毁后自定义事件会失效，但原生DOM事件依然有效。  
3. 一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。

## 2. 非单组件

组件就是实现应用中**局部**功能**代码**（html、css、js）和**资源**（图片、音频、字体...）的集合；

非单文件组件，一个文件中包含n个组件

### 01 Vue中使用组件的三大步骤

1. 定义组件(创建组件)  
2. 注册组件  
3. 使用组件(写组件标签)  
  
### 02 定义组件

使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别； 

区别如下：

1. **el不要写**，因为最终所有的组件都要经过一个vm管理，由vm中的el决定服务哪个容器。 
2. **data必须写成函数**，避免组件被复用时，数据存在引用关系。 
3. 使用template可以配置组件结构。 
  
### 03 注册组件

1. 局部注册：靠new Vue的时候传入components选项
2. 全局注册：靠Vue.component('组件名',组件)  
  
### 04 编写组件标签

`<组件名></组件名>`

`<组件名/>` 

### 05 组件名规范

**一个单词组成**

第一种写法(首字母小写)：school  
第二种写法(首字母大写)：School  

**多个单词组成**

第一种写法(kebab-case命名)：my-school  
第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持) 

### 06 组件嵌套

```javascript
const school = Vue.extend({  
   name:'school', 
   template:`  
      <div>         
	     <h2>学校名称：{{name}}</h2>   
         <h2>学校地址：{{address}}</h2>    
         <student></student>  
      </div>   `,  
   data(){  
      return {  
         name:'尚硅谷',  
         address:'北京'  
      }  
   },  
   //注册组件（局部）  
   components:{  
      student: student
   }  
})
```

### 注意事项

**组件名尽可能回避HTML中已有的元素名称**
例如：h2、H2都不行，可以使用name配置项指定组件在开发者工具中呈现的名字。

不用使用脚手架时，<组件名/>会导致后续组件不能渲染。

**简写方式**
const school = Vue.extend(options) 可简写为：const school = options

## 3. VueComponent

### 01 组件本质

组件本质是一个名为**VueComponent的构造函数**，且不是程序员定义的，是Vue.extend生成的。  

### 02 实现过程

我们只需要写`<school/>`或`<school></school>`，Vue解析时会帮我们创建school组件的实例对象，  即Vue帮我们执行的：new VueComponent(options)。  
  
特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent
  
### 03 关于this指向：  

**组件配置中**
data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。  

**new Vue(options)配置中**
data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。 

### 04 组件实例对象
  
VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。  Vue的实例对象，以后简称vm。

### 05 内置关系

**VueComponent.prototype.__proto__ === Vue.prototype**

让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。

## 4. 单组件

单文件组件，一个文件中包含1个组件，这个文件以 .vue 为后缀

### 01 组成标签

1. `<template></template>` ：
2. `<script></script>` ：
3. `<style></style>` ：

### 02 定义组件

`export default {components:{Student,School}}

### 03 引入并注册组件

`import App from './App.vue'

`components:{App}`

### 04 使用组件

``template:`<App></App>` ``

## 5. Vue2工程创建

[Vue脚手架](https://cli.vuejs.org/zh/#%E8%B5%B7%E6%AD%A5)是Vue官方提供的标准化开发工具（开发平台）

### 01 配置步骤

1. 下载[Node.js](https://nodejs.org/en)并配置环境变量
2. 打开cmd，全局配置[vue-cli](https://cli.vuejs.org/zh/guide/)  `npm install -g @vue/cli`
3. 在指定目录下创建项目 `vue create 项目名`

### 02 Vue脚手架结构

- **node_modules**：
- **public**：
	1. favicon：网页图片
	2. index.html：主页面
- **src**
	1. assets：存放静态资源
	2. components：存放组件
	3. App.vue：汇总所有组件
	4. main.js：入口文件
- .gitignore：git版本管制忽略的配置
- **babel.config.json**：babel的配置文件
- **package-lock.json**：包版本控制文件
- **package.json**：应用包配置文件
- README.md： 应用描述文件

### 03 render函数

作用是创建具体的元素。在vue中将组件呈现到页面上

```javascript
new Vue({
	el: '#app',
	render(createElement){
		return createElemnt('h1', '你好')
	}
	render:e => e('h1', '你好')
})
```

```javascript
new Vue({
	render:e => e(App)
})
```

### 04 修改默认配置

最好不修改的有public文件夹下的文件、scr文件夹、main.js

显示默认配置：在项目下打开cmd输入`vue inspect > output.js`，出现output.js文件，打开查看

**修改默认配置：在项目下添加文件vue.config.js，可以对脚手架进行个性化定制[具体配置](https://cli.vuejs.org/zh/config)**

### 05 ref 属性

**功能**
被用来给元素或子组件注册引用信息（id的替代者）

**获取信息**
应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）  

**使用方式**
1. 打标识：`<h1 ref="xxx">.....</h1>` 或 `<School ref="xxx"></School>`
2. 获取：`this.$refs.xxx`

### 06 props 配置

**功能**
让组件接收外部传过来的数据  
  
**传递数据**
```<Demo name="xxx" sex='xxx' .../>```  
  
**接收数据**
  
1. 第一种方式（只接收）：```props:['name', 'sex', ...] ```  
2. 第二种方式（限制类型）：```props:{name:String}```  
3. 第三种方式（限制类型、限制必要性、指定默认值）：  
```javascript
props:{  
    name:{
	    type:String, // 属性的类型  
	    required:true, // 属性是否必传  
	    default:'老王' // 默认值  
    }
}  
```  

**注意事项**
props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。

### 07 mixin 混入

**功能**
可以把多个组件共用的配置提取成一个混入对象  
  
**使用方式**
1. 定义混合：  
```js
    export mixin = {  
        data(){...},
        methods:{...}
        ...
    }  
```  
2. 使用混入：  
  
全局混入：Vue.mixin(xxx)
局部混入：mixins:['xxx']

### 08 插件

**功能**
用于增强Vue  

**本质**
包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。  
  
**定义插件**
  
```js  
对象.install = function (Vue, options) {  
    // 1. 添加全局过滤器  
    Vue.filter(...)  
    // 2. 添加全局指令  
    Vue.directive(...)  
    // 3. 配置全局混入(合)  
    Vue.mixin(...)    // 4. 添加实例方法  
    Vue.prototype.$myMethod = function () {...}  
    Vue.prototype.$myProperty = xxxx    
}  
```  

**使用插件**

`Vue.use()`

### 09 scoped

**作用**
让样式在局部生效，防止冲突。  

**写法**
`<style scoped>`
  
## 6. 组件化编码流程
  
**拆分静态组件**
组件要按照功能点拆分，命名不要与html元素冲突。  
  
**实现动态组件**
考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：  
1. 一个组件在用：放在组件自身即可。  
2. 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。  

**实现交互**
从绑定事件开始。

**props适用**
  
父组件 ==> 子组件 通信 
子组件 ==> 父组件 通信（要求父组件先给子组件一个函数）  
  
使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！ props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。

## 7. 浏览器本地存储

webStorage  
  
**存储内容大小一般支持5MB左右（不同浏览器可能还不一样）  **
  
**浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制**
  
**相关API**
  
1. `xxxxxStorage.setItem('key', 'value');`
 该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。  

2. `xxxxxStorage.getItem('person');`
该方法接受一个键名作为参数，返回键名对应的值。  

3. `xxxxxStorage.removeItem('key');`
该方法接受一个键名作为参数，并把该键名从存储中删除。  

4. ` xxxxxStorage.clear()`
该方法会清空存储中的所有数据。  
  
**注意事项**  
  
1. SessionStorage存储的内容会随着浏览器窗口关闭而消失。  
2. LocalStorage存储的内容，需要手动清除才会消失。  
3. ```xxxxxStorage.getItem(xxx)```如果xxx对应的value获取不到，那么getItem的返回值是null。  
4. ```JSON.parse(null)```的结果依然是null。

## 8. 组件自定义事件

一种组件间通信的方式，适用于：子组件 ==> 父组件
  
### 01 使用场景

A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。  
  
### 02 绑定自定义事件：  
  
第一种方式，在父组件中：
`<子组件名 @atguigu="test"/>`  或 `<子组件名 v-on:atguigu="test"/>`
  
第二种方式，在父组件中：  
```js  
<子组件名 ref="xxx"/>
    ......        
mounted(){
	this.$refs.xxx.$on('atguigu',this.xxx)
}  
```  

### 03 触发自定义事件

在子组件中 `this.$emit('atguigu',发送数据)`

若想让自定义事件只能触发一次，可以使用`once`修饰符，或`$once`方法。  

### 04 解绑自定义事件

解绑一个自定义事件：`this.$off('atguigu')`
解绑多个自定义事件：`this.$off(['atguigu','xxx'])`
解绑所有自定义事件：`this.$off()`

### 05 注意事项

组件上也可以绑定原生DOM事件，需要使用`native`修饰符。`@click.native='xxx'`
  
通过```this.$refs.xxx.$on('atguigu',回调)```绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题！

## 9. 事件总线

任意组件间通信

### 01 安装事件总线
  
```js  
new Vue({  
	......       
	beforeCreate() {          
       Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm 
    },
    ......   
})   
```  

### 02 使用事件总线：  
  
1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span> 
```js  
methods(){  
    demo(data){......}      
}      
......      
mounted() {        
	this.$bus.$on('xxxx',this.demo)     
}  
```  
2. 提供数据：```this.$bus.$emit('xxxx',数据)```  
3. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。

## 10. 消息订阅与发布（pubsub）  
  
1.   一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。  
  
2. 使用步骤：  
  
   1. 安装pubsub：```npm i pubsub-js```  
  
   2. 引入: ```import pubsub from 'pubsub-js'```  
  
   3. 接收数据：`pubsub.subscribe('xxx',数据)`，A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>  
  
```js  
methods(){  
    demo(data){......}      
}      
......      
mounted() {        
	this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息  
}  
```  
   4. 提供数据：`pubsub.publish('xxx',数据)`
  
   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>

## 11. Vue封装的过度与动画  
  
### 01 作用

在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。  

### 02 写法

准备好样式：  
  
**元素进入的样式**

1. v-enter：进入的起点  
2. v-enter-active：进入过程中  
3. v-enter-to：进入的终点  

**元素离开的样式**

1. v-leave：离开的起点  
2. v-leave-active：离开过程中  
3. v-leave-to：离开的终点  
  
使用```<transition>```包裹要过度的元素，并配置name属性：  

```vue  
<transition name="hello">  
	<h1 v-show="isShow">你好啊！</h1>  
</transition>
```

使用name-enter-active

```css
.hello-enter-active {
	transform: translateX();
}
```

### 03 注意事项

若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。

```vue  
<transition-group name="hello">  
	<h1 v-show="isShow" key="1">你好啊！</h1>  
	<h1 v-show="isShow" key="1">你好啊！</h1>  
</transition>
```

## 12. vue脚手架配置代理

编写vue.config.js配置具体代理规则：  
  
```js  
module.exports = {   
	devServer: {  
		proxy: {  
			'/api1': {
		        target: 'http://localhost:5000',
		        changeOrigin: true,  
		        pathRewrite: {'^/api1': ''}  
		    },      
		    '/api2': {
		        target: 'http://localhost:5001',
		        changeOrigin: true,  
		        pathRewrite: {'^/api2': ''} 
		    }    
		}  
	}
}
```

### /api1

匹配所有以 '/api1'开头的请求路径，意思是如果前缀为/api1则发送请求

### target

代理目标的基础路径

### pathRewrite

把发送给localhost:5050的地址去掉前缀api1

### changeOrigin

changeOrigin设置为true时，服务器收到的请求头中的host为localhost:5000  
changeOrigin设置为false时，服务器收到的请求头中的host为localhost:8080  
changeOrigin默认值为true  

## 13. 插槽

### 01 作用

让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于父组件 ===> 子组件。
  
分类：默认插槽、具名插槽、作用域插槽  

### 02 默认插槽

父组件中
```vue
<Category>  
    <div>html结构1</div>  
</Category> 
```
子组件中
```vue
<template>  
    <div>  
	    <!-- 定义插槽 -->  
        <slot>写在父组件中的那些html结构</slot>  
    </div>  
</template>
```

### 03 具名插槽

父组件中
```vue 
<Category>  
	<!-- 第一种写法 -->  
	<template slot="center">
		<div>html结构1</div>  
	</template>
	
	<!-- 第二种写法 --> 
	<template v-slot:footer>  
		<div>html结构2</div>  
	</template>
</Category>   

```
子组件中
```vue 
<template>  
	<div>
	<!-- 定义插槽 -->
		<slot name="center">插槽默认内容...</slot>  
		<slot name="footer">插槽默认内容...</slot>  
	</div>
</template>  
   ```

### 04 作用域插槽

**数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。**
（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）  

父组件中
```vue
<Category>  
	<template scope="scopeData">      
		<!-- 生成的是ul列表 -->      
		<ul>         
			<li v-for="g in scopeData.games" :key="g">{{g}}</li>
		</ul>   
	</template>
</Category>  
  
<Category> 
	<template slot-scope="scopeData">      
		<!-- 生成的是h4标题 -->
		<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
	</template>
</Category>
```
子组件中
```html
<template>  
    <div>  
        <slot :games="games"></slot>  
    </div>  
</template>
<script>  
    export default {  
        name:'Category',  
        props:['title'],  
        //数据在子组件自身  
        data() {  
            return {  
                games:['红色警戒','穿越火线','劲舞团','超级玛丽']  
            }  
        },  
    }  
</script>
```

## 14. vuex

专门在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（），也是一种组件间通信的方式，且适用于任意组件间通信

### vuex工作原理

### 搭建vuex环境

1. 下载vuex，npm i vuex@3
2. src下新建stroe文件夹并创建index.js
```js
// index.js
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

const actions = {
	oopp(context,value){
		if(...){
			context.commit('Add',value)
		}
	}
}
const mutations = {
	Add(state,value){
		state.unshift(value)
	}
}
const state = {
	
}

const store = new Vuex.Store({
	actions:actions,
	mutations,
	state
})

export default store
```
3. 在main.js里引入index.js
```js
// main.js
import store from './store'

new Vue({
	...
	store,
	...
})
```

### 读取vuex中数据

```$store.state.sum```  
  
### 修改vuex中数据

`$store.dispatch('action中的方法名',数据)`
```$store.commit('mutations中的方法名',数据)```

### getters的使用  
  
1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。  
2. 在```store.js```中追加```getters```配置  
```js  
...
const state = {...}
const getters = {  
    bigSum(state){          
	    return state.sum * 10=
	}   
}      
//创建并暴露store  
export default new Vuex.Store({
	...  
	getters   
})  
```  
3. 组件中读取数据：```$store.getters.bigSum```  
  
### 四个map方法的使用 

首先引入map方法
  
`import {mapState,mapGetters,mapActions,mapMutation} from 'vuex'`
  
1. <strong>mapState方法：</strong>用于映射```state```中的数据为计算属性  
```js  
computed: {  
    //借助mapState生成计算属性：sum、school、subject（对象写法）  
    ...mapState({sum:'sum',school:'school',subject:'subject'}),  
     //借助mapState生成计算属性：sum、school、subject（数组写法）  
    ...mapState(['sum','school','subject']),  
},
```  
2. <strong>mapGetters方法：</strong>用于映射```getters```中的数据为计算属性  
```js  
computed: {  
	//借助mapGetters生成计算属性：bigSum（对象写法）  
    ...mapGetters({bigSum:'bigSum'}),  
    //借助mapGetters生成计算属性：bigSum（数组写法）  
    ...mapGetters(['bigSum'])  
},  
```  
3. <strong>mapActions方法：</strong>用于生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数  
```js  
methods:{  
    //靠mapActions生成：incrementOdd、incrementWait（对象形式）  
    ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})  
    //靠mapActions生成：incrementOdd、incrementWait（数组形式）  
    ...mapActions(['jiaOdd','jiaWait'])  
}  
```  
4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数  
```js  
methods:{  
    //靠mapActions生成：increment、decrement（对象形式）  
    ...mapMutations({increment:'JIA',decrement:'JIAN'}),  
    //靠mapMutations生成：JIA、JIAN（对象形式）  
    ...mapMutations(['JIA','JIAN']),  
}  
```  

>备注：mapActions与mapMutations使用时，若要传递参数，需要在模板中绑定事件时传递好参数，否则参数是事件对象

### vuex模块化 & namespace

目的：让代码更好维护，让多种数据分类更加明确。  

修改 store.js
```js
const countAbout = {
  namespaced:true,//开启命名空间  
  state:{x:1},  
  mutations: { ... },  
  actions: { ... },  
  getters: {  
    bigSum(state){  
       return state.sum * 10  
    }  
  }  
}
const personAbout = {  
  namespaced:true,//开启命名空间  
  state:{ ... },  
  mutations: { ... },  
  actions: { ... }  
}  
const store = new Vuex.Store({  
  modules: {  
    countAbout,  
    personAbout  
  }  
}) 
```

开启命名空间后，组件中读取state数据：  
```js  
//方式一：自己直接读取  
this.$store.state.personAbout.list
//方式二：借助mapState读取：  
...mapState('countAbout',['sum','school','subject']),  
```  
开启命名空间后，组件中读取getters数据：    
   ```js  
//方式一：自己直接读取  
this.$store.getters['personAbout/firstPersonName']  
//方式二：借助mapGetters读取：  
...mapGetters('countAbout',['bigSum'])  
```
开启命名空间后，组件中调用dispatch  
```js  
//方式一：自己直接dispatch  
this.$store.dispatch('personAbout/addPersonWang',person)   //方式二：借助mapActions：  
...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})  
```
开启命名空间后，组件中调用commit  
```js  
//方式一：自己直接commit  
this.$store.commit('personAbout/ADD_PERSON',person)   
//方式二：借助mapMutations：  
...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
```

# 四、Vue路由 route

## 1. 路由的定义

路由 route 就是一组 key-value 的对应关系，key为路径，value可能是function 或 component，多个路由，需要经过路由器 router 的管理

key1 + value1 => 路由
key2 + value2 => 路由
key3 + value3 => 路由
key4 + value4 => 路由
......

多应用于SPA（Single Page web Application）单页面应用，点击页面中的导航不会引起页面的刷新，只会做页面的局部更新

## 2. vue-router 路由的使用

vue的一个插件库，专门用于实现SPA应用

### 01 vue-router 配置

1. 安装vue-router：vue2：npm i vue-router@3
2. 创建pages文件夹，放置路由组件
3. 创建router文件夹，添加路由器：index.js文件 ^111112
```js
import VueRouter from 'vue-router'
import About from '../pages/About'
import Home from '../pagesHome'
...

const router = new VueRouter({
	routes:[
		{
			path:'/about',
			component: About
		},{
			path:'/home',
			component: Home
		},
		...
	]
})
export default router
```
4. main.js 中配置
```js
import VueRouter from 'vue-router'
import router from './router'

Vue.use(VueRouter)
new Vue({
	el:'#app',
	render: h => h(App),
	router: router
})
```
5. App.vue中配置 ^111111
```vue
<!--实现切换（active-class可配置高亮样式）-->
<div>
	<router-link class="list" active-class="active" to="/about">About</router-link>
	<router-link class="list" active-class="active" to="/home">Home</router-link>
</div>
 <!--组件展示的位置-->
<div>
	<router-view></router-view>
</div>
```

### 02 注意事项

1. 路由组件通常存放在`pages`文件夹，一般组件通常存放在`components`文件夹。  
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。  
3. 每个组件都有自己的`$route`属性，里面存储着自己的路由信息。  
4. 整个应用只有一个router，可以通过组件的`$router`属性获取到。

## 3. 嵌套路由

配置路由规则，使用children配置项

```js  
routes:[ 
   {  
      path:'/about',  
      component:About,  
   },{  
      path:'/home',  
      component:Home,  
      children:[ //通过children配置子级路由  
         {  
            path:'news', //此处一定不要写：/news  
            component:News  
         },  
         {  
            path:'message',//此处一定不要写：/message  
            component:Message  
         }  
      ]  
   }  
]  
```

跳转（要写完整路径）
```vue  
<router-link to="/home/news">News</router-link>
<router-link to="/home/message">Message</router-link>
```

## 4. 路由传参 query

### 01 传递参数

跳转并携带query参数，to的字符串写法
```vue
<!--第一种写法-->
<router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>
<!--第二种写法-->
<router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">跳转</router-link>
```

跳转并携带query参数，to的对象写法
```vue
<router-link 
	:to="{
		path:'/home/message/detail',
		query:{
			id: m.id,
			title: m.title
		}
	}"
>
跳转
</router-link>  
```

### 02 接收参数
```js  
$route.query.id
$route.query.title
```

## 5. 路由命名 name

作用是简化路由的跳转
通过name配置
```js  
routes:[ 
	{  
	  name:'home',
      path:'/home',  
      component:Home,  
      children:[ //通过children配置子级路由  
         {  
			name:'news',
            path:'news',  
            component:News  
         }
      ]  
   }  
]  
```

```vue  
<!--简化前，需要写完整的路径 -->  
<router-link to="/home/news">跳转</router-link>  
<!--简化后，直接通过名字跳转 -->  
<router-link :to="{name:'news'}">跳转</router-link>  
<!--简化写法配合传递参数 -->  
<router-link   
   :to="{  
      name:'news',  
      query:{  
         id:666,  
         title:'你好'  
      }  
   }"  
>跳转</router-link>
>
```

## 6. 路由中的 params参数

配置路由，使用占位符声明接收params参数 
```js  
{  
   path:'/home',  
   component:Home,  
   children:[  
      {
         path:'news',  
         component:News  
      },{  
	     path: 'message',
         component:Message,  
         children:[  
            {  
               name:'xiangqing',  
               path:'detail/:id/:title', //使用占位符声明接收params参数  
               component:Detail  
            }  
         ]  
      }  
   ]  
}  
```  
传递参数  
```vue  
<!-- 跳转并携带params参数，to的字符串写法 -->  
<router-link :to="/home/message/detail/666/你好">跳转</router-link>  
              
<!-- 跳转并携带params参数，to的对象写法 -->  
<router-link   
   :to="{  
      name:'xiangqing',  
      params:{  
	    id:666,
	    title:'你好'  
      }  
   }"  
>跳转</router-link>  
```

**特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！  **

接收参数  
```js  
$route.params.id
$route.params.title 
```

## 7. 路由中的props 配置

作用就是让路由组件更方便的收到参数

### 01 第一种写法：props值为对象

该对象中所有的key-value的组合最终都会通过props传给Detail组件  
```js  
{  
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,  
	props:{a:900}
}
```

### 02 第二种写法：props值为布尔值

布尔值为true，则把路由收到的所有params参数通过props传给Detail组件 
```js  
{  
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,  
    props:true
}  
```

### 03 第三种写法：props值为函数

该函数返回的对象中每一组key-value都会通过props传给Detail组件  
```js  
{  
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,
	props($route){      
		return {         
			id:$route.query.id,
			title:$route.query.title      
		}   
	}
}  
```

## 8. 路由中的replace属性

replace属性
1. 作用：控制路由跳转时操作浏览器历史记录的模式；
2. 浏览器的历史记录有两种写入方式：分别为`push`和`replace`，`push`是追加历史记录，`replace`是替换当前记录。路由跳转时候默认为`push` ；
3. 如何开启```replace```模式：`<router-link replace>News</router-link>`
4. 浏览器中的前进后退依赖的是历史记录，执行的是push属性，压栈操作，默认将最后一个进栈的页面作为指针所指的方向。

## 9. 编程式路由导航

作用：不借助[[VueNote#^111111|router-link]]实现路由跳转，让路由跳转更加灵活  

给元素绑定事件，然后在methods方法的事件中实现 `this.$router.xxx` ，将[[VueNote#^111111|router-link]]中to中的所有属性加入
```js  
//$router的两个API 
this.$router.push({       
	name:'xiangqing',          
	params:{             
		id:xxx,             
		title:xxx          
	}   
}, ()=>{}, ()=>{})      
this.$router.replace({  
	name:'xiangqing',          
	params:{             
		id:xxx,             
		title:xxx          
	}   
}, ()=>{}, ()=>{})   
this.$router.forward() //前进
this.$router.back() //后退  
this.$router.go(num) //可前进也可后退，正数前进，负数后退
```

## 10. 缓存路由组件

- 作用：让不展示的[[VueNote#^111111|路由组件]]保持挂载，不被销毁
- 如果不配置include属性则表示所属的路由组件全部保持挂载
- include属性中的是组件名

字符串写法
```vue  
<keep-alive include="News">
    <router-view></router-view>  
</keep-alive>  
```
数组写法
```vue  
<keep-alive :include="['News','Message']">
    <router-view></router-view>  
</keep-alive>  
```

当引入keep-alive 的时候，页面第一次进入，钩子的触发顺序**created> mounted> activated**， 退出时触发deactivated，当再次进入（前进或者后退）时，只触发activated。

所以，有需要的话，应该把mounted钩子里的代码交给activated，或者不要created部分，直接将created中的代码转移到activated中。  

## 11. 路由守卫

作用：保护路由的安全（权限）

### 01 全局前置守卫

配置：在[[VueNote#^111112|路由器]]中配置
初始化、每一次路由切换之前执行 router.beforeEach()
```js
const router = new VueRouter({
	routes:[
		{
			name:'guanyu',
			path:'/about',
			component:About,
			meta:{isAuth:false}
		},
		...
	]
})
router.beforeEach((to,from,next)=>{  
	console.log('beforeEach',to,from,next)
	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
	        next() //放行
		}else{         
			alert('暂无权限查看')
	        // next({name:'guanyu'})      
        }   
    }else{      
	    next() //放行  
	}
})
export default router
```

### 02 全局后置守卫

配置：在[[VueNote#^111112|路由器]]中配置
初始化时、每次路由切换后执行  router.afterEach()
```js
//全局后置守卫：
router.afterEach((to,from)=>{  
	console.log('afterEach',to,from)   
	if(to.meta.title){
		document.title = to.meta.title //修改网页的title  
	}else{      
		document.title = 'vue_test'  
	}
})  
```

### 03 独享路由守卫

配置：在[[VueNote#^111112|路由器]]中配置
beforeEnter
```js
const router = new VueRouter({
	router:[
		{
			name:'guanyu',
			path:'/about',
			component:About,
			meta:{isAuth:false},
			beforeEnter(to,from,next){  
			    console.log('beforeEnter',to,from)  
			    if(to.meta.isAuth){
				    if(localStorage.getItem('school')=='atguigu'){  
				        next()  
				    }else{  
						alert('暂无权限查看')  
				        //next({name:'guanyu'})
				    }  
			    }else{  
				    next()  
				}  
			}
		},
		...
	]
})
```

### 04 组件内路由守卫

在组件文件xxx.vue中配置
```js 
export default {
	...
	//进入守卫：通过路由规则，进入该组件时被调用  
	beforeRouteEnter (to, from, next) {  
	},  
	//离开守卫：通过路由规则，离开该组件时被调用  
	beforeRouteLeave (to, from, next) {  
	}  
	...
}
```

## 12. 路由器的工作模式

### 01 hash模式

- 对于一个url来说， \#及其后面的内容就是hash值
   localhost:8080/students/#/about/...
- hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器
- hash模式：  
   1. 地址中永远带着#号，不美观 
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好
   4. 默认是hash模式
### 02 history模式

- 地址干净，美观 。  
- 兼容性和hash模式相比略差。  
- 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

### 03 切换工作模式

在路由器中配置mode属性
```js
const router =  new VueRouter({  
   mode:'history',
   ...
}
```

# 五、Vue3

## 1. Vue3简介  
  
- 2020年9月18日，Vue.js发布3.0版本，代号：One Piece（海贼王）  
- 耗时2年多、[2600+次提交](https://github.com/vuejs/vue-next/graphs/commit-activity)、[30+个RFC](https://github.com/vuejs/rfcs/tree/master/active-rfcs)、[600+次PR](https://github.com/vuejs/vue-next/pulls?q=is%3Apr+is%3Amerged+-author%3Aapp%2Fdependabot-preview+)、[99位贡献者](https://github.com/vuejs/vue-next/graphs/contributors)   
- github上的：[tags](https://github.com/vuejs/vue-next/releases/tag/v3.0.0)地址
  
## 2. Vue3带来了什么  
  
### 01 性能的提升  

- 打包大小减少41%  
- 初次渲染快55%, 更新渲染快133%  
- 内存减少54%  
  ......  

### 02 源码的升级  

- 使用Proxy代替[[VueNote#01 Object.defineProperty方法|defineProperty]]实现响应式  
- 重写虚拟DOM的实现和[Tree-Shaking](https://developer.mozilla.org/zh-CN/docs/Glossary/Tree_shaking)
  ......  

### 03 拥抱TypeScript

- Vue3可以更好的支持TypeScript

### 04 新的特性
  
1. Composition API（组合API）
   - setup配置 
   - ref与reactive  
   - watch与watchEffect  
   - provide与inject  
   - ......  
2. 新的内置组件  
   - Fragment   
   - Teleport  
   - Suspense  
3. 其他改变  
   - 新的生命周期钩子  
   - data 选项应始终被声明为一个函数  
   - 移除keyCode支持作为 v-on 的修饰符  
   - ......

## 3. Vue3工程创建

### 01 vue-cli 创建工程

[官方文档](https://cli.vuejs.org/zh/guide/creating-a-project.html#vue-create )
  
```bash  
## 查看@vue/cli版本，确保@vue/cli版本在4.5.0以上  
vue --version  
## 安装或者升级你的@vue/cli 
npm install -g @vue/cli  
## 创建
vue create 项目名
## 启动
cd 项目名
npm run serve
```

### 02 vite 创建工程

[官方文档](https://v3.cn.vuejs.org/guide/installation.html#vite)与[vite官网](https://vitejs.cn)

```bash  
## 创建工程
npm init vite-app 项目名
## 进入工程目录  
cd 项目名
## 安装依赖  
npm install  
## 运行  
npm run dev  
```

### 03 什么是vite
  
- vite是新一代前端构建工具。  
- 优势如下：  
	1. 开发环境中，无需打包操作，可快速的冷启动。  
	2. 轻量快速的热重载（HMR）。  
	3. 真正的按需编译，不再等待整个应用编译完成。  
- 传统构建 与 vite构建 对比图
  ![[Pasted image 20231124170014.png]]
  ![[Pasted image 20231124170024.png]]

## 4. Vue3工程结构

在main.js中，引入的不再是Vue构造函数，引入的是一个名为createApp的工厂函数
```js
import { createApp } from 'vue'
import App from './App.vue'

// 创建应用实例对象--app（类似于vue2中的vm，但比vm更“轻”
const app = createApp(App)
// 挂载app
app.mount('#app')
```
在组件中，模板中可以没有根标签
```vue
<template>
	<h1></h1>
	<h2></h2>
</template>
```
其余结构基本相同

## 5. setup函数

### 01 setup是什么

1. setup是Vue3.0中一个新的配置项，值是一个函数；
2. setup是所有<strong style="color:#DD5145">Composition API（组合API）</strong>“ 表演的舞台 ”。  
3. 组件中所用到的：数据、方法等等，均要配置在setup中。  

### 02 setup函数的两种返回值

   1. 若返回一个对象，则对象中的属性、方法, 在模板中均可以直接使用。（重点关注！） 
```js
export default {
	...
	setup(){
		let name = 'marry'
		let age = 18
		    
		function sayHello(){
			alert('${name} and ${age}')
		}
	
		return{
			name,
			age,
			sayHello
		}
	}
}
```

```html
<div>{{name}}</div>
<button @click="sayHello">点击</button>
```
   1. <span style="color:#aad">若返回一个渲染函数：则可以自定义渲染内容。（了解）</span>  
```js
setup(){
	...
	//返回一个函数（渲染函数）  
	return ()=> h('h1','尚硅谷')
}
```

### 03 注意事项

1. 尽量不要与Vue2.x配置混用  
	- Vue2.x配置（data、methos、computed...）中<strong style="color:#DD5145">可以访问到</strong>setup中的属性、方法。  
	- 但在setup中<strong style="color:#DD5145">不能访问到</strong>Vue2.x配置（data、methos、computed...）。  
	- 如果有重名, setup优先。  
2. setup不能是一个async函数，因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性。（后期也可以返回一个Promise实例，但需要Suspense和异步组件的配合）

## 6. ref函数 & reactive函数 

### 01 ref函数

作用定义响应式的数据

语法：
- 先引入ref函数
```import {ref} from 'vue'```

- 定义一个响应式的数据
```const xxx = ref(initValue)``` 

- 创建一个包含响应式数据的<strong style="color:#DD5145">引用对象（reference对象，简称ref对象）</strong>。  
	JS中操作数据： ```xxx.value```  
	模板中读取数据: 不需要.value，直接：```<div>{{xxx}}</div>```  

### 02 ref接收数据

  - 接收的数据可以是：基本类型、也可以是对象类型。  
  - 基本类型的数据：响应式依然是靠``Object.defineProperty()``的```get```与```set```完成的。  
  - 对象类型的数据：内部求助了Vue3.0中的一个新函数—— ```reactive```函数。

### 03 reactive函数  
  
- 作用: 定义一个<strong style="color:#DD5145">对象类型</strong>的响应式数据（基本类型不要用它，要用```ref```函数）  
- 语法：
  先引入reactive
  ```import {reactive} from 'vue'```
  接收一个对象（或数组）
  ```const 代理对象= reactive(源对象)```
  返回一个<strong style="color:#DD5145">代理对象（Proxy的实例对象，简称proxy对象）</strong>  
- reactive定义的响应式数据是“深层次的”。  
- 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据进行操作。

### 04 reactive接收数据

```js
// js中操作数据，不需要value
代理对象.属性 = 'xxx'
```

## 7. Vue3响应式原理

回顾Vue2响应式原理

### 01 实现原理:   

- 通过Proxy（代理）:  拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等。  
- 通过Reflect（反射）:  对源对象的属性进行操作。  
- MDN文档中描述的Proxy与Reflect：  
	1. Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy  
	2. Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect  
```js  
new Proxy(data, {  
	// 拦截读取属性值  
	get (target, prop) {  
		return Reflect.get(target, prop)          
	},          
	// 拦截设置属性值或添加新属性  
    set (target, prop, value) {  
	    return Reflect.set(target, prop, value)          
    },          
    // 拦截删除属性  
    deleteProperty (target, prop) {  
	    return Reflect.deleteProperty(target, prop)          
	}      
})      

proxy.name = 'tom'     
      ```

