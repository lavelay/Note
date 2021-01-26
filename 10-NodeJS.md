## Node.js

基于ChromeV8引擎的JS运行环境

- 代码只是具有特定格式的字符串而已
- 引擎可以认识，引擎可以解析和执行
- Google Chrome的V8引擎是目前公认的解析执行JS代码最快的引擎
- Node.js  中的JavaScript没有BOM、DOM，只有ECMAScript

**特性：**

- 可以进行文件的读写操作  
- 可以设置web服务器功能
- 可以操作数据库

1. event-driven 事件驱动
2. non-blocking I/O model 非阻塞IO模型（异步）
3. lightweight and efficient 轻量且高效



## REPL

REPL(Read Eval Print Loop:交互式解释器) 

- **读取** - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。
- **执行** - 执行输入的数据结构
- **打印** - 输出结果
- **循环** - 循环操作以上步骤直到用户两次按下 **ctrl-c** 按钮退出。



## 核心模块

> 官网文档 https://nodejs.org/dist/latest-v10.x/docs/api/
>
> 中文文档 http://nodejs.cn/api/
>

- 核心模块就是 Node 内置的模块，需要通过唯一的标识名称来进行获取。
- 每一个核心模块基本上都是暴露了一个对象，里面包含一些方法供我们使用



### fs模块

fs模块是文件操作模块。fs是 FileSystem的简写。它用来对文件，文件夹进行操作。

手册：http://nodejs.cn/api/fs.html

```js
// 引入模块。
const fs = require('fs');
```



#### 异步格式

```js
fs.readFile('文件路径'[,选项], (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

说明：

- 第一个参数：文件路径。 相对路径和绝对路径均可。
- 第二个参数： 配置项，可选参数。主要用来配置字符集。一般可设置为'utf8'

​      如果不设置该参数，文件内容会以二进制形式返回。

- 参数3: 读取完成后触发的回调函数。有两个参数 --- err 和 data

  - 读取成功

    - err: null

    - data: 不设置参数2,则返回二进制数据。可以使用 toString() 方法将二进制数据转为字符串

  - 读取失败

    - err: 错误对象
  - data: undefined



#### 同步格式

```javascript
const fs = require("fs")
let rs = fs.readFileSync('文件路径',"utf8");
console.log(rs)
```



#### 覆盖写入 writeFile

格式：`fs.writeFile(var1, var2, var3, var4);`

参数1: 要写入的文件路径 --- 相对路径和绝对路径均可，推荐使用绝对路径

参数2: 要写入文件的字符串

参数3: 配置项，设置写入的字符集，默认utf-8

参数4: 写入完成后触发的回调函数，有一个参数 --- err （错误对象）

```javascript
const fs = require('fs')
fs.writeFile('./a.txt', 'hello world niahi \n asfsdf', err => {
  if (err) {
    console.info(err)
    throw err
  }
})
```



#### 文件追加 appendFile

功能 ：向指定文件中写入字符串（追加写入）， 如果没有该文件则尝试创建该文件

格式：`fs.appendFile(var1, var2, var3, var4);`

参数1: 要写入的文件路径 --- 相对路径和绝对路径均可，推荐使用绝对路径

参数2: 要写入文件的字符串

参数3: 配置项，设置写入的字符集，默认utf-8

参数4: 写入完成后触发的回调函数，有一个参数 --- err （错误对象）

```javascript
const fs = require('fs')
fs.appendFile('./a.txt', '\n 为天地立命', err => {
  if (err) {
    console.info(err)
    throw err
  }
})
```



### 路径问题

#### \__dirname __filename 获取绝对路径

- __dirname：获取当前被执行的文件的文件夹所处的绝对路径
- __filename：获取当前被执行的文件的绝对路径



### path模块

- path.basename（路径）获取
- path.join()
- path.parse(path) 转成一个对象

```
path.basename('/foo/bar/baz/asdf/quux.html');// 返回: 'quux.html'
path.basename('/foo/bar/baz/asdf/quux.html', '.html');// 返回: 'quux'
path.dirname('/foo/bar/baz/asdf/quux');// 返回: '/foo/bar/baz/asdf'
path.extname('index.html');// 返回: '.html'
```



### 附：fs模块中的常用方法

| API                                         | 作用              | 备注           |
| ------------------------------------------- | ----------------- | -------------- |
| fs.access(path, callback)                   | 判断路径是否存在  |                |
| fs.appendFile(file, data, callback)         | 向文件中追加内容  |                |
| fs.copyFile(src, callback)                  | 复制文件          |                |
| fs.mkdir(path, callback)                    | 创建目录          |                |
| fs.readDir(path, callback)                  | 读取目录列表      |                |
| fs.rename(oldPath, newPath, callback)       | 重命名文件/目录   |                |
| fs.rmdir(path, callback)                    | 删除目录          | 只能删除空目录 |
| fs.stat(path, callback)                     | 获取文件/目录信息 |                |
| fs.unlink(path, callback)                   | 删除文件          |                |
| fs.watch(filename[, options]\[, listener])  | 监视文件/目录     |                |
| fs.watchFile(filename[, options], listener) | 监视文件          |                |
| fs.existsSync(absolutePath)                 | 判断路径是否存在  |                |

### 附：path模块其它方法列表

| 方法                       | 作用                               |
| -------------------------- | ---------------------------------- |
| path.basename(path[, ext]) | 获取返回 path 的最后一部分(文件名) |
| path.dirname(path)         | 返回目录名                         |
| path.extname(path)         | 返回路径中文件的扩展名(包含.)      |
| path.format(pathObject)    | 将一个对象格式化为一个路径字符串   |
| path.join([...paths])      | 拼接路径                           |
| path.parse(path)           | 把路径字符串解析成对象的格式       |
| path.resolve([...paths])   | 基于当前**工作目录**拼接路径       |



## 快速搭建Web服务器

```js
// 引入核心模块http
const http = require('http');
// 创建服务
const server = http.createServer(function(req, res) {
  console.log(req.connection.remoteAddress);
  res.end('hello world');
});
// 启动服务
server.listen(8081, function() {
  console.log('success');
});
```



==IP地址用来定位计算机==

==端口号用来定位具体的应用程序==

==所有要联网的应用程序都会占用一个端口号==



### 理解请求与响应

其中的参数是一个函数，这个函数是一个匿名函数，这个函数充当回调函数，有http请求时，会自动被调用

- 当某个客户端来请求这个服务器时，这个函数会自动调用，同时会自动给这两个参数赋值。第一个参数中包括本次请求的信息。

  - req：请求
    - req.url。本次请求的地址
    - req.method。   获取请求行中的请求方法
    - req.headers。    获取请求头

- 第二个参数用来设置本服务器对这次请求的处理。

  - res.end() 

    - 把本次的处理结果返回给客户端浏览器
  - res.setHeader()  设置响应头，比如设置响应体的编码
  
    `res.setHeader('content-type', 'text/html;charset=utf-8');`

  - res.statusCode 设置状态码



### HTTP 协议是什么

- HTTP(HyperText Transfer Protocol) 超文本传输协议。
- 协议双方： 浏览器与web服务器都要遵守的协议
- HTTP 协议中明确规定了`请求数据`和`响应数据`的格式(**报文**)
  - 浏览器 请求 资源 要遵守 http 协议：  请求报文
  - 服务器 返回 资源 要遵守 http 协议：  响应报文

### 请求报文

1. 请求行
2. 请求头
3. 请求体（可能是空）

#### 请求行

格式： `请求方法 请求路径 协议及版本`

```
GET / HTTP/1.1
GET /index.html HTTP/1.1
GET /common/get?id=123&name=jake HTTP/1.1
```

#### 请求头

- 浏览器在向服务器发送请求的时候自动携带的信息，一般不需要主动去设置；
- 信息是由键值对组成
- 如果需要设置请求头，使用setRequestHeader方法来设置

  [参考链接]https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers

| 键              | 值                                      |
| --------------- | --------------------------------------- |
| Host            | 请求的主机                              |
| Cache-Control   | 控制缓存（例如：max-age=60 缓存 60 秒） |
| Accept          | 客户端期望接收的文件的类型，逗号分隔    |
| User-Agent      | 标识什么客户端发送的这次请求            |
| Referer         | 这次请求的来源                          |
| Accept-Encoding | 可以接受的压缩编码                      |
| content-type    | 设置传递给服务器的请求体的格式          |

##### User-Agent

在服务器端，我们可以通过req.headers来获取所有的请求头信息。

在通过浏览器向web服务器发http请求时，会在请求头中自动附加上一些字段，例如：user-agent字段。这个字段中会记录该浏览器所在的设备的基本信息。例如，这个浏览器是在什么操作系统上运行，版本是什么，等等。 这个请求头到了服务器端之后，我们可以通过`req.headers['user-agent']`来拿到这个值。分析从这个值中保存的信息再进行后续的处理，例如：

- 对用户进行画像
- 统计有多少人，使用平板还是手机来访问这个网部
- 根据不同的设置进行页面跳转等。

```js
let userAgent = req.headers['user-agent'];
  if (userAgent.includes('Windows')) {
    console.log('你在使用window，pc端！！');
  } else if (userAgent.includes('iPad')) {
    console.log('你在使用iPad端！！');
  }
