# 一、Element UI

[element-ui官网](https://element.eleme.cn/#/zh-CN)

## 1. 引入element-ui

### 01 完整引入

npm i element-ui -S

在 main.js 中写入以下内容：
```javascript
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

### 02 按需引入

npm install babel-plugin-component -D

找到babel.config.js文件，追加配置：
```javascript
module.exports = {  
	presets: [  
		// '@vue/cli-plugin-babel/preset',  
	    ["@babel/preset-env", { "modules": false }],  
	],  
	plugins:[  
	    [  
			"component",
			{  
		        "libraryName": "element-ui",  
		        "styleLibraryName": "theme-chalk"  
		    }  
	    ]  
	]  
}
```

接下来，如果只希望引入部分组件，比如 Button 和 Select，那么需要在 main.js 中写入以下内容：
```javascript
import Vue from 'vue';
import { Button, Select } from 'element-ui';
import App from './App.vue';

Vue.component(Button.name, Button);
Vue.component(Select.name, Select);
/* 或写为
 * Vue.use(Button)
 * Vue.use(Select)
 */

new Vue({
  el: '#app',
  render: h => h(App)
});
```

## 2. 基本使用

![[Pasted image 20231124161821.png]]

划到最底部找到 Attributes ，有详细配置

![[Pasted image 20231124161950.png]]

