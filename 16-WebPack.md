WebPack

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

    > 一般的字体库文件大小都是好几M的，因此小字体库文件处理原	理可以忽略



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



# WebPack安装使用



## 问题

第一个问题：

一个网站页面打开后，里边的请求资源很多(img/js/css等)，有可能达到数十至上百个，
有的资源本身很小，但是也需要进行一次http网络请求，并且http协议的**开启**和**关闭**所耗费的资源比文件本身都大很多，形成了喧宾夺主、不划算的效果



第二个问题：

项目开发过程中会使用各种语言
① html、JavaScript、css 通用语言技术
② less、scss高级css语言技术
③ ES6(es2015)、ES7(es2016)、typescript(js的超集) ，javascript高级标准 (es2019)

以上 ② 和 ③ 高级技术可以开发使用，但是不能直接用于生产，相反要通过指定的编译器做[转码]()或[降级]()处理才可以在所有浏览器上运行，各个高级技术逐个做编译处理是一件繁琐、效率低下的工作



## 什么是webpack

WebPack可以看做是模块**打包机器**,它做的事情是，分析你的项目结构，
找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言
（less、es6、es7等），**一次性**将它们打包为合适的格式以供**所有浏览器**使用。



## 作用

1. 打包文件

   > 一次网络服务可能需要发送多个http请求，
   >
   > 请求的开启、关闭消耗的资源有可能比内容本身更消耗资源，
   >
   > 这样默认如把许多内容都打包为一个文件，做一次http请求更划算

2. 编译转码、降级高级技术标准为普通或通用的

   > 编译less、scss、typescript为浏览器可以运行的普通内容
   >
   > 降级es6、es7为es5或更低标准，使得代码的兼容性更好

3. 编译图片为base64格式 字符串，减少网络请求次数



## 安装webpack并使用

webpack 是前端的一个开发工具，可以从NPM官网上下载使用；
官网：
https://webpack.docschina.org/

### 安装

运行命令

```
yarn add -D webpack webpack-cli
```

> 安装webpack 和 webpack-cli两个包，webpack-cli是webpack的内部依赖
>
> -D 表示通过`开发依赖`形式安装webpack  ，yarn的全称为 --dev (npm 全称为 --save-dev)



### 配置指令

打开 `package.json`文件，在 scripts 节点中，新增名称为 pack 的成员：

```javascript
"scripts": {
  "build": "webpack"
}
```



现在就可以通过如下命令运行webpack了

```
npm run build
```



### jquery的设置

src/index.js文件中引入jquery并做隔行代码设置：

```javascript
// ES6模块化方式导入jquery
import $ from 'jquery'

$(function(){
  $('li:odd').css('background-color','lightgreen')
})
```

> src/index.js是两个文件内容的体现，本身还包括jquery



### 打包

终端执行如下命令，使得webpack可以对src/index.js文件内容做打包处理

```javascript
npm run build
```



打包后的效果，可以看到项目根目录自动生成dist/main.js文件，

其是 **jquery** 和 **隔行代码** 的集中打包体现：

src/index.js   ==============>  dist/main.js

> src  、dist  或 main.js 等名称后期通过配置可以更改为其他



### 应用

现在在`src/index.html`应用中**不用**引入jquery和index.js文件，直接引入打包好的main.js就可以

```html
<!-- <script src="../node_modules/jquery/dist/jquery.js"></script> -->
<!-- <script src="./index.js"></script> -->
<script src="../dist/main.js"></script>			// 直接引入dist/main.js
```



注意：

> index.js 和 index.html 文件必须放到**src**目录中，因为webpack默认会操作该目录并找对应文件
>
> dist/main.js是webpack执行过程中自动创建的(通过配置可以修改，这是后话)

## 小结

- webpack具备**打包**、**编译**、降级代码功能等多重功能
- webpack需要同时安装**webpack**和**webpack-cli**两个功能包
- webpack打包好的文件默认放到**dist**目录，可以配置为其他
- 在**package.json**文件中配置指令，使得webpack可以运行



## 运行和开发依赖