```

上面的代码对信息的分析比较粗略：只是根据是否包含了某些关键字来区分操作系统，更详细的分析可以参考：[zepto.js中对于用户设备的检测]https://github.com/madrobby/zepto/blob/master/src/detect.js#files

#### 请求体

在向http服务器发请求时，我们会附加上一些数据，例如做用户登陆验证时，我们发post请求会附上用户名和密码，这里的用户名和密码就是通过请求体来发送的。

值得注意的是，get类型的请求没有请求体，它的参数是通过附在url地址后面传递的 。

POST 请求有请求体，请求体就是发送给服务器的数据。



### 响应报文

1. 响应行
2. 响应头
3. 响应体

#### 响应行

```
-	状态码 ： 用来告诉浏览器服务器处理本次请求的结果。 不同的状态码对应不同的结果。
```

```js
// - 常见状态码及含义
//   - 200 - 成功
//   - 302 - 重定向
//   - 304 - 读取缓存
//   - 404 - 请求的资源不存在
//   - 500 - 服务器内部错误
```

可以通过res.statusCode 来设置响应码。

参考链接 https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status

#### 响应头

- 服务器返回响应的时候携带了附加信息
- 由键值对组成
- 每个请求的响应头可能都不一样：它完全取决于服务器；

| 键               | 值               |
| ---------------- | ---------------- |
| Date             | 响应时间         |
| Server           | 服务器信息       |
| **Content-Type** | 响应体的内容类型 |
| Content-Length   | 响应的内容大小   |

```javascript
const server = http.createServer(function(req, res) {
  res.setHeaders('content-type','text/html;charset=utf8')
});
```

#### 响应体

本次请求返回的主体内容。根据请求的不同，返回的内容也不同：

- 如果请求的是网页返回网页的内容
- 如果请求的是css返回样式文件的内容
- 如果请求的是图片返回图片的内容

在代码中，响应体的内容体现在res.end()中的内容上。

```
res.end(响应体)
```



## nodemon自动重启http服务

```bash
npm install -g nodemon
```


### 使用nodemon

在命令中，使用nodemon来代替node。

- 它是一个第三方的包（其它开发者写的工具），这里是通过全局安装的方式进行。



### get类型的接口-无参数

- req.method 可以判断请求的类型
- res.end()的参数只能是字符串，而不能是对象

### 接口与静态资源的区别

- 静态资源。
  - 它们一般表现为一个一个的文件。例如index.html, style.css, index.js。
  - 处理请求静态资源时，服务器一般就直接读出资源的内容，再返回给客户端浏览器
- 动态资源：接口
  - 它们不是以某个具体的文件存在的，而是服务器上的一段代码，访问接口时，服务器会执行这段代码，然后把代码的执行结果返回给客户端浏览器。




### 理解url

全称：Uniform Resource Locator，统一资源定位符。

格式：`协议://主机地址[:端口]/路径?查询字符串#锚点`

- http请求，默认端口80
- https请求，默认端口443
- MySQL默认端口3306



### nodejs中的url模块

- 引入

  `const url = require('url');`

- 使用它的方法

  - obj = url.parse(地址栏中输入的url)

  > ```
  > let urlobj = url.parse(req.url); // urlobj对象中，就有我们需要的信息
  > urlobj.pathname :获取用户输入的url的路径名 ('/schools/students')
  > urlobj.search: '?id=18&name=zs',
  > urlobj.query: 获取用户输入的url中的查询字符串( 'id=18&name=zs' )
  > urlobj.path: '/schools/students?id=18&name=zs',
  > urlobj.href: '/schools/students?id=18&name=zs' 
  > ```

上面urlobj.query只是获得了传递的全部参数，我们一般还需从地址栏中分析传递的数据。即从 `http://itcast.cn:80/schools/students?id=18&name=zs#phot`中分析出id和name的值来。



### nodejs中的querystring模块

用来对url中的查询字符串这部分进行处理

地址：https://nodejs.org/api/querystring.html#querystring_querystring_parse_str_sep_eq_options

#### 基本示例

```javascript
const qs= require('querystring');
let obj = qs.parse('id=18&name=zs');
console.log(obj)
```



### post接口

> 地址：/post
>
> 功能：获取用户传入的参数，并以json字符串格式返回，在返回的信息中要加上时间戳.
>
> ```
>接口地址:localhost:8080/post
> 参数：name=filex&age=30;
> 返回:{name:filex,age:30,_t:1563265441778}
> ```
> 

