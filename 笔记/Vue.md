## 前端三要素

#### HTML

#### css

css层叠样式表是一门标记语言，并不是编程语言，因此不可以自定义变量，不可以引用。



>css预处理器

css预处理器定义了一种新的语言。其基本思想是用一门专门的编程语言，为css增加了一些编程特性，将css作为目标生成文件，开发者就只要使用这种语言进行css的编码工作。

>SASS:

`世界上最成熟、最稳定、最强大的专业级CSS扩展语言！`

**基于Ruby**，通过微服务端处理，功能强大。解析效率高。上手难度高。

>LESS:

**基于NodeJS**，通过客户端处理，使用简单。功能比SASS简单，解析效率也低于SASS，时候后端工作人员。

#### js

## javaScript 框架

- jQuery

简化Dom操作

- Angular

Google收购的，java程序员开发（里面涉及了一些java的思想如：mvc），提出**模块化开发**理念，即把后端的MVC模式搬到了前端。

- React

facebook出品，特点是提出新概念[**虚拟DOM**]用于减少真实的dom操作。在内存中模拟dom操作，有效的提升了前端渲染效率，缺点是使用复杂。

- Vue

一款**渐进式JavaScript框架**，特点是集成了Angular(模块化)和React（虚拟dom）特点。特点是**声明式渲染**和**实时相应**。

- Axios

前端通信框架，Vue只处理dom，所以不具备通信能力，需要一个额外的通信框架与服务器交互，jQuery亦可,Axios和Vue更兼容。



## UI框架

- Ant-Design:阿里巴巴出品，基于React的UI框架
- ElementUI iview,ice:饿了吗出品，基于Vue的UI框架
- Bootstrap：Twitter推出的一个用于前端开发的开源工具包
- AmazeUI:又叫“妹子UI”，一款HTML5跨屏前端框架
- LayUI:面向后端开发者，AMD模块管理

## JavaScript 构建工具

- Babel:JS编译工具，主要用于浏览器不支持的ES新特性
- Webpack：模块打包器，主要作用是打包，压缩，合并及按序加载



## 第一个Vue程序

通过在线的cdn体验Vue

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-- view层 模板(template)-->
<div id="app">
    {{message}}
</div>

<!--操作代码-->
<script  src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        //元素绑定
        el:"#app",
        //Model:数据
        data:{
            message:"hello vue!"
        }
    });
</script>
</body>
</html>
```

绑定信息(v-bind:,  :)

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-- view层 模板-->
<div id="app">
    <span v-bind:title="message" >
        鼠标悬停查看绑定信息
    </span>
</div>


<script  src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        //元素绑定
        el:"#app",
        //Model:数据
        data:{
            message:"hello vue!"
        }
    });
</script>
</body>
</html>
```

点击事件(v-on:click ,@click)

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-- view层 模板-->
<div id="app">
    <button v-on:click="isClick">Click me</button>
</div>


<script  src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        //元素绑定
        el:"#app",
        //Model:数据
        data:{
            message:"hi"

        },
        methods:{
            isClick:function (event){
                alert(this.message);
            }
        }
    });
</script>
</body>
</html>
```

v-mdel(双向绑定)

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-- view层 模板-->
<div id="app">
    输入的文本：<input type="text" v-model="message">{{message}}
</div>


<script  src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        //元素绑定
        el:"#app",
        //Model:数据
        data:{
            message:"hi"
        }
    });
</script>
</body>
</html>
```

模板（组件，类似于html中的h1,p,span,这里的component更加灵活）

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-- view层 模板-->
<div id="app">
    
    <ruyi v-for="i in items" v-bind:li="i"></ruyi>
    <!--这里的ruyi组件相当于i个li组件-->

</div>


<script  src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    <!--组件 包含组件名ruyi，组件的样式template，组件传值props-->
    Vue.component('ruyi',{
        props:['li'],
        template:'<li>{{li}}</li>'
    })
    var vm = new Vue({
        //元素绑定
        el:"#app",
        //Model:数据
        data:{
            items:["A","B","C"]
        }

    });
</script>
</body>
</html>
```

## Axios

通信，获取后端数据并展示（这里的后端数据是伪造的json文件）

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>

<!-- view层 模板-->
<div id="app" v-clock>
    <div>成绩： {{info.Score}}</div>
    <div>姓名： {{info.name}}</div>
</div>

<!--Vue在线cdn-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
    var vm = new Vue({
        //元素绑定
        el:"#app",
        data(){
            return{
                info:{
                    Score:null,
                    name:null
                }
            }
        },
        mounted(){
            axios.get("../data.json").then(response => this.info=response.data)
        }

    });
</script>
</body>
</html>
```

data.json

```json
{"Score": "A","name": "ruyi"}
```



## 计算属性

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>

<!-- view层 模板-->
<div id="app" v-clock>
    <!--    方法，每次调用的时候是有计算开销的-->
    <p>ccurrentTime1 {{currentTime1()}}</p>
    <!--    计算属性，是属性，在内存中缓存，在数值不变的情况下没有计算开销-->
    <P> currentTime2 {{currentTime2}}</P>
