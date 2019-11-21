# WebPack

`作用`：

对css文件打包处理

对less文件打包处理

对ttf文件打包处理

对img文件打包处理

对es6、es7做降级处理打包

对vue文件打包处理

以上内容经过webpack可以**一次性**全部做**转码、降级**处理，使得开发速度更快、更高效

并且打包好的文件内容可以供所有浏览器识别使用，兼容性好



## 什么地方适合使用

`什么地方适合使用`：

1. spa(single program application单页面应用程序项目)项目(后台项目、手机移动端)，spa项目页面请求数量小于500个
2. vue、react、angular都要使用



`注意`：

​	像sohu、腾讯、163等cms(content manager system内容管理系统)等复杂、多页面系统不适合通过webpack开发

webpack是nodejs开发出来的

## 隔行换色案例

`步骤`：

1. 创建01-pack项目运行目录

   > 注意：01-pack的上级各目录不要有中文或特殊符号，一般英文、数字或横线 即可

2. 创建package.json文件  yarn -y init

3. 给项目安装jquery依赖包  yarn  add jquery

4. 创建目录文件 src/index.html   src/index.js

5. 在**src/index.js**中实现li标签隔行换色代码实现

   ```js
   // 页面加载事件
   $(function(){
     $('li:odd').css('background-color','lightgreen')
   })
   ```

   