对于获取post参数就相对复杂一些，主要是用到request对象的两个事件data,end。



## 自定义模块

```javascript
//myModule.js
const myPI = 3;
function add(a, b) {
  return a + b;
}
// 通过module.exports来导出
module.exports = {
  myPI,
  add
};
```

### 导出模块的两种方式

- exports
- module.exports

区别在于：

- 在引入某模块时，以该模块中module.exports指向的内容为准。
- 在定义模块时：
  - 在初始时，exports和module.exports是指向同一块内存区域，其内容都是一个空对象。
  - 如果直接给exports对象赋值（例如：exports={a:1,b:2}），此时，exports就不会再指向module.exports，而转而指向这个新对象，此时，exports与module.exports不是同一个对象。而在引入模块时，是以模块的中的module.exports为准，因此，此时写在exports上的对象是无法导出的。
- 在导出模块过程中，建议只用一种方式（建议直接使用module.exports）。



## npm使用

- `npm` 全称 `Node Package Manager`(node 包管理器)，它的诞生是为了解决 Node 中第三方包共享的问题。

```javascript
npm init --yes
// 或者是 npm init -y
//如果项目根目录下已经有了package.json文件，就不需要再去运行这个命令了
```

```
npm install  currency.js
```

currency.js是包名。不要省略.js，是有效包名的一部分。（currency表示另一个包）



### 全局安装包和本地安装包

- 全局安装: 包被安装到了系统目录（一般在系统盘的node_modules中），本机都可以使用使用。

  - 命令：`npm install -g 包名`

    - ```
    which node   // 查看node的安装目录
      which npm   // 查看npm的安装目录
      npm root -g // 查看全局包的安装目录
      npm list -g --depth 0 //查看全局安装过的包
      ```
  
- 局部安装（或者叫本地安装)，包并安装在当前项目的根目录下，与package.json同级目录的node_modules。就只在这个项目中可以使用。

  - ​	命令：`npm install 包名`

#### 全局安装nrm包

```javascript
// 第一步： 全局安装 
npm install nrm -g
// 第二步：列出所有的源信息
// （*）标注的就是当前使用的源
nrm ls
// 第三步：根据需要切换源 
// 例如：指定使用taobao源
nrm use taotao
```



#### 全局包与本地包的区别

- 全局安装的包一般可提供直接执行的命令

- 本地安装的包是与具体的项目有关的， 我们需要在开发过程中使用这些具体的功能。

- 要用到该包的命令执行任务的就需要全局安装
- 要通过require引入使用的就需要本地安装



### 开发依赖和生产依赖(了解)

- gulp-htmlmin。这个工具是用来把html代码进行压缩的（去掉空格，换行等），我们需要在开发时使用它，而项目一旦上线，我们就不再需要它了。，因此将它归类为"开发依赖"。
- jquery。在开发时参与源码编写，在发布上线的生产环境中也是需要它的。不仅在开发环境编写代码时要依赖它、线上环境也要依赖它，因此将它归类为"生产依赖"。

#### 操作

这两种依赖关系，在具体操作的过程中，有如下区别

1. 保存到开发依赖(devDependencies)

```javascript
npm install 包名 --save-dev
// 或者 npm install 包名 -D
```

通过这种方式安装的包出会现在package.json文件中的`devDependencies`字段中。

2. 保存到生产依赖(dependencies): 

```javascript
npm install 包名 --save
// 或者 npm install 包名
// 或者 npm install 包名 -S
```

通过这种方式安装的包出会现在package.json文件中的`dependencies`字段中。



### require的加载机制

- `require` 优先加载**缓存**中的模块
- 如果是**相对路径**，则根据路径加载**自定义模块**，并缓存
  - `require('./main')`  省略扩展名的情况
  - 先加载 `main.js`，如果没有再加载 `main.json`，如果没有再加载 `main.node`(c/c++编写的模块)
- 如果不是相对路径，则加载核心模块，并缓存
- 如果不是自定义模块，也不是核心模块，则加载**第三方模块**
  - node 会去本级 node_modules 目录中找
  - 如果在 node_modules 目录中找到 `moment` 目录，则加载该模块并缓存
  - 如果过程都找不到，node 则取上一级目录下找 `node_modules` 目录，规则同上
  - 如果一直找到代码文件的文件系统的根路径还找不到，则报错



### npm 常用命令

```bash
npm -v  // 查看npm 版本
which node   // 查看node的安装目录
which npm   // 查看npm的安装目录
npm root -g // 查看全局包的安装目录
npm list -g --depth 0 //查看全局安装过的包
```

- 升级 npm

  ```bash
  npm install npm --global
  npm install npm -g
  ```
  
- 初始化 `package.json`

  ```bash
  npm init -y // 或者是npm init --yes
  ```
  
- 安装第三方包

  ```javascript
  // 安装package.json中列出的所有的包
  npm install
  // 全局安装
  npm install 包名 -g
  // 本地安装，没有指定版本，默认安装最新的版本
  npm install 包名
  // 一次安装多个包
  npm install 包名1 包名2 包名3
  // 安装指定版本的包
  npm install 包名@版本号
  // 简写。把install简写成 i
  npm i 包名
  ```
  
- 删除已安装的包 

  ```bash
  npm uninstall 本地安装的包名
  npm uninstall -g 全局安装的包名
  ```
  
- 从缓存目录安装包

  ```bash
  # 查看缓存目录
  npm config get cache
  # 从缓存目录下载包
  # --cache-min 后面跟的是时间，单位是分钟，超过这个时间才去服务器下载
  npm install --cache-min 9999999 <package-name>
  ```

 

## Express框架

### Express 介绍

- Express 是一个基于 Node.js 平台，快速、开放、极简的 **web 开发框架**
- Express 是一个第三方模块，有丰富的 API 支持，强大而灵活的**中间件**特性
- Express 不对 Node.js 已有的特性进行二次抽象，只是在它之上扩展了 Web 应用所需的基本功能

- 如果安装不成功、运行下`npm cache clean -f`，再重装试试



```javascript
const express = require('express')
// 1. 调用 express() 得到一个 app
const app = express()

// 2. 设置请求对应的处理函数
//    当客户端以 GET 方法请求 / 的时候就会调用第二个参数：请求处理函数
app.get('/', (req, res) => {
  res.send('hello world')
})
// 3. 监听端口号，启动 Web 服务
app.listen(3000, () => console.log('app listening on port 3000!'))
```

- app.get('/')相当于添加个事件监听：当用户以get方式求"/"时，它后面的回调函数会执行，其回调函数中的req,res与前面所学http模块保持一致。
- res.send()是exprss提供的方法，用于结束本次请求。类似的还有res.json(),res.sendFile() 。



