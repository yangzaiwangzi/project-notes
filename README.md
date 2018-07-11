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
#### 3、使用axiso请求数据，并设置代理
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






