6. 在src/index.html里边引入jquery.js和 src/index.js，并绘制许多li标签

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <meta http-equiv="X-UA-Compatible" content="ie=edge">
     <title>Document</title>
     <script src="../node_modules/jquery/dist/jquery.js"></script>
     <script src="./index.js"></script>
   </head>
   <body>
     <ul>
       <li>第1个li标签</li>
       <li>第2个li标签</li>
       <li>第3个li标签</li>
       <li>第4个li标签</li>
       <li>第5个li标签</li>
       <li>第6个li标签</li>
       <li>第7个li标签</li>
       <li>第8个li标签</li>
     </ul>
   </body>
   </html>
   ```

7. 现在隔行换色效果就会呈现



`注意`：

1. src目录暂时是**固定**的，后期可以自定义

2. src/index.js   src/index.html 两个文件名字暂时是**固定**的，后期可以自定义



## 安装配置

webpack官网：https://webpack.docschina.org/

`步骤`：

1. 安装webpack和相关依赖包  yarn add -D webpack webpack-cli

2. 在package.json文件中设置如下内容

   ```js
     "scripts":{
       "build":"webpack"
     },
   ```

   > 现在就可以在命令行中执行 npm run build 命令应用webpack，后续讲解



`注意`：

1. 需要通过-D 开发依赖方式装包，yarn中 -D 和 --dev互为别名，npm中 -D 和 --save-dev互为别名
2. 要安装两个依赖包webpack和webpack-cli，后者是前者的内部依赖
3. build是自定义名称，scripts和webpack是固定的



## 运行和开发依赖

依赖包的安装分为两种方式：开发 和 运行

- 依赖包在项目生产中充当**工具**作用的，建议通过**开发依赖**方式安装，例如webpack
- 依赖包在项目生产完毕**上线后都需要**使用的，就通过**运行依赖**方式安装，例如jquery



安装**运行**依赖包(dependencies)

```javascript
yarn add XXX  // 直接装包，没有任何其他参数，旧npm版本中要求设置--save参数
例如jquery通过运行依赖方式安装
yarn add jquery
```

安装**开发**依赖包(devdependencies)

```javascript
yarn add XXX --save-dev // 设置额外参数--save-dev(简称为-D)
例如webpack等依赖包通过开发依赖方式安装
yarn add -D  webpack
```

问：依赖包如何区分是**开发的**还是**运行的**：
答：在 src/main.js 入口文件中通过require(或es6 import)引入的就是运行依赖包，否则是开发依赖包

​       或在组件中引入的，也是运行依赖包



运行依赖和开发依赖包会分别配置到package.json的  **dependencies**和 **devdependencies** 段里边

我们通过软件仓库获得到别人开发的项目代码，如果还需要二次开发，就执行如下指令安装依赖包，其表示要安装<font color=red>全部</font>的依赖包(运行的和开发的)

```
yarn
```

如果只是运行别人的项目，不做二次开发，就执行如下指令，表示只安装<font color=red>运行</font>依赖包(去除了不用的开发依赖包，**缩减了项目体积**，转而运行更快了)

```
yarn --production
```

`注意`：

1. npm通过开发依赖方式装为： npm i -D xxx  或  npm i --save-dev xxx    (-D  与 --save-dev互为别名)
2. **yarn**通过开发依赖方式装为： yarn add -D xxx  或  yarn add --dev xxx   (-D  与 --dev互为别名)
3. 不设置-D  默认就是运行依赖方式装包
4. 开发依赖 在前端开发体现不明显，后端nodejs比较突出



## 打包实现

`步骤`：

1. 在src/index.html中**注释掉**  jquery.js 和 index.js 的引入

   ```html
   <!--
   <script src="../node_modules/jquery/dist/jquery.js"></script>
   <script src="./index.js"></script>
   -->
   ```

   

2. 在 src/index.js 中通过 import  ** from ** 的方式引入 jquery

   ```js
   // 通过es6模块化方式，导入jquery(使用require方式导入也是可以的)
   // (把所有需要被打包的静态文件，都要放到该文件中)
   import $ from 'jquery'
   
   // 页面加载事件
   $(function(){
     $('li:odd').css('background-color','lightblue')
   })
   ```
   
   

3. 做打包处理，执行指令  npm run build

   > 打包完毕，就会在根目录生成**dist目录**，里边有main.js文件，其是jquery.js 和 隔行换色代码index.js 集成的体现

4. 在src/index.html中直接引入 dist/main.js的打包文件做应用即可

   ```html
    <!--引入jquery-->
    <!-- <script src="../node_modules/jquery/dist/jquery.js"></script> -->
    <!-- <script src="./index.js"></script> -->
    <script src="../dist/main.js"></script>
   ```
   


`原理`：

​	webpack**默认**会寻找 src/index.js 文件(本身包括两部内容：jquery.js和 隔行换色代码)，编译处理之，并把结果输出到 dist/main.js里边去了



`注意`：

1. webpack默认会生成dist目录存储打包文件，后期可以自定义该目录名字
2. 打包好的文件名称为main.js，后期也可以自定义该文件名字



# 配置

## 打包模式

`目标`：

​	可以给webpack配置不同的打包模式

> 现在打包时会黄色警告信息，提示没有设置mode模式



`步骤`：

1. 在项目根目录创建名称为 webpack.config.js 的配置文件

2. 在webpack.config.js中做如下配置

   ```js
   module.exports = {
     mode: 'development'   // 也可以配置为 production
   };
   ```
   
> production:生产模式，打包好的文件内容是优化压缩的
   > development:开发模式，打包好的文件内容适合开发调试，有适当的空白、回车、注释



`注意`：

1. webpack默认配置文件名称为webpack.config.js，也可以自定义为其他名字，但是package.json需要额外再做配置
2. 项目开发阶段适合使用 development 开发模式，开发完毕部署上线后使用 production(打包的文件体积小，节省资源)



## 入口和出口文件

​	src/index.js  改名字 为 src/main.js  (该文件是项目的主入口程序文件)

​	dist/main.js  改名字 为 dist/bundle.js

> src/index.js 是被打包的文件，称为“入口文件”
>
> dist/main.js 是打包后的文件，称为“出口文件”



`步骤`：

​	在webpack.config.js文件中做如下内容配置；

```js
const ph = require('path')
module.exports = {
  // 1) 给项目配置入口文件路径名
  entry: ph.resolve('./src/main.js'), 
  // 2) 给项目配置出口文件路径名
  output: {
    path: ph.resolve( './dist'), // 定义出口文件"目录"
    filename: 'bundle.js' // 定义出口"文件名称"
  }
}
```



`注意`：

1. 自行把物理文件src/index.js 的名字修改为 src/main.js 名字

2. path模块获得一个文件的**绝对路径名**有如下两种方式：

   1. path.join(__dirname,xxx)
   2. path.resolve(xxx)

   resolve相比join要更简便，可以不用设置__dirname

3. webpack是通过nodejs语言开发的，故在webpack.config.js文件中要通过**require**方式导入模块

   > 在src/main.js主入口文件倒是可以使用import或require 引入其他文件



## 编译模板文件

`步骤`：

1. 安装html-webpack-plugin插件依赖包  yarn  add -D  html-webpack-plugin

2. 在webpack.config.js中给上述插件做配置

   ```js
   const ph = require('path')
   var HtmlWebpackPlugin = require('html-webpack-plugin'); // 引入插件模块
   module.exports = {
   	// 给webpack配置功能插件
     plugins: [
       new HtmlWebpackPlugin({
         // 设置“源模板”文件的路径名
         template:ph.resolve('./public/index.html') 
       })
     ],
   }
   ```
   
3. 在public/index.html 不要引入任何js文件

4. 现在打包处理 npm  run build，就会发现在dist目录里边生成了index.html模板文件，内容来自 public/index.html，并且有**自动引入**打包好的js文件在里边



`注意`：

1. 如果不给HtmlWebpackPlugin内部配置template源模板文件，则会生成一个没有任何业务逻辑的、空的html模板文件
2. 创建public目录，并把文件 src/index.html  挪到这个目录中
3. dist目录文件不要做开发，要去src下边开发应用



## 实时打包

`目标`：

​	给webpack开启实时打包功能，使得浏览器可以随时查看修改代码的效果

> 项目的src目录里边任何一个文件被改动都需要**重新打包**看效果，工作效率太低
> 怎么做呢？
> 答：利用“实时打包”工具实现高科技效果，业务代码随时修改、浏览器随时查看对应效果



`步骤`：

1. 安装实时打包依赖包  yarn add -D webpack-dev-server

2. 在webpack.config.js文件做如下配置

   ```js
   module.exports = {
     // 给dev-server(实时打包运行机制)做配置
     devServer: {
       open: true,  // 启动实时打包服务后会自动开启浏览器并展示项目效果
       port: 12306, // web服务的端口号码,可以自定义为其他
       host: '127.0.0.1', //  web服务的主机名地址，必须是本机真实的
     },
   }
   ```

> 127.0.0.1 是每个电脑都拥有并且不变的ip地址，直接使用即可，推荐使用
>
> 端口号码：12306，理论值：1到65535之间  

3. 在package.json中做如下配置

   ```js
     "scripts": {
       "serve": "webpack-dev-server"
     },
   ```
   
> serve：是自定义名称，可以修改为其他
   >
   > webpack-dev-server：是固定名称

4. 现在在项目根目录命令行终端中可以执行 npm  run serve 指令，就自动打开浏览器查看项目运行效果了

   > 现在，src源代码随时修改，浏览器随时查看效果



`注意`：

1. npm run serve 会开启一个前台服务，不能关闭，否则没有实时加载效果了
2. 实时打包的内容提供者是“内存”，不需要借助物理文件支持，本身也不生成**dist目录和相关打包文件**
3. 实时打包本身有创建了一个http服务，并支持访问



# loader

### 应用css文件

`步骤`：

1. 新建 src/css/1.css 样式文件，并设置简单样式

2. 在 src/main.js 中import引入1.css文件

3. 此时，终端实时打包窗口报错

   > 错误原因提示：告知缺少对应的loader

`注意`：

webpack没有配置loader，实时打包服务**开启**状态下，直接应用css文件，命令行终端会报错，原因是没有loader支持



### loader介绍

`什么是`：

​	loader是webpack编译处理不同类型文件的工具(本质是函数)

​	css文件对应 style-loader、 css-loader

​	less文件对应 style-loader、 css-loader、 less-loader

​	img文件对应 url-loader 、file-loader

​	es6、es7文件对应 babel-loader



### 安装使用loader

`步骤`：

1. 安装loader相关依赖包  yarn add -D css-loader  style-loader

2. 在webpack.config.js中给loader做如下配置

   ```js
   module.exports = {
     // 给webpack配置各种loader
     module: {
       rules: [
         {
           // 1) css之loader配置
           test: /\.css$/, // 正则匹配名字以.css结尾的文件，然后交给如下loader处理
           use: ['style-loader', 'css-loader'],
         }
       ]
     }
   }
   ```
   
3. 现在重启实时打包服务(npm run serve)，css样式效果就ok了



`注意`：

1. style-loader、css-loader有严格的前后设置顺序，不要颠倒

2. 有的文件需要配置一个loader、有的需要配置多个，不固定



### 两个loader解读

两个loader的作用：

​	css-loader   :该loader可以实现在主入口js文件中以import/require的方式引入css 

​	style-loader ：该loader可以实现在html运行文档中以style标签的形式嵌入css 内容，使得样式生效

​	css-loader第一个顺序执行，style-loader之后再执行



css之loader运行原理：

1. webpack.config.js只要把css相关的loader给配置好，那么import引入的css文件内容就被打包到dist/bundle.js文件里边去了
2. bundle.js文件在执行的时候会通过 style 标签把css样式嵌入到应用程序文档里边



## img

### 应用img背景图片

`步骤`：

1. 给public/index.html创建两个div

2. 准备两个图片： src/img/bigger.jpg  src/img/small.jpg

3. 在1.css文件中给两个div设置背景图片等样式 (第1个div设置bigger.jpg  第2个div设置small.jpg)

   ```css
   #one{
     width: 200px;
     height: 100px;
     background-color: pink;
     background-image:url('../img/bigger.jpg')
   }
   #two{
     width: 200px;
     height: 100px;
     background-color: lightgreen;
     background-image:url('../img/small.jpg')
   }
   ```
   
4. 现在实时打包终端服务报错

   > 错误原因：jpg图片文件缺少对应的loader处理



`注意`：

> 设置两个图片，大小分别 大于 和 小于 8192个字节即可



### 安装使用loader

`步骤`：

1. 安装loader依赖包  yarn  add -D url-loader  file-loader

2. webpack.config.js配置loader，具体如下：

   ```js
   module.exports = {
       // 给webpack配置各种loader
     module: {
       rules: [
         {
           // 2) img图片之loader配置
           test: /\.(png|jpg|gif)$/i,
           loader: 'url-loader',
           options: {
             limit: 8192
           }
         }
       ]
     }
   }
   ```
   
3. 现在实时打包服务重启(npm run serve)，发现背景图片效果已经呈现



`注意`：

file-loader不需要配置，条件满足会自动调用



### loader解读

`相关loader作用`：

file-loader 把符合条件的图片文件**重新打包**生成在dist目录

url-loader:负责把图片变为**字符串**使用，并嵌入到应用文档里边，好处：可以节省一个http请求资源

`limit作用`：

文件大小  大于limit:8192   字节的，就走 file-loader，

文件大小  小于等于8192  字节的，就走 url-loader

url-loader  limit:8192(8k)是判断图片大小的**阈值**，该阈值建议大小是10k左右

`注意`：

1. index.html模板里边设置的**\<img\>标签图片**不能被webpack处理
2. 大小大于10kb的图片不适合变为字符串，不划算，因为图片变为字符串后，大小会更大



### 打包好图片在哪

`图片在哪`：

1. 大图片(大于8192字节)：重新生成在dist目录，名字会重新定义

2. 小图片(小于等于8192字节)：以base64格式字符串集成到打包的bundle.js文件里边，之后以style标签方式植入到运行应用文件里边，本身不会消耗http资源



### 创建子级目录存储图片

`步骤`：

​	给url-loader配置参数，具体如下：

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/i,
        loader: 'url-loader',
        options: {
          limit: 8192,
          outputPath:'image' // 创建子级目录存储生成的图片
        }
      }
    ]
  }
}
```