### 托管静态资源

参考文档：http://expressjs.com/en/starter/static-files.html

#### 忽略前缀

```javascript
const express = require('express')

const app = express();
// 2. 设置请求对应的处理函数
app.use(express.static('public'))
// 3. 监听端口号，启动 Web 服务
app.listen(3000, () => console.log('app listening on port 3000!'))
```

#### 限制前缀

```js
// 限制访问前缀
app.use('/public', express.static('public'))
```

这意味着想要访问public下的内容，必须要在请求url中加上/public

### 路由

> 参考文档：http://expressjs.com/en/starter/basic-routing.html

路由是指确定应用程序如何处理客户端的请求。路由（**Routing**）是由一个 **URL**（或者叫路径标识）和一个特定的 **HTTP 方法**（GET、POST 等）组成的，涉及到应用如何处理响应客户端请求。每一个路由都可以有一个或者多个处理器函数，当匹配到路由时，这些个函数将被执行。

#### 格式

```javascript
app.METHOD(PATH, HANDLER)
```

其中：

- `app` 是 express 实例

- `METHOD` 是一个 [HTTP 请求方法](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)。 全小写格式。如：post,get,delete等

- `PATH` 是服务端路径（定位标识）

  | 浏览器url                                 | 服务端路径           |
  | ----------------------------------------- | -------------------- |
  | http://localhost:8080                     | /                    |
  | http://localhost:8080/public/a/index.html | /public/a/index.html |
  | http://localhost:8080/index.html?a=1&b=2  | /index.html          |

- `HANDLER` 是当路由匹配到时需要执行的处理函数

#### 示例

- 路径
  - http://127.0.0.1:3000/xxxx
  - app.get('路径')
  - 路径：域名后面的path
- 处理 get 请求

```javascript
// 当你以 GET 方法请求 / 的时候，执行对应的处理函数
app.get('/', function (req, res) {
  res.send('Hello World!')
})

// 当你以 GET 方法请求 / 的时候，执行对应的处理函数
app.get('/file.html', function (req, res) {
  res.send('file.html');
  res.sendfile('文件路径'）
  // 这里的文件路径必须是绝对路径
})
```

- 处理 post 请求

```javascript
// 当你以 POST 方法请求 / 的时候，指定对应的处理函数
app.post('/', function (req, res) {
  res.send('Got a POST request')
})
```



#### get无参数

```javascript
const express = require('express');
const app = express();
app.get('/get', function(req, res) {
  // 直接返回对象
  res.json({ name: 'abc' });
});
app.listen('8088', () => {
  console.log('8088');
})
```

#### get有参数

express框架会自动收集get参数，并保存在req对象的query属性中。我们直接来获取即可。

```javascript
const express = require('express');
const app = express();
app.get('/get', function(req, res) {
  // 直接返回对象
  console.log(req.query);
  
  res.send({ name: 'abc' });
});
app.listen('8088', () => {
  console.log('8088');
});
```



### 写post接口

#### 无参数

```javascript
const app = express();
app.post('/post',function(req,res){
	res.send({name:"abc"})
})
```

#### 普通键值对参数

获取post普通键值对数据，要通过第三方模块`body-parser`来解析。

具体来说当content-type为x-www-form-urlencoded时，表示上传的普通简单的键值对 。如果通过postman测试的话，对应的设置如下：

##### 步骤

```javascript
// 1. 引入包
const bodyParser = require('body-parser');
// 2. 使用包
app.use(bodyParser.urlencoded({extended:false}));
app.post("/add",function(req,res){
    //3. 可以通过req.body来获取post传递的键值对	
})
```

- app.use(....)之后，在res.body中就会多出一个属性res.body。



#### 文件上传

如果post涉及文件上传操作，则会要使用`multer`这个包来获取上传的信息。

```html
enctype="multipart/form-data"
```

```javascript
npm install multer
```

```javascript
// 1. 引入包
const multer = require('multer');
// 2. 配置
const upload = multer({dest:'uploads/'}) // 上传的文件会保存在这个目录下
uploads表示一个目录名，你也可以设置成其它的
// 3. 使用
// 这个路由使用第二个参数 .upload.single表示单文件上传， 'cover' 表示要上传的文件在本次上次数据中的键名。类似于<input type="file" name='cover'/>
app.post("postfile",upload.single('cover'), function(req,res){

})
```

- 如果当前目录下没有uploads，它会自动创建uploads这个文件夹



### 中间件技术

- 一个流程结束之后，按顺序进入下一个流程；
- 一个流程如果出了问题，下一个流程也会受影响。
- 我们可以很方便地插入某一个特殊的处理环节，而不需要对原有环节造成影响。这样做的目的既提高了生产效率也保证了可维护性。

我们可以称其中的每一个处理环节就是一个中间件。

#### express中间件

中间件**是**一个特殊的url地址处理**函数**

- 中间件是 express 的最大特色，也是最重要的一个设计。`Express是一个自身功能极简，完全是路由和中间件构成一个web开发框架：从本质上来说，一个Express应用就是在调用各种中间件。`
- 一个 express 应用，就是由许许多多的中间件来完成的

- 应用级中间件。 [Application-level middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.application)
- 路由级中间件。[Router-level middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.router)
- 错误处理中间件。[Error-handling middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.error-handling)
- 内置中间件。[Built-in middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.built-in)
- 第三方中间件。[Third-party middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.third-party)



- 中间件本质就是一个函数，它被当作 `app.use(中间件函数)` 的参数来使用
- 中间件函数中有三个基本参数， req、res、next
  - req就是请求相关的对象，它和下一个中间件函数中的req对象是一个对象
  - res就是响应相关的对象，它和下一个中间件函数中的res对象是一个对象
  - next：它是一个函数，调用它将会跳出当前的中间件函数，执行中间件；如果不调用next，则整个请求都会在当前中间件卡住，而得不到返回。

##### 示例：使用中间件打印日志

```javascript
var express = require('express')
var app = express()
var myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}
// 注册中间件
app.use(myLogger)
app.get('/', function (req, res) {
  res.send('Hello World!')
})
app.listen(3000)	
```



##### 示例：使用多个中间件

```javascript
app.use((req, res, next) => {
  console.log("第1个中间件");
  next();
});
app.use((req, res, next) => {
  console.log("第2个中间件");
  res.setHeader('content-type', 'text/html;charset=utf8');
  res.a = 1;
  next();
});
app.use((req, res, next) => {
  console.log("第3个中间件");
  res.b = 2;
  console.log(res.a,res.b)
  res.end('中间件');
});
```

- 注意先后顺序。
- 注意通过req来附加额外的信息。

##### 示例：设定特定路径的中间件