</div>

<!--Vue在线cdn-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        //元素绑定
        el:"#app",
        methods:{
            currentTime1: function (){
                return Date.now();
            }
        },
        computed:{
            currentTime2: function (){
                return Date.now()
            }
        }

    });
</script>
</body>
</html>
```

## slot

插槽，前面的component只负责样式的渲染，比如这里的todo组件就是一个div中套一个插槽和一个列表，列表中继续嵌套插槽。这里的插槽可以是文本，也可以是组件，非常灵活！从某种程度上来说我们可以将大的框架写出来，里面的每个部分用一个个插槽实现，降低耦合性，提高代码的复用性。

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>

<!-- view层 模板-->
<div id="app" v-clock>
<todo>
    <todo_title slot="todo_title" :title="title"></todo_title>
    <todo_item slot="todo_item" v-for="i in item" :item="i"></todo_item>
</todo>
</div>

<!--Vue在线cdn-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
    Vue.component("todo",{
        template:'<div>\n' +
            '    <slot name="todo_title"></slot>\n' +
            '    <ul>\n' +
            '        <slot name="todo_item"></slot>\n' +
            '    </ul>\n' +
            '</div>'
    })
    Vue.component("todo_title",{
        props:["title"],
        template: '<div>{{title}}</div>'
    })
    Vue.component("todo_item",{
        props:["item"],
        template:'<li>{{item}}</li>'
    })
    var vm = new Vue({
        //元素绑定
        el:"#app",
        data:{
            title:"选项",
            item:["A","B","C","D"]
        }

    });
</script>
</body>
</html>
```

## 自定义事件与内容分发

现在我们的网页元素是由一个个组件构成的，而数据可能集中在外部管理，如何删除组件中的一些元素以及它对应的数据呢？

![image-20230411171832505](G:/typora_img/image-20230411171832505.png)

如果我们想要删除com1_2中的指定元素，我们要删除com1_2中的一个li元素，这个在com1_2中定义一个删除方法就可以实现，此外我们还要将data中关于那个li元素的数据删除，很显然com1_2的权限不够，他只能去通知data删除指定（传参）数据。

在todo_item中调用方法remove，并且通知removeItem删除数据。

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>

<!-- view层 模板-->
<div id="app" v-clock>
<todo>
    <todo_title slot="todo_title" :title="title"></todo_title>
    <todo_item slot="todo_item" v-for="(i,index) in item"
               :item="i" :index="index" v-on:remove="removeitem(index)"></todo_item>
</todo>
</div>

<!--Vue在线cdn-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
    Vue.component("todo",{
        template:'<div>\n' +
            '    <slot name="todo_title"></slot>\n' +
            '    <ul>\n' +
            '        <slot name="todo_item"></slot>\n' +
            '    </ul>\n' +
            '</div>'
    })
    Vue.component("todo_title",{
        props:["title"],
        template: '<div>{{title}}</div>'
    })
    Vue.component("todo_item",{
        props:["item","index"],
        template:'<li>{{index}}------{{item}} &nbsp;<button @click="remove">删除 </button></li>',
        methods:{
            remove: function (index){
                this.$emit('remove',index)
            }
        }
    })
    var vm = new Vue({
        //元素绑定
        el:"#app",
        data:{
            title:"选项",
            item:["A","B","C","D"]
        },
        methods:{
          removeitem: function (index){
              this.item.splice(index,1);
          }
        }
    });