依赖包的安装分为两种方式：开发 和 运行

- 依赖包在项目生产中充当**工具**作用的，建议通过开发依赖方式安装，例如webpack
- 依赖包在项目生产完毕**上线后都需要**使用的，就通过运行依赖方式安装，例如jquery



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
yarn add --save-dev  webpack
```

问：依赖包如何区分是**开发的**还是**运行的**：
答：在 src/index.js 入口文件中通过require(或es6 import)引入的就是运行依赖包，否则是开发依赖包



运行依赖和开发依赖包会分别配置到package.json的  **dependencies**和 **devdependencies** 段里边



我们通过软件仓库获得到别人开发的项目代码，如果还需要二次开发，就执行如下指令安装依赖包，其表示要安装<font color=red>全部</font>的依赖包(运行的和开发的)

```
yarn
```

如果只是运行别人的项目，不做二次开发，就执行如下指令，表示只安装<font color=red>运行</font>依赖包(去除了不用的开发依赖包，**缩减了项目体积**，转而运行更快了)

```
yarn --production
```

> vue环境里边 开发、运行 依赖的效果不能体现
>
> nodejs中体现的更好



## webpack配置

### 打包模式

webpack首次运行打包后会产生下图的**警告**信息(原因是没有设置使用模式)，使得页面提示不是很友好，可以通过配置给消除(原因是没有设置**打包模式**)



在项目**根目录**中，新建一个 [webpack.config.js]() 配置文件，内容如下



```javascript
module.exports = {
  mode: 'production'    // production    development
}
```

> 这是 使用 Node 语法， 向外导出一个 配置对象
> production：打包的dist/main.js文件是优化、压缩的
> development：打包的dist/main.js文件有适当的空白、换行、注释，可读性好



### 入口和出口配置

默认情况：

webpack的**入口**和**出口**文件分别是  src/index.js 和 dist/main.js

如果有需要，可以对以上路径名进行修改



在[webpack.config.js]() 配置文件中也可以给其他参数做配置

```javascript
module.exports = {
  entry: 'xxx',		//被打包的文件
  output:{
    path:'xxx',		//打包文件输出目录
    filename:'xxx',	//打包文件的名字
  }
}

```

> entry：配置入口文件
>
> output：配置出口 目录和文件



例如：

```js
const path = require('path')
module.exports = {
  entry: path.resolve('./src/index.js'),		//被打包的文件
  output:{
    path:path.resolve('./dist'),			//打包文件输出目录
    filename: 'bundle.js'				//打包文件的名字
  }
}
```

> path.resolve('./src/index.js.')					// E:\Vue40\every_day\03day\Code\01-webpack\src\index.js
>
> path.join(__dirname,  './src/index.js')     // E:\Vue40\every_day\03day\Code\01-webpack\src\index.js
>
> resolve较比join更加方便，其**不用**设置__dirname，也可以根据相对路径拼装出一个绝对路径



## 构建模板页面

webpack默认情况下只对src/index.js文件打包，完毕后在html应用文件中手动引入使用，不够智能。

现在目标：

webpack打包src/index.js文件的同时也要去**打包** src/index.html 模板文件，并**生成**在 dist/index.html，同时**自动引入**对应的js出口文件



有一个名称为**html-webpack-plugin**的插件，可以帮助我们把html模板文件也打包到dist目录去，并在其中

**自动引入**js打包文件，然后dist/index.html就可以直接用于生产使用了

[参考官网](https://webpack.docschina.org/plugins/html-webpack-plugin)：



### 装包

运行指令装包

```javascript
yarn add html-webpack-plugin -D
```



### 去除js文件引入

在src/index.html中不需要引入任何js文件，打包后会**自动**引入

```html
  <!-- <script src="../node_modules/jquery/dist/jquery.min.js"></script> -->
  <!-- <script src="./index.js"></script> -->
  <!-- <script src="../dist/bundle.js"></script> -->