`注意`：

1. 经过上述配置，以后再做物理打包npm run build,大图片就被存储到 **dist/image** 目录里边去了
2. outputPath本身是file-loader的参数，但是可以给url-loader配置，它们内部会自动传递



### base64格式字符串说明

`什么是`：

​	Base64是一种基于**64个可打印**字符来**表示二进制数据**的方法，是二进制数据的封装

​	一个图片最本质的内容是二进制数据，当前应用级别无法直接表示，需要借助base64格式



### 各种loader配置介绍

```js
	// 没有参数的 1个或多个 加载器配置(use方式)
{ test: /\.格式$/, use: 加载器 },				    //1个
{ test: /\.格式$/, use: [加载器,加载器] },	//多个 数组元素 

  // 没有参数的 1个或多个 加载器配置(loader方式)
{ test: /\.格式$/, loader: 加载器},			    //1个
{ test: /\.格式$/, loader: 加载器!加载器},	//多个 !叹号分隔

	// 有参数的 1个或多个 加载器配置
{ test: /\.格式$/, loader: 加载器, options:对象参数}, //1个
{ test: /\.格式$/, 
  use:[
    {loader: 加载器, options:对象参数},
    {loader: 加载器, options:对象参数},
    ...
  ]
}, //多个
```



# Loader