```javascript
var express = require('express')
var app = express()
app.use(function (req, res, next) {
  console.log('应用级中间件，能匹配所有请求')
  next()
})
app.use('/api1',function (req, res, next) {
  console.log('只匹配/api1请求')
  next()
})
app.get('/api1', function (req, res) {
  res.send('Hello World!')
})
app.listen(3000)
```



### 路由中间件

#### 使用场景

路由过多时，代码不好管理。以大事件的代码为例，我们定义了管理员角色的接口和普通游客的接口，这些接口如果全写在一个入口文件中(如下只是显示了4个接口，如果是40个接口，就会很难读了)，是很不好维护的。

```javascript
const express = require('express');
const app = express();
// 两种用户的操作，对应不同的接口
app.get('/getfrontdetail', (req, res) => {
  res.send('获取游客详情');
});
app.get('/getfrontinfo', (req, res) => {
  res.send('获取游客信息');
});
// 两种用户的操作，对应不同的接口
app.get('/getadmincate', (req, res) => {
  res.send('管理员获文章类别信息');
});
app.get('/getadmininfo', (req, res) => {
  res.send('获取管理员信息');
});
app.listen(3000, () => {
  console.log(3000);
});
```

我们的目标就是把它们拆开到不同的文件中，以便于管理。

#### 基本步骤

1. 整理接口名。

   对众多的接口名进行整理和分类，以一级目录，二级目录这样的方式进行。例如：

   ​	/admin/getcate 

   ​	/admin/getinfo

   ​	/front/getinfo

   ​	/front/getdetail

   2.通过nodejs的模块化，分模块定义路由中间件，并导出

   3.在入口文件中，导入并使用路由中间件

定义两个路由文件：

- front.js
- server.js

```javascript
// ./router/front.js
const express = require('express');
const router = express.Router();
router.get('/getinfo', function(req, res) {
  res.send('getinfo');
});
router.get('/getdetail', function(req, res) {
  res.send('getdetail');
});
module.exports = router;
```



```javascript
// ./router/server.js
const express = require('express');
const router = express.Router();

router.get('/getinfo', function(req, res) {
  res.send('管理员getinfo');
});
router.get('/getdetail', function(req, res) {
  res.send('管理员getdetail');
});
module.exports = router;
```

在主入口文件中使用它们

```javascript
const express = require('express');
const app = express();

const frontRouter = require('./router/front');
const serverRouter = require('./router/admin');

app.use('/front', frontRouter);
app.use('/server', serverRouter);
```



### 什么是会话控制

会话控制就是用来弥补http无记忆的缺陷的一种技术。它能够将数据持久化（保存数据）的保存在客户端(浏览器)或者服务器端，从而让浏览器和服务器进行多次数据交换时，产生连续性。

让每一次的请求和响应都知道对方是谁。

### 会话控制的分类

- cookie： 将数据保存到**客户端**（浏览器）
- session： 将数据保存到**服务器端**



#### 理解cookie

- cookie是将数据持久化（保存）存储到客户端（浏览器）的一种技术
- cookie是**键值对格式的字符串**
- 可以通过浏览器查看某个网站的cookie
- 如果浏览器保存了cookie，则向服务器发请求时，就会**自动带上这个cookie**。把cookie放在请求头中，发送给服务器。



#### 从服务器发送cookie给客户端

##### 原生的方法

设置单个cookie

```javascript
//在nodejs中，通过res.setHeader来设置响应头。
res.setHeader('set-cookie', 'name=curry');
```

设置多个cookie

```javascript
//在nodejs中，通过res.setHeader来设置响应头。
res.setHeader('set-cookie', ['name=curry', 'age=30']);
```

如果cookie值是中文的话，还要对这个值进行额外的编码。

```
let name = new Buffer('好汉').toString('base64'); //5aW95rGJ
var info = new Buffer('5aW95rGJ', 'base64').toString();
```

##### express中提供的方法

express框架给我们提供了一个res.cookie方法，用来设置cookie

`res.cookie(cookie名, cookie值,{其它属性});`



#### cookie详细设置

参考：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie

从服务器端，发送cookie给客户端，是通过设置Set-Cookie这个特殊的响应头来实现的。包括了对应的cookie的名称，值，以及各个属性。

```html
Set-Cookie: <cookie-name>=<cookie-value> 
Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>
Set-Cookie: <cookie-name>=<cookie-value>; Max-Age=<non-zero-digit>
Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>
Set-Cookie: <cookie-name>=<cookie-value>; Path=<path-value>
Set-Cookie: <cookie-name>=<cookie-value>; Secure
Set-Cookie: <cookie-name>=<cookie-value>; HttpOnly
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Strict
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Lax

// Multiple directives are also possible, for example:
Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>; Secure; HttpOnly
```

一个cookie所具有的主要的属性包括：

- Domain：域，表示当前cookie所属于哪个域或子域下面。对于服务器返回的Set-Cookie中，如果没有指定Domain的值，那么其Domain的值是默认为当前所提交的http的请求所对应的主域名的。比如访问 http://www.example.com，返回一个cookie，没有指名domain值，那么其为值为默认的www.example.com。
- Path：表示cookie的所属路径。
- Expire time/Max-age：表示了cookie的有效期。expire的值，是一个时间，过了这个时间，该cookie就失效了。或者是用max-age指定当前cookie是在多长时间之后而失效。如果服务器返回的一个cookie，没有指定其expire time，那么表明此cookie有效期只是当前的session，即是session cookie，当前session会话结束后，就过期了。对应的，当关闭（浏览器中）该页面的时候，此cookie就应该被浏览器所删除了。
- secure：表示该cookie只能用https传输。一般用于包含认证信息的cookie，要求传输此cookie的时候，必须用https传输。
- httponly：表示此cookie必须用于http或https传输。这意味着，浏览器脚本是不允许访问操作此cookie的(document.cookie不能访问)。



#### 设置有效期 

expires字段来用设置这个cookie在哪个时间内是有效的。值得注意的是，时间格式是UTC时间格式

`"cooke-name=cookie-value;expires=UTC时间"`

如下示例

```js
res.setHeader('set-cookie', ['id=1;expires=' + new Date(Date.now() + 1000 * 5).toUTCString()]);
```

表示id=1这个cookies在5秒之后失效。

如果使用express带的setCookie，则可以

`res.cookie('name', 'ok', { expires: new Date(Date.now() + 1000*5) })`

#### 在服务器端获取cookie

1. 手动解析

向服务器发送的请求中会自动携带cookie，具体来说它会在req.headers.cookie中保存。要注意取到的cookie中只包括键值对，而cookies的属性（如过期时间）是看不到的。

```javascript
req.headers.cookie; //isLogin=true; name=xsfss
```

这个字符中中包含了全部的cookie，为了把它们的值解析出来成一个对象，我们可以通过node的核心对象querystring来进行解析。