```



### 给webpack配置插件

在 [webpack.config.js]()中，导入 html-webpack-plugin 插件：

同时，把这个插件配置给plugins项目

```javascript
const  HtmlWebpackPlugin  =  require('html-webpack-plugin')
plugins:  [
  new  HtmlWebpackPlugin({
    template:  'xxx'  // 被打包的html母模板文件路径名
  })
]
```

例如

```js
plugins: [
  new HtmlWebpackPlugin({
    // 设置被打包的html母模板文件路径名
    template: path.join(__dirname, './src/index.html')
  })
]
```



## 实时打包

现在 src/index.js和 src/index.html 都可以做打包处理了，但是有一个问题，就是当源码文件发生变动时，就需要重新打包才可以看到效果，这样工作效率比较低下。

webpack有一个名称为 **webpack-dev-sever** 工具，

这个工具可以**实时**处理js、**实时**处理html模板、**实时**编译查看效果，显著提高开发效率

> 这个工具安装配置好后，随时修改源码文件随时在浏览器上看效果，不用反复打包

### 装包

运行指令：

```
yarn add webpack-dev-server -D
```



### 参数配置

[配置参考](https://webpack.docschina.org/configuration/dev-server/)

在[webpack.config.js]()里边给webpack-dev-server配置运行参数

```javascript
// 给实时打包工具webpack-dev-server做相关配置
devServer: {
  port: 1024, // 实时http服务端口配置
  host: '127.0.0.1', // 实时http服务主机ip地址配置
  open: true, // 自动启动浏览器并呈现相关效果
  compress: true // 以压缩方式传输网络内容
}
```



### 启动指令

打开并配置package.json文件：

```javascript
"scripts": {
  "serve": "webpack-dev-server"
}
```



现在使用如下指令就可以运行webpack-dev-server了

```javascript
npm run serve
```

> 上述npm run  serve 是一个前台进程，终端窗口不能关闭，否则没有效果

现在 src/index.html 和 src/index.js  文件 可以实现随时修改随时看效果功能了

注意

- 实时打包文件内容以**内存**形式提供(不会生成dist物理目录和文件)，并通过**/根目录**形式被访问



## 小结

1. webpack通过配置文件**webpack.config.js**可以配置打包模式、入口和出口文件

2. 给webpack安装配置html-webpack-plugin插件可以**同时打包**html模板文件，同时html打包好的文件会自动引入js出口文件

3. 给webpack安装配置webpack-dev-server工具包可以实现**实时**打包并**查看**效果

    

# WebPack具体打包处理

### 运行css步骤

1. 创建css文件和内容 相关

2. 项目主入口文件引入css

3. 在线实时打包运行

   错误原因：当前的webpack环境中，还不能对**css内容**进行识别



### 什么是loader

webpack本身就是一个**打包机器**，其不能对具体代码内容部分进行**处理**(或处理得非常有限)，不同的代码内容(less/scss/ES6(ES7)/image/css等等)需要webpack找到不同的**loader**(装载器)实现转码、编译、降级处理。



loader就是webpack手下的**小兵**(本质是javascript函数)，帮助webpack处理编译不同类型的内容，webpack打包过程中，遇到不同类型文件内容就会寻找对应loader处理



处理不同内容的loader：

| 不同内容 | loader处理器                                     |
| -------- | ------------------------------------------------ |
| css      | style-loader 和 css-loader                       |
| less     | less-loader 和 less(less是less-loader的内部依赖) |
| 图片     | url-loader 和 file-loader                        |
| ttf      | url-loader                                       |
| ES6/ES7  | babel-loader                                     |
| ...      | ...                                              |

[各种loader参考](https://webpack.docschina.org/loaders/)



### 安装处理css的loader

运行指令(通过开发依赖模式安装依赖包)

```javascript
yarn add style-loader css-loader -D
```

> 处理css内容需要两个loader配合使用 style-loader css-loader
> css-loader   :该loader可以实现在主入口js文件中以import/require的方式引入css 
> style-loader ：该loader可以实现在html文档中以style标签的形式嵌入css



### 配置loader

打开 [webpack.config.js]() 配置文件，在 module -> rules 数组中，新增处理 css 样式表的loader规则：

```javascript
module: { 
  // 制定各种类型文件的处理规则
  rules: [ 
    // css后缀文件loader匹配
    { test: /\.css$/, use: ['style-loader', 'css-loader'] }
  ]
}
```

> 先配置style-loader、再配置css-loader，有严格的顺序要求，执行的时候是先css-loader然后style-loader

现在css内容就可以正常打包处理了



注意：配置文件修改了，需要**重启**webpack或webpack-dev-server (npm run serve 或 npm run build)



给webpack做loader配置的其他格式参考：

```javascript
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