### 应用less文件

1. 创建 src/css/2.less 文件 和 简单的样式内容

   ```css
   /*给li设置border边框*/
   ul{
     li{border:2px solid green;}
   }
   ```
   

   
2. 在 src/main.js 中import引入less文件

   现在实时打包终端窗口报错

   > 错误原因：less文件缺少处理的loader



### 安装使用loader

`步骤`：

1. 安装相关loader依赖包  yarn  add -D  less-loader  less

2. webpack.config.js做如下配置：

   ```js
   module.exports = {
       // 给webpack配置各种loader
     module: {
       rules: [
         {
           // 3) less之loader配置
           test: /\.less$/,
           use:['style-loader','css-loader','less-loader']
         }
       ]
     }
   }
   ```

   现在重启服务(npm run serve)，发现less样式已经生效




`注意`：

1. rules是一个组别，里边可以为不同类型文件配置对应的loader
2. style-loader、css-loader、less-loader需要一并配置，并且它们有严格的**前后设置顺序**，不能颠倒，而执行顺序恰好相反，less-loader第一个，css-loader第二个，style-loader是第三个



### loader解读

`各自作用`：

​	less-loader：处理less内容为css内容，css内容再交给css-loader和style-loader处理

​	css-loader   :该loader可以实现在主入口main.js文件中以import/require的方式引入css (less)