```javascript
// 1. 把; 替换成&，以让querystring能够解析
let cookiestr = req.headers.cookie.replace('; ', '&');
console.log(req.headers.cookie);
console.log(cookiestr);
// 2 解析成对象
let cookieObj = qs.parse(cookiestr);
let { isLogin, name } = cookieObj;
```

2 . 使用cookie-parser进行解析

如果想快速解析，则可以使用cookie-parser这个包。

先安装`npm install cookie-parser`

再使用：

```js
var cookieParser = require('cookie-parser');
app.use(cookieParser());

// 某个具体的路由回调函数中，cookies会以对象的格式保存在req对象中
console.log(req.cookies);
```



#### 删除cookie

express框架提供了一个删除方法。从服务器端删除:

```javascript
app.get('/quit', (req, res) => {
  res.clearCookie('name');
  res.clearCookie('isLogin');
  res.redirect('/login.html');
});
```



### session

服务器使用session把用户的信息临时保存在了服务器上，用户离开网站后session会被销毁。这种用户信息存储方式相对cookie来说更安全

session有一个缺陷：如果web服务器做了负载均衡，那么下一个操作请求到了另一台服务器的时候session会丢失。或者服务器重启了session数据也会丢失。

#### 设置

```javascript
1. 引入session包
const session = require('express-session');

const app = express();

//2. 配置项
let conf = {
  secret: '123456', //加密字符串。 使用该字符串来加密session数据，自定义
  resave: false, //强制保存session即使它并没有变化
  saveUninitialized: false //强制将未初始化的session存储。当新建了一个session且未
  //设定属性或值时，它就处于未初始化状态。
};

//3. 注册为express-session中间件
app.use(session(conf));
```

#### 设置session

```js
app.post('/loginAPI', (req, res) => {
    // 此处省略用户信息校验
    // 直接通过req.session来设置
	req.session.isLogin = true;
    req.session.name = req.body.username;
    res.end()
};
```

#### 获取session

```javascript
app.get('/index.html', (req, res) => {
    console.log(req.session)
};
```

#### 删除session

```javascript
app.get('/quit', (req, res) => {
    req.session.destroy();
};
```



#### 参考代码

```javascript
const express = require('express');
const session = require('express-session');
const bodyparser = require('body-parser');
const qs = require('querystring');
const app = express();

//2. 配置项
let conf = {
  secret: '4ey32erfyf3fgpg', //加密字符串。 使用该字符串来加密session数据，自定义
  resave: false, //强制保存session即使它并没有变化
  saveUninitialized: false //强制将未初始化的session存储。当新建了一个session且未
  //设定属性或值时，它就处于未初始化状态。
};
//3. 注册为express-session中间件
app.use(session(conf));
app.use(bodyparser.urlencoded({ extended: false }));
app.use(express.static('public'));

app.post('/loginAPI', (req, res) => {
  res.send(req.body.username);
  req.session.isLogin = true;
  req.session.name = req.body.username;
 
  let str = `
  <h1>${req.body.username}登录成功</h1>
  <a href='./vip.html'>vip</a>`;
  res.send(str);
});
app.get('/vip.html', (req, res) => {
  // session的值可以是任何的数据类型，比如布尔，数组，对象等
 
  let { isLogin, name } = req.session;

  if (isLogin) {
    let htmlstr = `
    <h1>weclome ${name}</h1>
    <a href='./quit'>退出</a>`;
    res.send(htmlstr);
  } else {
    res.send('<h1>请先登录</h1> <a href="./login.html">登录</a>');
  }
});

app.get('/quit', (req, res) => {
  req.session.destroy();
  res.redirect('/login.html');
});

app.listen(3000, () => {
  console.log(3000);
});
```



### cookie、session原理

cookie原理：

- 从服务器端向客户端留下信息；每次访问时都带上

session原理：

- 服务器端会为每个用户（浏览器）各自保存一个session（文件）。当服务器保存session之后，会以cookie的形式告诉浏览器，你的session号是哪一个。它把session号返回给了浏览器，而把真实的数据保存在服务器。
- 下次再来访问服务器的时候，浏览器就会带着它自己的session号去访问，服务器根据session号就可以找到对应的session了。



### cookie和session的优缺点

cookie：优点是节省服务器空间，缺点不安全。不要保存敏感信息。

session：优点是安全，缺点需要服务器空间， 是一种最常见的解决方案。



## 跨域

### 原因

不同源的ajax请求 -------- 跨域错误。

一个请求同时满足如此三个条件时，就会出现跨域问题，从而导致ajax请求失败：

- 你的浏览器多管闲事了。
  同源策略：==不同源地址之间，默认不能相互发送AJAX请求==

- 发出请求不符合同源策略要求。

  - 发请求的页面的url和接口的url必须是同源的。

  - 同源是指：`协议相同`，`域名相同`，`端口相同`。

  - 在前后端分离开发的场景下，前端的页面和后端的服务经常是分开部署的。

- 你的请求是xhr请求。就是常说的ajax请求。

### 实现跨域请求的方案--JSONP

**JSON** with **P**adding，是一种借助于 `script` 标签发送跨域请求的技巧。

其原理:

- script的src标签是可以发跨域请求的，借助 `script` 标签src请求服务端上的接口
- 服务端的接口返回JavaScript 脚本，并附上要返回的数据。

以后绝大多数情况都是采用 JSONP 的手段完成不同源地址之间的跨域请求，它其实并**不是ajax请求**。

#### 让script标签的src指向一个接口

> 前端：让script标签的src指向一个后端接口的地址；
>
> 后端：接口的返回值是一个js函数调用语句

前端页面

```html
<script src="http://localhost:3000/getTime"></script>
```

注意：

- script标签中的src会指向一个后端接口的地址。由于script标签并不会导致跨域问题，所以这里的请求是可以正常发送和接收的。
- 与我们之前理解的src指向某个具体的.js文件不同，我们只需要确保src所指向的地址的返回内容是js代码就行了，而不必要一定是.js文件。

后端接口

```bash
const express = require('express');
const app = express();
app.get('/gettime', (req, res) => {
  res.end(`alert(1)`);
})
app.listen(3000, () => {
  console.log('你可以通过http://localhost:3000来访问...');
});
```

注意：

- 后端接口的返回值是一个特殊的字符串： 一个刻意拼写的js函数调用语句



#### 传递函数名到后端

> 前端：让script标签的src指向一个后端接口的地址，并附加函数名；
>
> 后端：接口的返回值是一个js函数调用语句
>
> 目标：当请求成功时，执行前端指定的函数



`前端页面`

```html
<script>
	function fn(){
        console.log()
    }
</script>
<script src="http://localhost:3000/getTime?callback=fn"></script>
```

注意：

- 在前端自己定义一个函数，把函数名传给后端
- 使用get方式传参，并且参数名是callback。这个参数名要与后端保持一致。