### 打包好的css在哪

css的文件内容最终会被打包进 dist/bundle.js 出口文件中，浏览器运行就可以看到效果

 (原理：css效果是通过style标签体现出来，bundle.js执行的时候会自动创建style标签和样式)

> 执行一次`npm run build` **物理**打包操作，会发现css样式内容被打包到bundle.js文件文件中



### 安装loader

在css中给元素设置背景图片，这个图片文件需要通过url-loader处理

运行指令：

```javascript
yarn add file-loader url-loader -D

```

> file-loader是url-loader的内部依赖也需要一并安装



### 配置loader

在 [webpack.config.js]() 的配置文件中，新增一个 rules 规则来 处理 img图片 文件

```javascript
{
  // css样式中图片的处理loader设置
  test: /\.(png|jpg|gif)$/,
  use: [
    {
      loader: 'url-loader',
      options: {
        limit: 8192
      }
    }
  ]
}
```

> file-loader是url-loader的内部依赖模块，不需要设置
>
> 使用 url-loader, 它接受一个 limit 参数，单位为字节(byte)

`options/limit`  是给url-loader设置大小<font color=red>阈值</font>(8192字节=8k)

被处理的图片大小"小于等于"8192,那么就给其转码为<font color=red>base64字符串</font>格式图片，该格式图片可以嵌入到css样式文档中形成图片效果，好处是节省了http请求资源消耗，

否则就调用file-loader形成一个新的物理图片文件，在网络上有独立的http请求



### 在线实时运行

1. 生成物理图片
2. 生成base64字符串格式图片



经过上述步骤，现在进行实时打包，通过浏览器源代码可见：

- 大图被重新创建出来，并给重命名了
- 小图是通过**字符串**方式体现



### base64格式字符串

计算机里边每个文件都是通过”二进制码“组成的，包括图片

问：什么是base64格式图片？

答：Base64就是一种基于**64个可打印**字符来**表示二进制数据**的方法。 

一个图片可以变为二进制数据，该数据再编码为base64格式

 