​	style-loader ：该loader可以实现在html运行文档中以style标签的形式嵌入css 内容



`原理`：

1. less文件内容被less-loader转变为普通css内容，并嵌入到打包文件(dist/bundle.js)中
2. bundle.js文件会创建一个**style标签**，并植入到应用html文档中，使得css(less)样式生效



## es6

`步骤`：

1. 在src/main.js中设置 let、箭头函数 等es6高级语法内容

   ```js
   // 应用es6高级语法(let、箭头函数、反勾号字符串设置等等)
   let city = 'beijing'
   let getInfo = ()=>{
     return 'abc'
   }
   let str = `I like ${city}`
   ```

   

2. 物理打包  npm run build，查看bundle.js文件，发现es6高级内容**没有做降级**处理(这样各个浏览器访问的时候会出现问题，尤其是低版本浏览器不能很好运行es6内容)



`注意`：

​	我们以es6作为主要讲解目标，原理上也可以使用es7、es8等，它们都是高级语法



### babel-loader&preset&plugin关系

不同类型文件在webpack中都有不同的loader做解析处理，es6高级标准对应loader的名称为“**babel-loader**”，单这个loader也不做具体事宜



`它们的关系`：

webpack:是大老板

​	babel-loader：二级承包商，负责找到preset干活

​		preset：对常用plugin做封装，方便安装使用，是三级承包商，负责找到plugin干活

​			plugin：每个es6高标准技术都对应一个plugin做降级处理，最底层苦力



在webpack中，不同类型的es6高级语法做降级处理都有**独立的工具**做编译转换处理，这个工具称为plugin

例如：