`后端接口`

```bash
const express = require('express');
const app = express();
app.get('/gettime', (req, res) => {
  let { callback } = req.query;
  res.end(`${callback}()`);
})
app.listen(3000, () => {
  console.log('你可以通过http://localhost:3000来访问...');
});
```

注意：

- 后端接口接收函数名，并返回一个字符串，其内容是`函数调用语句`



#### 后端回传数据

> 前端：让script标签的src指向一个后端接口的地址，并附加函数名；
>
> 后端：接口的返回值是一个js函数调用语句,并附加实参；
>
> 目标：当请求成功时，执行前端指定的函数

前端页面

```html
<script>
      function dosomething(rs) {
        console.log(rs);
      }
</script>
<script src="http://localhost:3000/getTime?callback=dosomething"></script>
```

注意：

- script标签中的src会指向一个后端接口的地址。由于script标签并不会导致跨域问题，所以这里的请求是可以常发送的。
- 把前端的函数名传给后端

后端接口

```bash
const express = require('express');
const app = express();
app.get('/gettime', (req, res) => {
  let { callback } = req.query;
  let data = JSON.stringfy( {a:1,b:2} )
  res.end(`${callback}(${data})`);
})
app.listen(3000, () => {
  console.log('你可以通过http://localhost:3000来访问...');
});
```

注意：

- 接收函数名，组装一个特殊的字符串：`函数调用语名`
- 把要回传的参数转成字符串，并嵌入返回值，当作函数的实参。



#### jQuery封装的jsonp

jquery中的ajax已经封装好了的jsonp方式。你可以直接使用，具体来说就是给ajax请求添加一个dataType属性，其值为"jsonp"。示例如下：

前端页面

```javascript
       $(document).ready(function(){
        $.ajax({
            type : "get",
            async: false,//是否同步
            url : "请求地址",
            dataType: "jsonp",
            jsonp:"callback", //请求的参数名
            jsonpCallback: "jsonpCallback",//要执行的回调函数
            success : function(data) {
                console.log(data)
            }
        });
    });
//jsonp优点:
     //完美解决在测试或者开发中获取不同域下的数据,用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback。参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。
//jsonp缺点：
     //1.jsonp只支持get请求而不支持post请求,也即是说如果想传给后台一个json格式的数据,此时问题就来了,浏览器会报一个http状态码 415错误,告诉你请求格式不正确
     //2.安全问题
```



后端接口

```java
const express = require('express');
const app = express();
app.get('/gettime', (req, res) => {
  let { callback } = req.query;
  let data = JSON.stringfy( {a:1,b:2} )
  res.end(`${callback}(${data})`)
})
    
app.listen(3000, () => {
  console.log('你可以通过http://localhost:3000来访问...');
});
```

像express框架已经提供了一个名为jsonp的方法来处理jsonp请求:

```java
const express = require('express');
const app = express();
app.get('/gettime', (req, res) => {
  let data = {a:1,b:2}
  res.jsonp(data)
})
app.listen(3000, () => {
  console.log('你可以通过http://localhost:3000来访问...');
});
```



#### jquery封装的jsonp原理分析

第一步：产生一个随机函数名；并创建这个函数(jQuery34109553463653123275_1565234364495)；

第二步：动态创建script标签，其src就是拼接的后端接口地址及callback值，如果有其它参数，则正常传递

第三步：请求成功返回之后，执行第一步中创建的函数(jQuery34109553463653123275_1565234364495)。这个函数最终会指向$.ajax({success:function(){}}) 中的success

第四步：`销毁` 第一步中创建的函数及第二步中创建的script标签

- 添加断点调试

- 这里有一段模拟代码(面试，手写jsonp)

```php+HTML
 <body>
    <div class="container">
      <h1>jsonp</h1>
      <div>需要后端接口的配合：http://localhost:3005/jsonp</div>
      <pre>
        //--后端测试代码如下
          const express = require('express');
          const app = express()
          // 留言板接口 -- 获取所有数据
          app.get('/jsonp', (req, res) => {
            var { callback } = req.query;
            res.setHeader('content-type', 'application/javascript');
            res.end(callback + '({a:1,b:2})');
          });
          app.listen(3000,()=>{})
      </pre>
    </div>
    <script>
      function buildCallBackFunction(options, callbackFunName) {
        window[callbackFunName] = function(result) {
          options.success(result);
          window[callbackFunName] = null;
          delete window[callbackFunName];
        };
      }
      function buildParam(options) {
        var params = options.params;
        if (!params) {
          return '';
        }
        if (typeof params === 'object') {
          var arr = [];
          for (var p in params) {
            arr.push(`p=${params[p]}`);
          }
          return arr.join('&');
        } else if (typeof params === 'string') {
          return params;
        } else {
          return '';
        }
      }
      function buildScript(url) {
        var script = document.createElement('script');
        script.setAttribute('src', url);
        script.onload = function() {
          document.getElementsByTagName('head')[0].removeChild(script);
        };
        document.getElementsByTagName('head')[0].appendChild(script);
      }
      function json(options) {
        var { url, params, success } = options;
        var callbackFunName = 'callback_' + Date.now();
        var params = buildParam(options);
        params += !params ? 'callback=' + callbackFunName : '&callback=' + callbackFunName;
        url += '?' + params;
        buildCallBackFunction(options, callbackFunName);
        buildScript(url);
      }

      json({
        url: 'http://localhost:3005/jsonp/jsonp',
        // params: 'a=1&b=2',
        params: { a: 1, b: 2 },
        success: function(result) {
          console.log(result);
        }
      });
    </script>
  </body>
</html>
```



### 实现跨域请求的方案--CORS

CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。它允许浏览器向跨源服务器，发出[`XMLHttpRequest`](http://www.ruanyifeng.com/blog/2012/09/xmlhttprequest_level_2.html)请求，从而克服了AJAX只能[同源](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)使用的限制。CORS需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10(ie8通过XDomainRequest能支持CORS)。

[参考](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS

通过在**被请求的路由中**设置header头，可以实现跨域。不过这种方式只从最新的浏览器（IE10）才支持。

```javascript
app.get('/time', (req, res) => {
  // // 允许任意源访问，不安全
  // res.setHeader('Access-Control-Allow-Origin', '*')
  // 允许指定源访问
  res.setHeader('Access-Control-Allow-Origin', 'http://www.xxx.com')
  res.send(Date.now().toString())
})
```

- 这种方案无需客户端作出任何变化（客户端不用改代码），就当跨域问题不存在一样。
- 服务端响应的时候添加一个 `Access-Control-Allow-Origin` 的响应头
- 如果ajax请求中还附加了cookie，则还需要设置一句：`res.setHeader('Access-Control-Allow-Credentials', 'true');`

自行下载使 npm cors https://www.npmjs.com/package/cors

### jsonp vs cors 对比

jsonp：

- 不是ajax
- 只能使用`get方式`传参
- 兼容性好 

cors:

- 就是ajax
- 支持各种方式的请求(post,get....)
- 浏览器的支持不好



## path模块

- path是一个node的内置模块，引入后使用

- path.join() 用于进行路径信息的合并处理

  ```javascript
fs.readFile(path.join(__dirname, '我们最习惯的相对路径'), 'utf8', () => { //... });
  ```



## 托管静态资源的方式

- 1 首页的请求处理方式与之前相同

- 2 剩余的文件进行静态资源托管设置

  - 检测url是否以/public/开头即可，使用  字符串.startsWith()

- 3 检测后缀名将不同文件进行对应的处理

  - path.extname(req.url);    可以取出地址中的后缀(扩展名)

- 4 设置地址读取文件

  ```javascript
try {
    //  - try块中的代码出现报错后，错误不会真的报错来，而是执行后面的catch块内容
  } catch (err) {
    // err是错误信息，可选
    //  - 这里用来进行try块报错后的处理操作
  } finally {
    // 可以省略finally,不常用，反正都会执行
  }
  ```



## post接口的设置方式

- req.on('data', fn);  请求进行数据传输时会触发这个事件(会多次触发)
  - fn接收一个参数是某一段请求参数的buffer格式
  - 需要通过一个字符串进行拼接，buffer会自动转换为字符串类型
- req.on('end', fn); 请求的数据接收完毕时触发
  - 我们如果要使用post的请求参数，应当在end事件中进行操作
- end中接收的请求参数为urlencoded不好操作
  - 使用内置模块querystring的parse() ，可以将urlencoded转换为对象结构

- req.method 可以获取请求方式，值是一个大写的字符串 'GET'  'POST'



### npm start的启动方式

- npm init后会生成package.json文件
  - 在"scripts"属性中设置一个新属性“start”：“node 文件名”  或  "start": "nodemon 文件名"
- 在项目中打开终端，输入 npm start 即可启动项目中的webserver
  - 好处：无需我们查看项目结构找到webserver的文件了，直接通过npm start启动即可



## git工具的文件忽略功能

- 在项目的根目录下设置一个文件  .gitignore 
  - 内部可以设置不需要被git进行管理的一些内容(目录或文件)
    - 书写    node_modules   表示这个目录不需要被git管理
    - 书写    *.txt   表示所有txt文件都不需要git管理



## 静态资源托管的方式

```javascript
app.use(express.static(path.join(__dirname, './admin_public/')));
```

- 自定义地址的托管

  ```javascript
app.use('/admin', express.static(path.join(__dirname, './admin_public/')));
  ```

## 设置get请求的接口的方式：

- req.query可以直接接收get请求参数的对象结构
- res.send()  通用功能
  - 发送中文不会乱码，因为express设置了默认响应头为  text/html;charset=utf-8
  - 发送对象会自动转换为JSON格式的字符串，会设置响应头为 application/json;charset=utf-8



## post接口的设置

- 使用的包名为  body-parser 

- 让app使用bodyParser的功能进行req.body的设置
  - **app.use(bodyParser.urlencoded({extended: false}));**
    - false表示使用内置模块querystring进行处理，true为默认值使用第三方模块qs处理
  - 可以在app.post()的回调函数中直接使用req.body进行请求体的操作



## 文件上传的处理

- 使用了multer中间件

  - 安装：npm i multer
  - multer({ dest: '地址' });  // 简略处理方式
  
- 使用string-random包

  - 下载并引入
    - const sr = require('string-random')
  - 使用方式：  
    - sr()  或  sr(随机字符串长度)

## 路由

> 编程中的路由指的是  对 ‘客户端到服务端的请求’ 进行处理的一种方式
>
> - 例如：客户端通过 /common/post 发送请求，服务端对 /common/post进行处理，这就是设置了一个路由操作。（其实就是设置了一个接口，一个接口就可以称为是一个路由）

- 基本的路由设置方式：

  - app.get(地址，回调);
  - app.post(地址，回调)

- express中提供了路由的管理工具

  - 如果在server.js中设置n个路由(接口)，功能都混在一起，不方便处理

  - 使用方式：

    - 将某部分路由功能放到一个单独的模块中保存

      - 通过let router = express.Router()创建一个路由管理器实例
      - router的使用方式与app相同
      - 通过 module.exports = router 方式进行导出/暴露
  
    - 从server.js中进行模块的引入

      - 通过app.use()以中间件方式使用路由模块的功能

        ```js
let uesrRouter = require('./router/userRouter.js');
        app.use('/user', userRouter);
        ```
      ```
        注意：userRouter模块内部设置具体路由时，就不要再写 /user的部分了
      ```

## cookie和session

> http是一种**无状态**的协议：
>
> - 每次客户端请求服务端时，都是'初次见面'

## cookie

- cookie在登录中的设置方式：
  - 问题：服务端每次接受用户的请求时，用于http无状态，所以无法确定用户的身份
  - 为了解决这个无状态的问题，会在登录成功时，**服务端给用户下发cookie的数据(小票)**
  - **cookie的数据是保存在客户端的**
  - 等以后用户再请求服务端时，带着小票一起发送过去(自动)，服务端检测小票的信息即可判断这个用户使用访问过

  
  

## session

> session不是一个新技术，实际上就是cookie的一种使用方式

- session实现方式：
  - 因为cookie是保存在客户端的，用户可以随意修改或伪造
  - 服务端不再将数据直接下发到客户端保存了，而是将**数据保存在服务端**
  - **下发的是保存数据区域的标识(手牌)**
  - 用户下次请求时带着标识到服务端，开箱子读取数据进行操作即可
- 好处：确保数据无法被用户操作，安全




## 跨域

> 同源策略是浏览器自带的一种安全机制。
>
> - 本质上就是浏览器不允许我们使用ajax进行非同源地址的访问

- 浏览器从一个域名的网页去请求另一个域名的资源时，域名、端口、协议任一不同，都是跨域
- 这时就需要我们能够突破浏览器的同源策略限制，这种操作称为 跨域



### JSONP跨域方式

- 使用场景：
  - CORS公司内部进行使用
  - JSONP会在我们请求第三方接口时常用
- 设置方式：
  - 原生的设置方式：
    - 客户端的处理方式
      - 设置script标签，将src设置为接口地址
      - 通过callback参数传递客户端的处理函数名称
      - 在这个请求发送前设置好对应的处理函数即可
    - 服务端的处理方式：
      - 服务端接收处理函数名称
      - 响应函数调用形式的字符串，并传入数据即可
  - jQuery的设置方式：
    - 在jQuery的ajax方法中设置一个dataType属性，值为'jsonp'
  - axios不支持JSONP