[base64说明](https://www.imooc.com/article/27804)

问：什么样子的图片适合变为字符串形式显示？

答：网络中，每一个图片相当于一次http请求，图片多了的话，性能损失比较严重。
而将图片转化成base64格式的字符串，则极大地减少了请求数，因为base64是文本格式，可以直接放在body里。一般对于小于**10KB**大小的图片进行**base64**转码(大图片不适合做字符串转换，否则得不偿失)

(每个图片转变为base64格式后，大小都要变得大一些)



注意：

> html模板文件 中的img图片标签，**不会**被webpack处理的，只有css文件的背景图片才处理



### 图片子级目录

如果有多个图片都以物理文件形式被打包生成在dist目录，那么这个目录会显得非常凌乱，现在可以给loader做配置，使得图片生成在一个指定目录

给url-loader的options选项配置**outputPath**选项，使得在dist目录下创建子目录用于存储生成的图片

```js
{
  test: /\.(png|jpg|gif)$/i,
  use: [
    {
      loader: 'url-loader',
      options: {
        limit: 8192,
        outputPath: 'image'  // 现在做物理打包，图片就形成在dist/image目录里边了
      }
    }
  ]
}
```



## 处理less文件

创建独立的less样式文件并做引入使用

### 运行less步骤

1. 创建less文件和内容

2. 项目主入口文件引入less

3. 在线实时打包运行

   原因：缺少对应的loader处理less文件

### 安装loader

处理 less 的 webpack loader。将 Less 编译为 CSS

运行指令：

```javascript
yarn add less-loader less -D
```

> less是less-loader的依赖模块，需要一并安装



### 配置loader

在 [webpack.config.js]() 的配置文件中，新增一个 rules 规则来 处理 less 文件：

```javascript
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }
```

> 注意：
>
> ​	style-loader、css-loader、less-loader有严格的前后顺序要求
>
> ​	less-loader处理less内容为css内容，css内容再交给css-loader和style-loader处理



## 处理es6内容

### 运行es6标准内容

es6:  箭头函数、let、解构赋值、...扩展运算符、反单引号字符串等等

通过es6高标准技术实现项目开发

在src/index.js入口文件中声明使用es6标准内容



结果：es6的标准代码打包**前后**没有变化，与预期不相符(webpack应该**降级**es6/es7为es5标准)

打包好的代码兼容性差，只能在主流前沿浏览器中运行，低版本浏览器有可能就运行失败了



### babel-loader介绍

webpack是打包工具，不是代码转换工具，具体转换工作需要交给loader去做(不同的内容对应不同loader，css-loader  less-loader file-loader等)，如果开发者使用了es6或es7语法，为了各种浏览器都可以识别提升兼容性，就需要降级为es5标准，用于降级es6或es7的loader名称为**babel-loader**

在webpack官网可以找到处理es6高标准的babel-loader



babel是一个JS编译器，用来转换最新的JS语法，比如把ES6, ES7等语法转化成ES5语法，从而能够在大部分浏览器中运行。像箭头函数、let变量、反单引号字符串等，都可以转换。



[babel官网](https://babel.docschina.org)

在处理高级JS语法(ES6/ES7)的时候，webpack去寻找babel-loader，babel-loader自己不干活，具体交给plugin插件处理，不同es6/es7的语法对应不同的plugin转码，逐一安装使用太过繁琐，这时候**preset**出现了，其是一组**常用plugin**的集合，方便plugin的安装使用，提升开发效率(如果遇到冷门的es6语法，preset有可能处理不了，这时候再安装具体plugin处理即可)



### 安装loader

运行指令：

```javascript
yarn add babel-loader @babel/core @babel/preset-env -D

```

> 一共要安装3个模块
>
> @babel/core是内部依赖
>
> @babel-preset-env是许多常用plugin的集合



### 配置loader

在 [webpack.config.js]() 的配置文件中，新增一个 rules 规则来 处理 es6高级语法内容

```javascript
{
  // 通过loader对js文件中的es6/es7高标准进行降级处理，处理为es5
  test: /\.js$/,
  exclude: /node_modules/,
  use: 'babel-loader'
}

```

> exclude：设置表示对应目录不要经过babel-loader处理

配置示例：



在项目**根目录**创建[babel.config.js]()文件做如下配置

```javascript
module.exports = {
  presets : ['@babel/preset-env'],
}

```

> 作用：使得babel-loader找到preset插件集合帮忙处理es6/es7内容



### 应用

在入口文件中添加各种es6高级语法内容

```javascript
// 通过es6标准编写js代码
// 1) 箭头函数
var getInfo = ()=>{
  console.log('正在学习loader使用');
}
getInfo()

// 2) 解构赋值
const {name,number:num} = {name:'front62',number:75}
console.log(name,num);

// 3) let使用
let address="顺义"

// 4) 字符串拼装
var weather="晴朗"
console.log(`今天的天气情况：${weather}`);
```

之后webpack进行打包处理（npm run build），在dist/bundle.js打包文件中查看babel-loader/preset对es6内容的降级处理效果



## 处理ttf文件

`步骤`：

1. 设置字体库文件

   src/font/STCAIYUN.TTF

2. 在src/index.html中设置被操作p标签目标

   ```html
   <p>秋侵人影瘦，霜染菊花肥</p>
   ```

3. 在 src/css/1.css中设置p标签使用字体库文件

   ```css
   /*定义一个字体库*/
   @font-face{
     font-family: 'cai';
     src:url('../font/STCAIYUN.TTF');
   }
   /*页面元素应用字体库*/
   p{font-family: 'cai'}
   ```

   > 此时实时打包服务操作终端会提示字体库文件缺少对应的loader

4. 配置使用url-loader

   ```js
   module: { 
     // 制定各种类型文件的处理规则
     rules: [ 
       {
         //5) 处理字体库文件 的loader配置
         test:/\.(ttf|ttc|otf|woff)$/i,
         loader: 'url-loader',
         options: {
           limit: 10000, // 10k大小的阀值
           outputPath: 'fonts' // 为存储生成的字体库文件设置子级目录
         }
       }
     ]
   }
   ```
   
> 处理字体库文件的loader与img图片的都一样，都是url-loader，并且条件满足会自动调用file-loader
   >
   > 现在字体库文件正常生效了



## @别名和默认后缀

脚手架搭建的项目，都会配置**@符号别名**，代表src的绝对目录信息，以方便其他文件引入

同时还可以给常用文件配置**后缀名**，使得文件引入可以省略设置，提高开发速度

如果有需要，可以在webpack.config.js中做如下配置：

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
      '.css'
    ],
  },
}
```

## 小结

1. 处理css文件的loader有两个：  

   css-loader：允许入口文件通过模块化方式引入css文件

   style-loader：把css样式内容通过style标签嵌入到html文档中

2. 处理image图片的loader有两个：

   url-loader：把比较小的图片变为字符串

   file-loader：大图片重新编译生成处理

3. 处理less文件的loader有3个

   less-loader(less)：把less的内容编译转码为css内容

   style-loader、css-loader

4. es6/es7降级处理

   babel-loader：自己不干活，找preset处理

   preset：自己不干活，找plugin处理

   plugin：针对不同类型的高标准内容做降级处理



# webpack中配置使用vue

## 安装vue

运行指令 

```javascript
yarn add vue
```

vue各个文件名称说明：

> vue.common.js                    //  基于 CommonJS 的模块构建
> vue.esm.js            				//  基于 ES6 Module 的模块构建
> vue.js                                    //  基于 通用性 的模块构建，根据使用情形灵活调用不同类型模块构建
>
> ​												// 在浏览器、node中均可以使用
>
> vue.min.js                            // 和 vue.js 一样, 属于压缩后版本
> vue.runtime.common.js   //  基于 CommonJS 的运行时构建[删减版本]
> vue.runtime.esm.js           //  基于 ES Module 的运行时构建[删减版本]
> vue.runtime.js                   //  基于 UMD 的运行时构建[删减版本]
> vue.runtime.min.js           //和 vue.runtime.js 一样, 属于压缩后版本[删减版本]

runtime：运行时意思，是**删减版**，本身有功能缺失，但是不致命，相同的功能有多种实现，在删减版中只保留一种，好处是运行快、耗费资源少

各种应用情形

1. 浏览器端可以使用  vue.js  或 vue.min.js
2. node中可以使用vue.common.js或vue.runtime.common.js
3. webpack中使用分为两种情形：
   1. 普通容器渲染(new Vue({el:'xxx'}))，要使用不带runtime系列的
   2. render方法渲染的，均可以使用



## vue包说明

原因： 

默认情况下，使用 import 直接导入的 vue 模块，并不是功能最全的 vue 包；而是runtime删减版的；

删减版的 vue 包中功能很少(关于容器渲染只支持render函数方式)



如何让 import 导入最全的 vue 包呢？

答：

```javascript
import Vue from 'vue' 
```

改写为 

```javascript
import Vue from 'vue/dist/vue.min.js'
```

注意：在学习阶段，可以暂时 import 最全的 vue 包；后期开发项目的时候，要使用 删减版的 (因为有应用render函数), 好处是节省资源



## 处理单文件组件

.vue单文件组件本质上与css、img、less等都是属于特定类型内容，要想webpack可以打包处理也需要找到对应的加载器，处理vue单文件组件的加载器名称为 ”**vue-loader**“ ，请先**安装**和**配置**

### 安装

运行指令，安装vue-loader

```javascript
yarn add -D vue-loader vue-template-compiler
```

> vue-template_compiler是vue-loader的依赖，必须一并安装，否则vue-loader无效



### 配置

在webpack.config.js文件中，添加rules匹配规则，使得.vue单文件组件可以被loader解析处理

```javascript
// webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  module: {
    rules: [
      // ... 其它规则
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      }
    ]
  },
  plugins: [
    // 请确保引入这个插件！
    new VueLoaderPlugin()
  ]
}
```

> webpack配置文件修改后都需要重启服务

> rules:使得vue文件可以被vue-loader处理
>
> VueLoaderPlugin：使得各种loader也能针对vue单文件组件内容起作用，例如style-loader处理css内容、less-loader处理less内容、url-loader处理图片内容、babel-loader处理es6/es7内容等



# VueCLI

在VueClI3版本的脚手架项目中，可以在项目根目录下通过如下指令，查看全部的的webpack配置信息

```
vue inspect > output.js				// 查看全部webpack配置信息
```

> 如上指令执行完毕，会在项目根目录下生成output.js文件，内容就是默认的webpack配置信息



# yarn

什么是yarn

> 快速、可靠、安全的依赖管理工具。
>
> Yarn是由Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具 ，正如官方文档中写的，Yarn 是为了弥补 npm 的一些缺陷而出现的



与npm的主要区别

> yarn安装更快，会同时安装多个，而npm按照队列一个一个顺序安装，必须等到当前的包安装完毕后才能去安装下一个



安装步骤：

```
npm i -g yarn    // 全局方式安装yarn
```

> yarn --version   // 可以查看安装好的yarn的具体版本号码



给yarn配置taobao镜像

```
yarn config set registry https://registry.npm.taobao.org		// 配置为taobao的镜像源
```

> yarn config get registry				// 查看当前使用的源
>
> 镜像：外国npm服务器的全部资源被定期复制到中国服务器，以方便中国用户就近下载相关的资源，这个中国服务器就是“镜像”



yarn与npm针对各个指令的执行

|    **对比**    |         **yarn**          |          **npm**          |
| :------------: | :-----------------------: | :-----------------------: |
|     初始化     |       yarn init -y        |        npm init -y        |
|  安装全部依赖  |  yarn install 或者 yarn   |        npm install        |
|    新增依赖    |      yarn add 依赖包      |    npm install 依赖包     |
|                |    yarn add 依赖包 -D     |   npm install 依赖包 -D   |
|    删除依赖    |    yarn remove 依赖包     |   npm uninstall 依赖包    |
|    更新依赖    |       yarn upgrade        |        npm update         |
| 全局安装或删除 | yarn global remove 依赖包 |  npm uninstall 依赖包 -g  |
|  同时下载多个  |  yarn add 依赖包 依赖包   | npm install 依赖包 依赖包 |

> npm: --save-dev 和 -D 互为别名，表示通过开发依赖方式安装依赖包
>
> yarn: --dev 和 -D 互为别名，表示开发依赖
>
> yarn：global代表全局
>
> npm: -g 代表全局



相关文章

1. [vue.js 2.x 官网-国内](https://vue.docschina.org/)   或  [vue.js2.X 官网-国外](http://cn.vuejs.org)
2. [npm](https://www.npmjs.com/)
3. [饿了么组件库](http://element-cn.eleme.io/#/zh-CN)
4. [github](https://github.com/)
5. [webpack打包](https://webpack.docschina.org/)
6. [babel下一代javascript编译器](https://babel.docschina.org/)
7. [bootcdn免费提供静态内容支持](https://www.bootcdn.cn/)
8. [w3c帮助官网](http://www.w3school.com.cn)
9. [鸟哥帮助官网](http://www.runoob.com)
10. [JavaScript 指南](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide)
11. [印记中文(深入挖掘国外前端新领域，为中国 Web 前端开发人员提供优质文档！)](https://docschina.org/)
12. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
13. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)
14. [Vue开源项目汇总](https://github.com/opendigg/awesome-github-vue)
15. [Vuejs中文社区](https://www.vue-js.com)
16. [JavaScript Standard Style代码规范](https://standardjs.com/)