> let 有独立的plugin做降级
>
> ``字符串 有独立的plugin降级
>
> 箭头函数  有独立的plugin降级
>
> 这样一个项目如果使用多种类型的es6高级语法，势必需要安装配置许多plugin，比较繁琐，前辈针对该情况已经有解决方案
>
> 有preset机制，preset是针对许多“常用”plugin的集合，这样只需要安装配置preset一个依赖包就可以降级许多es6高级语法



`注意`：

​	webpack本身有功能扩展插件plugin，例如html-webpack-plugin

​	babel-loader也有plugin的概念

​	它们各说各的，彼此没有关系



### 安装配置loader和preset

babel-loader的官网：https://babel.docschina.org/

`步骤`：

1. 安装依赖包  yarn add -D  babel-loader @babel/core @babel/preset-env

2. webpack.config.js中配置loader，具体如下

   ```js
   module.exports = {
     module: {
       rules: [
         {
           //4) 处理es6高级语法的loader配置
           test: /\.js$/, // 匹配js文件，交给如下loader处理
           exclude: /node_modules/, // 排除指定目录不处理
           use: 'babel-loader',
         }
       ]
     }
   }
   ```

   > (此时：webpack已经可以找到loader了)

3. 在项目**根目录**创建babel.config.js文件，里边配置如下内容：

   (作用：使得babel-loader 可以找到preset 对代码做降级处理)

   ```js
   // 配置，使得babel-loader可以找到preset
   //       preset可以找到plugin
   module.exports = {
     presets: ['@babel/preset-env']
   }
   ```

   > 现在给项目重新做物理打包( npm run build)，发现dist/bundle.js文件内容针对es6高级内容已经做降级处理了



`注意`：

1. 一共要安装3个功能包

   > babel-loader 
   >
   > @babel/core 是内部依赖
   >
   > @babel/preset-env是许多常用plugin的集合
   >
   > @符号就是普通名字组成部分而已

  2. babel-loader找到preset有3种方式
     a.     webpack.config.js配置文件
     b.     .babelrc配置文件
     c.     babel.config.js 配置文件 【 推荐】使用

## ttf字体

`步骤`：

1. public/index.html 创建p标签和显示内容

2. 复制字体库文件到项目指定目录  src/fonts/STCAIYUN.TTF

3. 在src/css/1.css文件中引入字体库、应用字体库，具体如下

   ```css
   /*给p标签内容设置指定的字体库*/
   /*定义一个字体库*/
   @font-face{
     font-family: 'cai';
     src:url('../font/STCAIYUN.TTF');
   }
   /*页面元素应用字体库*/
   p{font-family: 'cai'}
   ```
   
现在实时打包窗口报错
   
提示，ttf字体库文件缺少对应的处理loader
   



`注意`：

1. 可以到自己电脑的  C:\Windows\Fonts  目录获取要使用的字体库文件




### 配置loader

`步骤`：

1. 在webpack.config.js中为字体库文件配置loader，具体如下：

   ```js
   module.exports = {
     module: {
       rules: [
         {
           //5) 处理字体库文件 的loader配置
           test:/\.(ttf|eot|otf|woff|svg)$/i,
           loader: 'url-loader',
           options: {
             limit: 10000, // 10k大小的阀值
             outputPath: 'fonts' // 为存储生成的字体库文件设置子级目录
           }
         },
       ]
     }
   }
   ```

2. 现在做实时打包，npm run build，字体库应用成功

`原理`：

 1. 大字体库文件，会被file-loader解析处理，在dist/font目录重新生成出来，并重新起名字

 2. 小字体库文件，会被url-loader解析处理变为base64格式字符串，直接嵌入到 dist/bundle.js 文件中，并以style标签方式植入的应用程序文档(dist/index.html)中

    > 一般的字体库文件大小都是好几M的，因此小字体库文件处理原理可以忽略



`注意`：

1. ttf等字体库文件需要的loader 与 img图片的一样，就是url-loader和file-loader
2. url-loader配置limit和outputPath参数
3. 字体库文件格式有许多，例如 ttf、eot、woff、svg等
4. font-face可以通过多个字体库文件定义多个



# @别名和默认后缀

`步骤`：

