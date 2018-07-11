# project-notes
Start a project and take notes
#### 1、修改ip和端口
在package.json文件的对象中增加config属性，代码如下：
```javascript
  "config": {
    "nuxt": {
      "host": "192.168.xx.xxx",
      "port": "2222"
    }
  }
```
即可，打开网址 http://192.168.xx.xxx：2222 访问你的项目。
#### 2、建立路由
pages下新建文件或文件夹，文件即路由。<br>
Nuxt.js 依据 pages 目录结构自动生成 vue-router 模块的路由配置。<br>
不多说，看文档，[GO->](https://zh.nuxtjs.org/guide/routing)
#### 3、使用SCSS编译CSS样式
添加新依赖
```
  npm i node-sass sass-loader scss-loader --save-dev
```
书写样式的代码如下：
```
<style lang="scss" scope>
  h1{
	color:red;
  }
</style>
```
lang代表使用的预编译语言，scope设置该style的样式修饰中只在作用于该页面。
#### 4、使用axiso请求数据，并设置代理
[GO->](https://github.com/nuxt-community/axios-module/blob/master/docs/options.md)<br>
添加依赖
```
  npm install @nuxtjs/axios
```
上述链接已详细介绍，在nuxt.config.js文件添加代码：
```javascript
  modules: [
    '@nuxtjs/axios'
  ], 
  axios: {
    proxy: true // Can be also an object with default options
  },
  proxy: {
    '/api/': { target: 'http://112.80.xx.xxx', pathRewrite: {'^/api/': ''} }
  },
```
至此，数据请求、跨域、服务端和客户端cookie的默认携带都已解决，已可以完成和后端开发人员的交互。
#### 5、使用vuex
不了解vuex，可学习官网[GO->](https://vuex.vuejs.org/zh/)<br>
nuxt官网提供了使用vuex的教程[GO->](https://zh.nuxtjs.org/examples/vuex-store)
在store文件夹中新建index.js、mutations.js等,你需要的文件
```javascript
//index.js 文件
import Vuex from 'vuex'

import mutations from './mutations'

const createStore = () => {
  return new Vuex.Store({
    state: {
      aaa:111, 
    },
    mutations
  })
}

export default createStore
```
```javascript
//mutations.js 文件
const mutations = {
	BBB(state) {
		state.aaa = 222;
	}
} 
```
```javascript
//a.vue a组件文件
computed: mapState([ //获取store数据
  'aaa'
]),  
methods: {
    ...mapMutations([ //获取mutations的对象
	'BBB' 
    ]), 
    CCC(){
        this.BBB();   //操作mutations，从而修改store数据
    }
}
```
备注：以上的事例中aaa/AAA/BBB/CCC,均为自定义变量名；这是一个基本使用方法，还有其他的参考官网。
#### 登录鉴权
官网提供教程[GO->](https://zh.nuxtjs.org/examples/auth-routes)<br>
使用express-session保存最终的登录状态；<br>
使用nuxtServerInit()在每次进入页面时做相应的动作；<br>
即过程如下：<br>
express-session保存状态->nuxtServerInit()中判断状态是否存在(即是否登录)，不存在则没有登录，存在在将需要用到的状态数据存储到vue的store中->其他组件从store中获取需要的数据