</script>
</body>
</html>
```

## Vue-cli

- 安装nodejs     https://nodejs.org/en
- 安装淘宝镜像 

```
npm install cnpm -g
```

- 安装vue-cli

```
npm install vue-cli -g
```

- 创建vue程序

```
vue init webpack 项目名
```

>project name	项目名

>project description	项目描述

>Author	项目作者

> Vue build	

> install vue-router	是否安装vue-router

>Use ESLint to lint your code	是否使用ESLint做代码检查

>Set up unit test	单元相关测试

> Setup e2e tests with Nightwatch	单元测试

> Should we run npm install for you after the project has been created	创建完后直接初始化

- 安装相应依赖

```
npm install
```

- 运行

```
npm run dev
```




## Webpack

webpack是一个现代JavaScript应用程序的静态模块打包器（module bundler）。当webpack处理应用程序时，它会递归的构建一个依赖关系图（dependency graph）,其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个bundle。

Webpack是当下最热门的前端资源模块化管理和打包工具，它可以将许多松散耦合的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分离，等到实际需要时再异步加载。通过loader转换，任何形式的资源都可以当作模块，如CommonsJS，AMD,ES6,CSS,JSON,等

伴随移动互联网的大潮，越来越多的网站从网页模式转化到WebApp模式。WebApp通常是一个SPA（单页面应用），每个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的JS代码，这给前端的开发流程和资源组织带来挑战。

前端开发是基于多语言，多层次的编码和组织工作，交付的产品是基于浏览器的，这些资源通过增量加载的方式运行到浏览器端，如何在开发环境中组织好这些碎片化的资源是前端工程师多年来一直探索的问题。

- 早期的模块化

```javascript
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="module3.js"></script>
<script src="module4.js"></script>
```

一些弊端：

全局作用域下容易造成变量冲突

文件只能按照<script>的书写顺序进行加载

开发人员必须解决模块和代码库的依赖关系（手动导入）

在大型项目中各种资源难以管理

- CommonsJS

服务器端的NodeJS遵循CommonJS规范，该规范核心思想是允许模块通过require方法来同步加载所需依赖的其他模块，然后通过exports或module.exports来暴露的接口

```
require("module");
require("../module.js")
export.doStuff = function(){};
module.exports = someValue;
```

优点：

服务器端便于重用

npm中有大量可以使用的模块包

简单易用

缺点：

同步的模块加载方式不适合在浏览器环境，浏览器的资源是异步加载

不能非阻塞的并行加载多个模块

- AMD

Asynchronous Module Definition规范就是一个接口define（id?,dependencies?.factory）;他要在生命模块的时候指定所有的依赖dependencies，并且还要当作形参传到factory中。

```
define("module",['dep1','dep2'],function(d1,d2){
return someExportedValue;
});
require(["module","../file.js"],function(module,file){});
```

优点：

在浏览器环境中异步加载

并行加载多个模块

缺点：

提高开发成本

不符合通用的模块化思维

- CMD

Common Module Definition和AMD相似，与CommonJS规范保持很大的兼容性。

```
define(function(require,exports,module){
var $ = require("jquery");
var Spinning = require("../spinning");
exports.doSomething = ...;
module.exports = ...;
})
```

优点：

依赖就近，延迟执行

可以很容易在Nodejs中执行

缺点：

依赖SPM打包，模块的加载逻辑偏重

- ES6

EcmaScript6标准增加了JavaScript语言层面的模块定义。其思想是，尽量静态化，是编译的时候就能确定模块的依赖关系，以及输入和输出变量。CommonJS和AMD都只能在运行时确定。

```
import "jquery";
export function doStuff(){}
module "localModule"{}
```

优点：

容易进行静态分析

缺点

原生浏览器不兼容

全新的命令



人们期待的模块系统

可以兼容多种模块风格，尽量可以 利用已有的代码，不仅仅是JavaScript模块化，还有CSS，图片，字体等资源。webpack目前可以做到

#### 安装webpack

```
npm install webpack -g
npm install webpack-cli -g
```

#### 配置

创建webpack.config.js配置文件

- entry：入口文件，指定WebPack用哪个文件作为项目的入口
- output：输出，指定处理完成的文件存放位置
- module:模块，用于处理各种类型的文件
- plugins：插件，如：热更新，代码重用
- resolve：设置路径指向
- watch：监听，用于设置文件改动后直接打包

```js
'use strict'
const path = require('path')
const utils = require('./utils')
const config = require('../config')
const vueLoaderConfig = require('./vue-loader.conf')

function resolve (dir) {
  return path.join(__dirname, '..', dir)
}



module.exports = {
  context: path.resolve(__dirname, '../'),
  entry: {
    app: './src/main.js'
  },
  output: {
    path: config.build.assetsRoot,
    filename: '[name].js',
    publicPath: process.env.NODE_ENV === 'production'
      ? config.build.assetsPublicPath
      : config.dev.assetsPublicPath
  },
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
    }
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueLoaderConfig
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        include: [resolve('src'), resolve('test'), resolve('node_modules/webpack-dev-server/client')]
      },
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('img/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.(mp4|webm|ogg|mp3|wav|flac|aac)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('media/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
        }
      }
    ]
  },
  node: {
    // prevent webpack from injecting useless setImmediate polyfill because Vue
    // source contains it (although only uses it if it's native).
    setImmediate: false,
    // prevent webpack from injecting mocks to Node native modules
    // that does not make sense for the client
    dgram: 'empty',
    fs: 'empty',
    net: 'empty',
    tls: 'empty',
    child_process: 'empty'
  }
}

```

#### 使用webpack

- 创建项目mywebpack（创建文件夹，使用IDEA打开）
- 添加modules目录
- 在modules下添加一个hello模块（hello.js）,暴露一个方法

```js
//暴露一个方法
exports.sayHi = function (){
    document.write("<div>everything is ruyi</div>")
}
```

- 在modules下添加main模块（main.js）,接收并调用hello

```js
var hello = require("./hello");
hello.sayHi();
```

- 编写webpack文件(webpack.config.js)

```js
module.exports = {
    entry:'./modules/main.js',
    output:{
        filename:"./js/bundle.js"
    }
}
```

- 使用webpack命令打包，生成浏览器兼容的bundle.js文件
- 创建一个index.html，调用bundle.js文件即能实现模块化开发

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!--前端模块化开发-->
<script src="dist/js/bundle.js"></script>
</body>
</html>
```

## Vue-router