1. 在之前的VueCLI脚手架项目中执行 指令  vue inspect > output.js (获得webpack的相关配置信息)

   那么系统根目录就生成**output.js**文件，查看可以**找到** @别名 和 后缀名 设置语法

2. webpack.config.js文件中做如下配置

   ```js
   const ph = require('path')
   module.exports = {
     resolve: {
       alias: {
         // 配置别名
         '@': ph.resolve('./src'),
       },
       // 配置自动识别后缀名
       extensions: [
         '.js',
         '.vue',
         '.json',
         '.css',
         '.less'
       ],
     },
   }
   ```

   > 现在在src/main.js中就可以使用@符号，代表src目录绝对路径名,被引入各种类型文件的后缀名字也可以**省略**了




`注意`：

项目中应用程序文件的彼此引入操作并不都是在src/main.js中进行的，有的时候许多目录层次很深的文件也要对其他文件进行引入，使用@符号会极大方便项目的开发，方便文件移植



# Vue

`安装`：

```
yarn add vue
```



依赖包、模块

> yarn add 依赖包
>
> 一个依赖包里边包含多个模块
>
> 模块就是一个js文件，内部有执行**模块化导出**动作，例如module.exports  或 export default {}



## 模块说明

vue不同模块类型

> 1. vue.common.js，基于CommonJS模块化构建的 module.exports = Vue
>
> 2. vue.esm.js，基于ES6模块化构建的 export default Vue
>
> 3. vue.runtime.js，删减版vue的体现，把相同功能的多余实现方式给删除掉
>
> ​								内部只有render，没有template
>
> 4. vue.js、 vue.min.js，通用型的，在浏览器上可以直接使用，完整版的
>
> ​								template和render都存在，一个都不少



各种应用情形

1. 浏览器端可以使用  vue.js  或 vue.min.js
2. nodejs中可以使用vue.common.js或vue.runtime.common.js(nodejs没有使用vue的必要)
3. webpack中使用分为两种情形：
   1. 普通容器渲染(new Vue({el:'xxx'}))，要使用**不带runtime**系列的(el要通过template渲染实现)
   2. el+render方法渲染的，全部模块都可以使用



## 应用

`步骤`：

1. 在public/index.html中设置div容器，并输出data数据

   ```html
     <div id="app">
       {{ msg }}
     </div>
   ```
   

   
2. 在src/main.js中 引入Vue、并实例化对象

   ```js
   // 1. 引入Vue模块
   import Vue from 'vue/dist/vue.common.js'
   // 2. 实例化Vue对象
   var vm = new Vue({
     el:'#app',
     data:{
       msg:'hello'
     }
   })
   ```
   
> 注意：如果Vue实例内部没有render，请引入完整版的vue，不要使用runtime的



`注意`：

1. import Vue from 'vue/dist/vue.common.js'   // 引入完整版的vue  ，适合el渲染容器应用
2. import Vue from 'vue'  // 引入删减版的Vue，即vue/dist/vue.runtime.common.js  适合el+render方法渲染容器应用
3. 虽然 div容器 和 new Vue() 代码放到两个文件中，但是不影响实际运行效果，因为经过  npm run build  打包后，它们就**合体**了，new Vue()   的内容就被融入到   div容器  所在的运行文档里边了



## 应用单文件组件

`步骤`：

1. 创建src/App.vue单文件组件，并设置h2标签内容

   ```html
   <template>
     <div>
       <h2>
         我是App根基组件
       </h2>
     </div
   </template>
   ```
   

   
2. 在src/main.js中直接引入vue模块，再引入App组件，Vue实例内部通过render对指定的App组件进行渲染操作

   ```js
   // 1. 引入vue模块,具体是删减版的
   import Vue from 'vue'
   // 2. 引入App根基组件模块
   import App from '@/App'
   
   var vm = new Vue({
     el:'#app',
     data:{
       msg:'hello'
     },
     // 3. 通过render成员方法，使得App根基组件内容对div容器进行覆盖渲染
     //render:function(h){
     //	return h(App)
     //}
     render:h=>h(App)
   })
   ```
   
> 此时，实时打包终端窗口报错，提示vue文件需要对应的loader做处理




`注意`：

1. render方法可以使得组件内容对**div容器**进行**覆盖渲染**
2. 实际项目中，div#app就是一个空容器，不设置任何内容，命运就是被一个指定的组件(一般是App.vue)覆盖的，然后在App.vue里边构建其他业务
3. 因为当前环境是 el+render模式，所以就使用默认的vue即可



## 单文件组件配置loader

1. 安装依赖包 yarn add -D  vue-loader vue-template-compiler

2. 在webpack.config.js中做如下配置：

   ```js
     // vue-loader相关配合使用的模块
     const VueLoaderPlugin = require('vue-loader/lib/plugin'); 
   
     module.exports = {
       module: {
         rules: [
           {
             // 6) vue文件对应的loader配置
             test: /\.vue$/,
             loader: 'vue-loader'
           },
         ]
       }
     }
   
     plugins: [
       // vue-loader配置的功能插件
       // 我们之前有为不同类型文件配置过许多loader(css/less/img/js等等)，
       // 现在把下边语句设置好,作用是：各种loader针对单文件组件内部也是生效的
       // 并且 vue组件内部 的img标签 和 background-image 图片都可以被loader处理
       new VueLoaderPlugin(),
     ]
   ```
   
> 现在重启实时打包 npm run serve,发现App.vue组件已经把div#app容器给覆盖并显示了




`注意`：

1. 在vue单文件组件内部设置的css、less、img、es6高级语法、背景图片/img标签图片 都会被相关的loader做处理

2. vue-loader：针对vue单文件组件做转码、降级处理，使得编译后的内容可以被浏览器直接运行，vue组件是特殊类型文件，当然需要loader处理



## 组件案例

`步骤`：

1. 创建目录src/views，在该目录创建3个组件文件(Home.vue、Movie.vue、Music.vue)，设置简单示意内容即可

2. 安装路由 yarn add vue-router

3. 创建路由配置文件 src/router.js，内容如下

   ```js
   // 引入Vue
   import Vue from 'vue'
   // 引入路由
   import VueRouter from 'vue-router'
   
   // 给Vue注册路由组件(router-link/router-view)
   Vue.use(VueRouter)
   
   // 创建路由对象
   export default new VueRouter({
     routes:[
       // 锚点 和 路由关系
       {path:'/',redirect:'/home'},
       {path:'/home', component:()=>import('@/views/Home')},
       {path:'/movie', component:()=>import('@/views/Movie')},
       {path:'/music', component:()=>import('@/views/Music')},
     ]
   })
   ```
   
   > 上述 import() 是函数调用  (非模块化导入动作)
   
4. src/main.js主入口文件导入路由、并挂载

   ```js
   import Vue from 'vue'
   import App from '@/App'
   
   import router from './router' // 导入路由对象
   
   var vm = new Vue({
     router, // 挂载路由
     el:'#app',
     render:h=>h(App)
   })
   ```
   

   
5. src/App.vue根基组件中设置路由标签 和 显示组件占位符

   ```html
   <template>
       <div>
         <h2>App根组件</h2>
         <p id="btn">
           <!--单击按钮-->
           <router-link to="/home">首页</router-link>
           <router-link to="/movie">电影</router-link>
           <router-link to="/music">音乐</router-link>
         </p>
         <p id="cont">
           <!--业务组件显示占位符-->
           <router-view></router-view>
         </p>
       </div>
   </template>
   
   <script>
   export default {
     name: 'App'
   }
   </script>
   
   <style lang="less" scoped>
   div{
     #btn{
       width: 400px;
       height: 50px;
       background-color:pink;
       .router-link-active{background-color: orange;}
     }
     #cont{
       width: 400px;
       height: 200px;
       border:2px solid blue;
     }
   }
   </style>
   ```
   
   > 现在单击标签  切换显示组件效果已经呈现




`注意`：

1. src/router.js的内容可以完全挪到src/main.js中，但是这样会使得main.js文件内容比较凌乱
2. 虽然 main.js 和 router.js 中对Vue都有引入，但是系统运行时，它们是同**一个路由对象**
