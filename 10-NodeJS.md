## Node.js

基于ChromeV8引擎的JS运行环境

- 代码只是具有特定格式的字符串而已
- 引擎可以认识，引擎可以解析和执行
- Google Chrome的V8引擎是目前公认的解析执行JS代码最快的引擎
- Node.js  中的JavaScript没有BOM、DOM，只有ECMAScript

**特性：**

1. event-driven 事件驱动
2. non-blocking I/O model 非阻塞IO模型（异步）
3. lightweight and efficient 轻量且高效

npm是世界上最大的开源生态系统，npm是基于Node.js开发的



## fs核心模块

在Node中想进行文件操作，就要引入fs核心模块

```javascript
var fs = require('fs');//用require方法加载fs核心模块
fs.readFile('dizhi', function (error, data) { //第一个参数是文件路径，第二个参数是回调函数
  //成功：data 数据
  		 //error null
  //失败：data undefined没有数据
       //error 错误对象
})
```



#### 方法1：在 REPL中运行

REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。

Node 自带了交互式解释器，可以执行以下任务：

- **读取** - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。
- **执行** - 执行输入的数据结构
- **打印** - 输出结果
- **循环** - 循环操作以上步骤直到用户两次按下 **ctrl-c** 按钮退出。

具体操作：

1. 在任意控制台中输入node 并回车确定，即可进行入node自带的REPL环境。
2. 此时，你可以正常写入js代码，并执行。
3. 如果要退出，连续按下两次ctrl+c



#### 方法2：执行一个JS文件

1. 请事先准备好一个js文件。
   - 例设这的路径是：e:/index.js
   - 具体内容是

```javascript
var a = 1;
console.info(a + 2);
```

2. 打开小黑窗，进入到这个文件的目录
   - 技巧，在资源管理器中按下shift，同时点击鼠标右键，可以选择在此处打开powershall窗口。
   - cd 命令可以用来切换当前目录。
3. 接下来 通过  ` node `  `js文件的路径 的格式来执行这个js文件。

```javascript
node index.js
```

注意:

- 执行js文件时，如果当前命令行目录和js文件**不在**同一个盘符下，要先切换盘符
- 执行js文件时，如果当前命令行目录和js文件**在**同一个盘符中，则可以使用相对路径找到js文件并执行

### nodejs的helloworld程序

下面，我们来通过一个最基本的http服务器程序来见识nodejs的作用。

第一步：新建一个文件，名为  `d:/http.js`( 文件名及路径名可以自行设置，建议均不使用中文字符)

第二步：在文件中录入如下代码。

```javascript
// 引入http模块
const http = require('http');

// 创建服务
const server = http.createServer(function(req, res) {
  console.log(`来自${req.connection.remoteAddress}的客户端在${new Date().toLocaleTimeString()}访问了本服务器`);
  res.end('<h1>hello world! very good!!</h1> <p>' + req.connection.remoteAddress + '</p>');
});
// 启动服务
server.listen(8081, function() {
  console.log('服务器启动成功，请在http://localhost:8081中访问....');
});
```

第三步：在小黑窗中进入到d盘根目录，键入命令 `node http.js`

第四步：打开一个浏览器容器，输入'http://localhost:8081'，观察效果

第五步：把localhost改成你自己电脑的ip地址，再把这个路径发你的同学来访问。

- 如果不能访问，有可能你需要手动关闭你自己计算机的防火墙。



- Node.js提供了大量的工具（API），能够让我们完成文件读写、Web服务器创建等功能。

![1562665560127](E:/待办事项/JS每日/2-nodejs/node-material.assets/1562665560127.png)

### nodejs和浏览器和javascript的关系

#### nodejs和浏览器的关系

不同之处：

![1562665535479](E:/待办事项/JS每日/2-nodejs/node-material.assets/1562665535479.png)

- 安装了浏览器这个软件，它不但可以执行ECMAScript，浏览器这个软件内置了window对象，所以浏览器有处理DOM和BOM的能力。
- 安装了NodeJs这个软件，它不但可以执行ECMAScript，NodeJS这个软件也内置了一些东西，包括全局成员和模块系统，同时还可以载入第三方模块来完成更强大的功能。



#### nodejs和javascript的区别？

- nodejs是一个容器（不是一个新语言），ECAMScript程序可以在这个容器中运行。
  - 不能在nodejs使用window对象，也不能在nodejs使用dom操作。因为nodejs中并不包含这个对象。
- javascript是由三个部分组成：ECAMScrtipt,Bom,Dom

### 学习Nodejs的意义

在我们熟悉的浏览器上执行JS不是很好吗？为什么要学习Nodejs呢？主要原因：

- 大前端必备技能
- 使得JS能够和操作系统 “互动” （读取文件，写入文件等，管理进程）
- 为JavaScript提供了服务端编程的能力
  - 文件IO
  - 网络IO
  - 数据库
- 了解接口开发，进一步理解Web开发，了解后端同学的工作内容



## nodejs中的模块化

### 模块化

一个js文件中可以引入其他的js文件，能使用引入的js文件的中的变量、数据，这种特性就称为模块化。使用模块化开发可以很好的解决变量、函数名冲突问题，也能灵活的解决文件依赖问题。

- 以前

  es5不支持模块化，让前端人员很为难。为了让支持模块化，我们一般会借用第三方库来实现：

  - sea.js. https://www.zhangxinxu.com/sp/seajs/
  - require.js. https://requirejs.org/

- 现在

  - es6原生语法也支持模块化
  - Nodejs内部也支持模块化（与es6的模块化有些不同之处），具体的语法在后面来介绍

### nodejs中的模块

每个模块都是一个独立的文件。每个模块都可以完成特定的功能，我们需要时就去引入它们，并调用。不需要时也不需要要管它。（理解于浏览器的js中的Math对象）

nodejs模块的分类

- 核心模块
  - 就是nodejs自带的模块，在安装完nodejs之后，就可以随意使用啦。相当于学习js时使用的Array对象。
  - 全部模块的源代码 https://github.com/nodejs/node/tree/master/lib
- 自定义模块
  - 程序员自己写的模块。就相当于我们在学习js时的自定义函数。
- 第三方模块
  - 其他程序员写好的模块。nodejs生态提供了一个专门的工具来管理第三方模块，后面我们会专门讲到。
  - 相当于别人写好的函数或者库。例如我们前面学习的JQuery库，arttemplate等。

#### 核心模块

> 官网文档 https://nodejs.org/dist/latest-v10.x/docs/api/
>
> 中文文档 http://nodejs.cn/api/
>
> 学会查 API，远远比会几个 API 更重要

- 核心模块就是 Node 内置的模块，需要通过唯一的标识名称来进行获取。
- 每一个核心模块基本上都是暴露了一个对象，里面包含一些方法供我们使用
- 一般在加载核心模块的时候，变量的起名最好就和核心模块的标识名同名即可
  - 例如：`const fs = require('fs')`

示例：用fs模块读取文件

```javascript
const fs = require('fs');
let htmlStr = fs.readFileSync( 'index.html')).toString();
console.log(htmlStr)
```

注意：require()中直接写模块的名字

- 不要加.js
- 不要加其它路径



#### 第三方模块

所谓第三方模块，顾名思义，就是别人写的模块（不是自己写的，也不是nodejs自带的）。在浏览器环境中使用第三方函数或者是库是很自然的，一般有两步：

1. 去官网下载js文件。或者使用DSN外链。
2. 在自己的html页面中引入

以jquery为例

1. 去jquery官网中下载jquery.js文件。
2. 在html页面中使用 script link标签引入这个js文件
3. 开始使用啦

这个过程中很容易，我们也慢慢习惯了，但这种使用方式是有问题的：

- 随着引入的第三方库越来越多，你得每一个库都去他们各自的官网上下载。引入10个库，都得下载10次
- 各个库的版本号在升级更新时，你也无法准确得知。

> 阿爷无大儿，*木兰*无长兄，愿为市鞍马，从此替爷征。
> 东市买骏马，西市买鞍鞯，南市买辔头，北市买长鞭。旦*辞*爷娘去，暮宿黄河边，不闻爷娘唤女声，但闻黄河流水鸣溅溅。旦*辞*黄河去，暮至黑山头，不闻爷娘唤女声，但闻燕山胡骑鸣啾啾。

木兰词中所述的场景：木兰替父从军，要买其参战装备要四处奔走。我们做个效果，要实现某个功能，要四处下载包，难到就没有一个类似于京东超市一样的地方，可以实现一站式配齐吗？

有，这个超市就是 大名鼎鼎的 `npm`。 在node中，我们通过npm来解决下载、使用、管理第三方模块的问题。

 

## fs模块

fs模块是文件操作模块。fs是 FileSystem的简写。它用来对文件，文件夹进行操作。

手册：http://nodejs.cn/api/fs.html

```js
// 引入模块。
// 可以使用var、let，但是建议使用const，因为我们不希望它被改变
const fs = require('fs');
```

fs模块中操作文件(或者文件夹)的方法，大多都提供了两种选择：

- 同步版本的
- 异步版本的

### 文件内容读取 - readFile

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

    - data: 文件内容，如果不设置参数2,则返回二进制数据。可以使用 toString() 方法将二进制数据

      转为正常字符串

  - 读取失败

    - err: 错误对象
    - data: undefined

示例：

```javascript
const fs = require("fs")
fs.readFile('文件路径',"utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

#### 同步格式

与异步格式不同在于：

- api的名字后面有Sync
- 不是通过回调函数来获取值，而是像一个普通的函数调用一样，直接获取返回值

```javascript
const fs = require("fs")
let rs = fs.readFileSync('文件路径',"utf8");
console.log(rs)
```



### 文件写入 

#### 覆盖写入 writeFile

功能：向指定文件中写入字符串（覆盖写入）， 如果没有该文件则尝试创建该文件。它把把文件中的内容全部删除，再填入新的内容。

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

在读取文件时，写相对路径是容易出问题的。下面我们来看会出什么问题。

假设有如下两个文件，它们所处的目录及文件名如下所示：

```
day01/js/fs.js
day01/js/text.txt
```

fs.js代码的作用是读出text.txt中的内容，并显示出来。

```
const fs = require('fs');
fs.readfilesync("./text.txt",'utf8'); 
//注意这里对text.txt的访问使用的是相对"fs.js" 本身的路径
```



现在，我们想要运行fs.js这个文件有两种方式：

- 如果终端中的路径定位在`js目录`下，则通过`node fs.js`

- 如果终端中的路径定位在`day01目录`下，则通过：`node js/fs.js` 

  此时就不能正确找到文件了。



原因是：我们在fs中读取文件时，使用的是相对路径，而相对路径的参考点是运行这个js文件的小黑窗的路径。而这个路径我们是可以通过cd命名来调整的。

解决方法，就是在操作文件时，使用**绝对路径**来定位文件。

#### \__dirname __filename 获取绝对路径

绝对路径： 从磁盘根目录开始到指定文件的路径。

相对路径：是以某个文件的位置为起点，相对于这个位置来找另一个文件。

nodejs中提供了两个全局变量来获取获取绝对路径：

- __dirname：获取当前被执行的文件的文件夹所处的绝对路径
- __filename：获取当前被执行的文件的绝对路径

#### path模块

http://nodejs.cn/api/path.html#path_path

它是一个核心模块，用来处理路径问题：拼接，分析，取后缀名。

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





## http模块-基本使用

http是nodejs的核心模块，让我们能够通过简单的代码创建一个Web服务器，处理http请求。

------

### 快速搭建Web服务器

1. 新建文件，写入如下代码。

```js
// http.js
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

2. 运行代码, `node http.js`
3. 在浏览器地址栏中输入：localhost:8081 观察效果。

说明

1. 把localhost改成本机ip地址，让同一局域网的同学访问。

2. 如果你修改了代码，必须先停止服务，然后再启动。这样才能生效。

   ctrl+c 停止服务。

3. 更改res.end()的内容，`重启`后，再次观察。

   - 获取ip，返回给浏览器



### 理解请求与响应

在上面的代码中，我们通过http.createServer方法创建一个http服务。

```javascript
// 创建服务
const server = http.createServer((req, res) => {
  console.log(req.connection.remoteAddress);
  res.end('hello world');
});
```

其中的参数是一个函数，这个函数是一个匿名函数，这个函数充当回调函数的角色，当有http请求时，它会自动被调用。



这个回调函数有它有两个参数。这两个参数非常重要，也非常复杂.

- 第一个参数表示`来自客户端浏览器的请求`，第二个参数用来`设置对本次请求的响应`。它们的形参名并不重要，但是，一般第一个参数名使用req或者request表示，第二个参数使用res或者resposne表示。

- 当某个客户端来请求这个服务器时，这个函数会自动调用，同时会自动给这两个参数赋值。第一个参数中包括本次请求的信息。

  - req：请求
    - req.url。本次请求的地址
    - req.method。   获取请求行中的请求方法
    - req.headers。    获取请求头

- 第二个参数用来设置本服务器对这次请求的处理。

  - 这个参数一般命名是res，它是一个对象，其中有很多方法和属性。

  - res.end() 

    - 把把本次的处理结果返回给客户端浏览器
    - 如果不写这一句，则客户端浏览器永远收不到响应。

  - res.setHeader()  设置响应头，比如设置响应体的编码

    `res.setHeader('content-type', 'text/html;charset=utf-8');`

  - res.statusCode 设置状态码



### 根据不同 url 地址处理不同请求

前面已经可以对浏览器的请求做出响应了，但是响应的内容总是一样的。能不能根据url的不同，做出合适的响应呢？当然可以，那么首先就需要知道浏览器请求的url是什么。

涉及到和请求相关的信息，都是通过请求响应处理函数的第一个参数完成的。代码示例

```javascript
// http.js
// 引入核心模块http
const http = require('http');

// 创建服务
const server = http.createServer(function(req, res) {
  if(req.url === "/a.html"){
      // 读出文件内容
      // 通过res.end()返回
  }
  else if(req.url === "/b.html"){
      
  }
    else{
        res.end("");
    }
});
// 启动服务
server.listen(8081, function() {
  console.log('success');
});
```

res.setHeader('content-type', 'text/html;charset=utf-8');



### HTTP 协议是什么

- HTTP(HyperText Transfer Protocol) 超文本传输协议。
- 协议双方： 浏览器与web服务器都要遵守的协议
- 请求通常是由像浏览器这样的接受方发起的
- HTTP 协议中明确规定了`请求数据`和`响应数据`的格式(**报文**)
  - 浏览器 请求 资源 要遵守 http 协议：  请求报文
  - 服务器 返回 资源 要遵守 http 协议：  响应报文

### 请求报文

http协议规定了浏览器向服务器发请求时的格式。

- 它由三个部分组成

1. 请求行
2. 请求头
3. 请求体（可能是空）

- 可以使用 chrome network面板来查看请求。



#### 请求行

格式： `请求方法  请求路径 协议及版本`

示例：

```
GET / HTTP/1.1
GET /index.html HTTP/1.1
GET /common/get?id=123&name=jake HTTP/1.1
```

在http模块中，我们可以通过req.method来获取本次请求的方法。请求路径会在保存在req.url属性中。

```js
const server = http.createServer(function(req, res) {
  console.log(req.method);
  console.log(req.url)
});
```



#### 请求头

- 浏览器在向服务器发送请求的时候自动携带的信息，一般不需要主动去设置；
- 信息是由键值对组成
- 如果需要设置请求头，使用setRequestHeader方法来设置
- [参考链接](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)

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
  } else if (userAgent.includes('iPhone')) {
    console.log('你在使用iPhone！！');
  }
```

上面的代码对信息的分析比较粗略：只是根据是否包含了某些关键字来区分操作系统，更详细的分析可以参考：[zepto.js中对于用户设备的检测](https://github.com/madrobby/zepto/blob/master/src/detect.js#files)



#### 请求体

在向http服务器发请求时，我们会附加上一些数据，例如做用户登陆验证时，我们发post请求会附上用户名和密码，这里的用户名和密码就是通过请求体来发送的。

值得注意的是，get类型的请求没有请求体，它的参数是通过附在url地址后面传递的 。

POST 请求有请求体，请求体就是发送给服务器的数据。



### 响应报文

http协议规定了服务器向浏览器返回数据时的格式。

- 它由三个部分组成

1. 响应行
2. 响应头
3. 响应体

#### 响应行

格式：  协议及版本 状态码  说明

```
-	状态码 ： 用来告诉浏览器服务器处理本次请求的结果。 不同的状态码对应不同的结果。
```

示例：

```js
HTTP/1.1 200 OK
HTTP/1.1 404 Not Found 
// 状态码：
// - 描述了请求过程中所发生的情况
// - 每个状态码的第一位数字都用于描述状态的一般类别("成功"、"出错"等)
// - 常见状态码及含义
//   - 200 - 成功
//   - 302 - 重定向
//   - 304 - 读取缓存
//   - 404 - 请求的资源不存在
//   - 500 - 服务器内部错误
// 
```

可以通过res.statusCode 来设置响应码。

```
res.statusCode
```

参考链接 https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status

#### 响应头

- 服务器返回响应的时候携带了附加信息
- 由键值对组成
- 每个请求的响应头可能都不一样：它完全取决于服务器；

几个常见的响应头

| 键               | 值               |
| ---------------- | ---------------- |
| Date             | 响应时间         |
| Server           | 服务器信息       |
| **Content-Type** | 响应体的内容类型 |
| Content-Length   | 响应的内容大小   |

可以通过如下代码来模拟

格式是：

`res.setHeaders('键','值');`

示例

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
- ......

在代码中，响应体的内容体现在res.end()中的内容上。

```
res.end(响应体)
```



## 使用 nodemon来自动重启http服务

我们每次修改了代码，都需要重启http服务器:

1. 进入控制台
2. 按下ctrl+c，停止已有http服务器。
3. 手动运行：node index.js 来重启服务器。

这会很麻烦。

有没有一个工具会自动检测到我们的修改并自动重新运行我们的代码呢？

有，它叫nodemon。https://www.npmjs.com/package/nodemon

### 安装 nodemon

通过npm包管理工具来进行安装。任意打开一个小黑窗，输入如下命令

```bash
npm install -g nodemon
```

此操作`需要联网`，根据网络速度所耗时间不同。

- npm是一个工具。用来管理node代码中要使用的第三方模块。它是随着node的安装而自动安装的：如果你安装node，则npm也已经安装过了，你可以直接使用。


### 使用nodemon

等待安装成功之后，使用方法也非常简单：在命令中，使用nodemon来代替node。

例如，

```bash
node server.js  // 
// 改成 nodemon server.js
nodemon server.js
```

它的好处在于会自动监听server.js这个文件的变化，如果变化了，就会重新自动再去运行。相当于是：

```bash
while(server.js 变化了){
  node server.js
}
```

说明：

- 它是一个第三方的包（其它开发者写的工具），我们这里是通过全局安装的方式进行。



## http模块-处理静态资源

静态资源指的是html文件中链接的外部资源，如css、js、image文件等等。

### 处理二次请求

从服务器获取html文件之后，如果这个html文件中还引用了其它的外部资源（图片，样式文件等），则浏览器会重新再发请求。

假设在index.html中还引入了 style.css 1.png 或者 .js文件，则：

浏览器请求localhost:index.html之后，得到的从服务器反馈的内容，解析的过程中还发现有外部的资源，所以浏览器会再次发出第二次请求，再去请求相应的资源。

一个最朴素的想法是根据不同的请求来返回不同的文件。

```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

//创建服务器
const app = http.createServer((req, res) => {

  if (req.url === '/index.html') {
    let htmlString = fs.readFileSync(path.join(__dirname, 'index.html'));
    res.end(htmlString);
  }
  else if (req.url === '/style.css') {
    let cssString = fs.readFileSync(path.join(__dirname, 'style.css'));
    res.setHeader('content-type', 'text/css');
    res.end(cssString);
  } else if (req.url === '/1.png') {
    let pngString = fs.readFileSync(path.join(__dirname, '/1.png'));
    res.end(pngString);
  } else {
    res.setHeader('content-type', 'text/html;charset=utf-8');
    res.statusCode = 404;
    res.end('<h2>可惜了, 找不到你要的资源' + req.url + '</h2>');
  }
}); 
//启动服务器，监听8082端口
app.listen(8082, () => {
  console.log('8082端口启动');
});
```

### 为不同的文件类型设置不同的 Content-Type

通过使用res对象中的setHeader方法，我们可以设置content-type这个响应头。这个响应头的作用是告诉浏览器，本次响应的内容是什么格式的内容。以方便浏览器进行处理。

常见的几中文件类型及content-type如下。

- .html：` res.setHeader('content-type', 'text/html;charset=utf-8') `
- .css：`res.setHeader('content-type', 'text/css;charset=utf-8')`
- .js：`res.setHeader('content-type', 'application/javascript') `
- .png：`res.setHeader('content-type', 'image/png')`

其它类型，参考这里：https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types

### 批量处理请求

由于我们不法事先得知一个.html文件中会引用多少个静态资源，所以，我们不能像处理某个页面一样去处理它们。我们的解决办法有两大类是：

1. 把这类静态资源连同所有的.html文件全放在固定的文件夹中。在用户请求时，当判断当前的req.url是在这个文件夹下就是直接读内容，并返回。

```javascript
01-server.js
// 创建服务器

const fs = require('fs');

// 1. 加载http
const http = require('http');
// 2. 创建server对象
const server = http.createServer((req, res) => {
    // 浏览器请求的是 /message.html
    console.log(req.url);


    fs.readFile('./public' + req.url, (err, data) => {
        if (err) return console.log(err);
        // 没有错误，将读取的结果响应给浏览器
        res.end(data);
    });

    /* if (req.url === '/message.html') {
        fs.readFile('./public/message.html', (err, data) => {
            if (err) return console.log(err);
            // 没有错误，将读取的结果响应给浏览器
            res.end(data);
        });
    } else if (req.url === '/assets/bootstrap.css') {
        fs.readFile('./public/assets/bootstrap.css', (err, data) => {
            if (err) return console.log(err);
            // 没有错误，将读取的结果响应给浏览器
            res.end(data);
        });
    } else if (req.url === '/assets/avatar.png') {
        fs.readFile('./public/assets/avatar.png', (err, data) => {
            if (err) return console.log(err);
            // 没有错误，将读取的结果响应给浏览器
            res.end(data);
        });
    } */
});
// 3. 监听端口，开启服务
server.listen(4000, () => console.log('开始监听 4000'));
```

- 2. 分析后缀名，如果是允许的，就直接返回

```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');
const url = require('url');
//创建服务器
const app = http.createServer((req, res) => {
  //实现静态web服务器的效果
  // 对于每一个请求，如果它的req.url是.html,.css,.png 这类资源
  // 1. 判断一个url的后缀是不是.html,css。。
  //    获取后缀;
  //    判断
  // 2.我们就直接读入文件，并返回
  console.log(req.url);

  let urlObj = url.parse(req.url);
  let extName = path.extname(urlObj.pathname);
  if (extName === '.html' || extName === '.css' || extName === '.png' || extName === '.bmp') {
    // 拼接绝对路径;
    // console.log(path.join(__dirname, req.url));
    let absolutePath = path.join(__dirname, urlObj.pathname);
    // 如果这个文件存在，就读出并返回
    if (fs.existsSync(absolutePath)) {
      let str = fs.readFileSync(absolutePath);
      res.end(str);
    } else {
      res.statusCode = 404;
      res.end(urlObj.pathname + ' not found!');
    }
  } else {
    res.statusCode = 404;
    res.end(urlObj.pathname + ' not found!');
  }
});
//启动服务器，监听8082端口
app.listen(8082, () => {
  console.log('8082端口启动');
});
```



## http模块-实现接口功能

在前面学习ajax时，我们说接口是后端同学写好的，我们前端同学只需要调用即可。现在，我们学习了nodejs，我们就可以客串一把后端同学的角色，来试着写写接口了。

### get类型的接口-无参数

现在假设我们自己就是一名后端程序员，现在要实现一个get类型的接口。具体要求如下：

地址：/gettime

功能：以json字符串格式返回服务器的时间戳。

示例：

```
输入:localhost:8080/gettime;
返回:{_t:1563265441778}
```

要使用postman软件进行测试。

参考代码：

```javascript
const http = require('http');
const app = http.createServer((req, res) => {
  if (pathname === '/gettime') {
    let obj = {_t : Date.now()}
    res.end(JSON.stringify(obj));//  把对象转成字符串之后再返回
  } else {
    res.end('error');
  }
});
app.listen(8083, () => {
  console.log(8083);
});
```

说明：

- req.method 可以判断请求的类型
- res.end()的参数只能是字符串，而不能是对象

### 接口与静态资源的区别



![1563336795597](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563336795597.png)

服务器上有很多的资源，每个资源都有自己的url。客户端浏览器想要访问某个资源就要向服务器发起对应的请求。

资源的分类：

- 静态资源。
  - 它们一般表现为一个一个的文件。例如index.html, style.css, index.js。
  - 处理请求静态资源时，服务器一般就直接读出资源的内容，再返回给客户端浏览器
- 动态资源：接口
  - 它们不是以某个具体的文件存在的，而是服务器上的一段代码，访问接口时，服务器会执行这段代码，然后把代码的执行结果返回给客户端浏览器。

目前学习过的发送请求有两种途径：

- 在地址栏中直接访问这个url
- 通过某个a标签进行进行跳转
- 通过表单进行提交
- 通过ajax技术访问这个url。

发送请求有很多类型：

- get
  - 在地址栏中直接访问这个url就是get方式
- post
  - 通过表单提交，可以设置form的method为post
- delete
- ....



url的作用是确定用户要访问的资源的位置，在地址栏中输入回车之后，这个请求会到web服务器中来，然后由web服务器来决定此时返回什么数据给用户。但是，我们能够根据url来推测服务器会返回什么信息吗？

```javascript
url:http://nodejs.cn/api/querystring.html
请求一个页面，名是querystring.html

url:http://oa.itcast.cn/seeyon/main.do?method=main

url:https://mail.qq.com/cgi-bin/frame_html?sid=aLqnlljMxF54DgtW&r=d281ced83329f34caae9786fcb5d4934

```

显然，不能，你能从服务器上获得什么，完全是由服务器决定的。

### 理解url

全称：Uniform Resource Locator，统一资源定位符。

作用： 定位资源(css,html,js,png, avi......)。

格式：`协议://主机地址[:端口]/路径?查询字符串#锚点`

- 协议
  - http
  - https
- 主机地址
  - IP地址 或者 域名
- 端口
  - http请求，默认端口80
  - https请求，默认端口443
  - MySQL默认端口3306
- 路径
  - 服务器文件夹上的资源。（.html/.css/.images/.js/接口）
- 参数（查询字符串）
  - ? 后面的部分，是键值对的形式
- 锚点
  - 网页内部的锚点链接

例如：http://itcast.cn:80/schools/students?id=18&name=zs#photo

经典用法：访问文件时传递参数。

```html
// index.html
<a href='detail.html?id=1'>新闻1</a>
<a href='detail.html?id=2'>新闻2</a>
```



```html
// detail.html
<script>
// 1. 获取id
// 2. 根据id值去获取这个新闻的详情 
</script>
```



### nodejs中的url模块

作用:url模块用来对url（例如：http://itcast.cn:80/schools/students?id=18&name=zs#photo）进行解析，进而得到各种信息。

手册地址：http://nodejs.cn/api/url.html

步骤：

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

上面urlobj.query只是获得了传递的全部参数，我们一般还需从地址栏中分析传递的数据。即从 `http://itcast.cn:80/schools/students?id=18&name=zs#phot`中分析出id和name的值来。这个操作是如何实现的呢？



### nodejs中的querystring模块

用来对url中的查询字符串这部分进行处理。nodejs中提供了querystring这个核心模块来帮助我们处理这个需求。

地址：https://nodejs.org/api/querystring.html#querystring_querystring_parse_str_sep_eq_options

#### 基本示例

```javascript
const qs= require('querystring');
let obj = qs.parse('id=18&name=zs');
console.log(obj)
```



### get类型的接口-带参数

现在假设我们自己就是一名后端程序员，现在要实现一个get类型的接口。具体要求如下：

> 地址：localhost:8080/get
>
> 功能：获取用户传入的参数，并以json字符串格式返回，在返回的信息中要加上时间戳.
>
> 示例：
>
> ```
> 1.不加参数
> 输入:localhost:8080/get;
> 返回:{_t:1563265441778}
> 2.带参数
> 输入:localhost:8080/get?name=filex&age=30;
> 返回:{name:filex,age:30,_t:1563265441778}
> ```
>
> 要求：能通过postman软件的测试。



分析：get请求的参数附加在url中，我们可以使用url模块来取出用户url中的参数部分，再使用querystring模块取出具体的参数值。



这里我们直接使用两个核心模块`url`和`querystring`来实现上述的需求。

```javascript
const http = require('http');
const queryString = require('querystring');
const url = require('url');

const server = http.createServer(function(req, res) {
  var { pathname, query } = url.parse(req.url);
  var obj = queryString.parse(query);

  console.log(p, url.parse(req.url));
  if (pathname === '/get' && req.method === 'GET') {
    res.setHeader('content-type', 'application/json');
    obj.d: Date.now() };
    res.end(JSON.stringify(str));
  } else {
    res.setHeader('content-type', 'text/html;charset=utf-8');
    res.end('大家好');
  }
});
server.listen(8088, function() {
  console.log('success', 8088);
});
```



### post接口

假设我们自己就是一名后端程序员，现在要实现一个post类型的接口。具体要求如下：

> 地址：/post
>
> 功能：获取用户传入的参数，并以json字符串格式返回，在返回的信息中要加上时间戳.
>
> 示例：
>
> ```
> 接口地址:localhost:8080/post
> 参数：name=filex&age=30;
> 返回:{name:filex,age:30,_t:1563265441778}
> ```
>
> 要求：通过postman软件的测试。



post类型与get类型的接口区别较大，主要在两个方面：

1. 类型不同

   对于类型不同还比较好判断，我们可以通过 req.method 来获取

2. 传参不同

   - get请求参数在请求行中（附加在url后面）
   - post请求参数在`请求体`中

对于获取post参数就相对复杂一些，主要是用到request对象的两个事件data,end。

基本流程是：

1. 在req对象上添加两个事件，用来收集参数

   1. req.on("data",function(chunk){ })

      每次收到一部分数据就会触发一次这个事件，回调函数也会相应的执行一次。其中的chunk是一个形参（你也可以换个参数名），它是一个buffer。

   2. req.on("end",function(){})

2. 解析参数

   1. queryString

```javascript
const http = require('http');
const url = require('url');
const queryString = require('querystring');
const server = http.createServer(function(req, res) {
  var { pathname } = url.parse(req.url);
  if (pathname === '/post' && req.method === 'POST') {
    let data = '';
    req.on('data', chunk => {
      data += chunk;
    });
    req.on('end', () => {
      res.setHeader('content-type', 'application/json');
      var str = { ...queryString.parse(data), d: Date.now() };
      res.end(JSON.stringify(str));
    });
  } else {
    res.setHeader('content-type', 'text/html;charset=utf-8');
    res.end('大家好');
  }
});

server.listen(8088, function() {
  console.log('success', 8088);
});
```

在发post请求时，传递的数据会在请求体中，它也是字符串格式，并且是一点一点上传到web服务器的（是积小成多，而不是一蹴而就）每上传一部分就会触发data事件，而最后全部上传完成之后，会触发end事件。

下面是一个示例代码，用来模拟使用post请求发送大量的数据，以观察req.on('data', chunk => {})多次触发的现象。

```javascript
var xhr =new XMLHttpRequest();
xhr.open('post','http://localhost:8080/post');
xhr.setRequestHeader('content-type','application/x-www-form-urlencoded');
xhr.send("name="+"imissyou".repeat(100000));
```



## 留言板案例

我们在前面学习ajax时，学习了如何去实现一个留言板，当时，我们是通过ajax调用现有的接口来实现的，现在我们采用全服务器端的思想来实现。

具体实现之后的效果如下。

### 文件系统

```
|--message
|--/node_modules
|--/package.json 
|--/server.js    主程序
|--/db.json      以json字符串格式保存留言信息
|--/message.html 页面
```



### 实现一个静态web服务器

1. 新建一个文件夹，比如msg
2. 将使用到的html文件、css文件、图片文件、js文件等复制到准备好的文件夹msg中
3. 将模拟数据db.json文件复制到msg中
4. 在msg文件夹中，创建app.js，搭建Web服务环境

### 实现留言列表

- 当输入地址，回车，会向服务器发送一次GET请求
- 服务器接收到请求，要给浏览器返回它要的数据

### 实现添加留言功能

1. 给表单设置action和method属性
2. 添加接口, 用于处理action
   1. 获取用户提交的数据
   2. 写入到message.json中
      1. 先读出来
      2. 转成数组
      3. 使用数组push，来追加
      4. 转成字符串，写回去

- 点击界面中的“添加”时，向服务器发送请求，并提交数据给服务器，注意设置表单的action和method
- 服务器接收到请求，完成数据添加，并作出响应，告知浏览器添加成功与否



参考代码

```js
const http = require('http');
const fs = require('fs');
const path = require('path');
const qs = require('querystring');

const app = http.createServer((req, res) => {
  console.log(req.url);
  if (req.url === '/message.html') {
    //1. 读入html文件
    let htmlString = fs.readFileSync('./message.html');

    //2.去message.json中读出留言内容，拼接htmlString中去

    let msgString = fs.readFileSync('./message.json', 'utf8');
    let msgArr = JSON.parse(msgString);

    //3.接接真实留言信息

    let htmlMsgStr = '';
    msgArr.forEach(ele => {
      let m = `
        <li class="media">
          <img class="mr-3" src="./assets/avatar.png" alt="张三" />
          <div class="media-body">
            <h4>${ele.name}</h4>
            <p>${ele.message}</p>
            <p>${ele.date}</p>
          </div>
        </li>
        `;
      htmlMsgStr += m;
    });
    // 4. 把htmlString中的{{{msg}}} 替换成msgArr表示的真实的留言信息
    htmlString = htmlString.toString().replace('##msg##', htmlMsgStr);
    console.log(htmlMsgStr);
    //5. 返回
    res.end(htmlString);
  } else if (req.url === '/assets/bootstrap.css') {
    let htmlString = fs.readFileSync(path.join(__dirname, req.url));
    res.end(htmlString);
  } else if (req.url === '/assets/avatar.png') {
    let htmlString = fs.readFileSync(path.join(__dirname, req.url));
    res.end(htmlString);
  } else if (req.url === '/addmsg' && req.method === 'POST') {
    // 收集用户提交的信息
    let postStr = '';
    req.on('data', p => {
      postStr += p;
    });
    req.on('end', () => {
      let obj = qs.parse(postStr);
      console.log(obj.name);
      console.log(obj.message);

      // 把信息添加到message.json文件中
      //1.读出message.json。转成数组
      let msgStr = fs.readFileSync('./message.json', 'utf8');
      let msgArr = JSON.parse(msgStr);
      //2. 向数组添加一条数据
      msgArr.push({
        name: obj.name,
        message: obj.message,
        date: Date.now()
      });
      //3.把这个数组写回到message.json中
      fs.writeFileSync('./message.json', JSON.stringify(msgArr));

      //进行页面的跳转，回到message.html
      res.end('<script>window.location.href="message.html"</script>');
    });
  }
});

app.listen(8080, () => {
  console.log(8080);
});
```



## 自定义模块

我们自己写的模块就是自定义模块。在nodejs中 ，我们对代码的封装是以模块（一个一个的文件）为单位进行的。一般的做法是实现好某一个功能之后，封装成一个模块，然后在其它文件中使用这个模块。



使用一个模块，就是一个js文件中去使用另一个js文件中定义的变量，常量，函数....



###  基本步骤

1.定义模块

新建一个js文件，用模块名给它命名。例如，你的模块叫myModule，则这个js文件最好叫myModule.js

2.导出模块

在myModule.js内部，我们定义一些函数，变量，当然，它们会根据我们的业务要求做一些不同的工作。最后根据情况导出这些函数，变量。

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

注意：

- module.exports 是固定写法，一般放在文件的最末尾，也只用一次。
- module.exports表示当前模块要暴露给其它模块的功能。你当然不必须要所有在模块中定义的函数都暴露出来。

3.引入模块

在你需要使用模块的文件中，使用require语句引入你定义好的模块，注使用相对路径。假设我们当前的文件是index.js，而我们希望在index.js文件中使用myModule.js中的add方法。

我们的做法是：

```javascript
// index.js
const myMath = require('./myMath');
```

上面的require()就是用来引入模块的。这里要注意使用自定义模块时，使用相对路径，而使用核心模块时，不需要写路径。

4.使用模块

当一个模块被成功引入之后，就可以按使用核心模块的过程一样去使用它们了。

```javascript
// index.js
const myMath = require('./myMath');

// 在使用之前请先打印出来看看。
console.log(myMath);

let rs = myMath.add(23,45);
console.log(rs)
```



### 导出模块的两种方式

在自定义模块过程中，有两种导出模块的内容的方式：

- exports
- module.exports

参考：https://nodejs.org/api/modules.html#modules_exports_shortcut

它们的关系是：  exports是module.exports的别名，即：

```javascript
exports === module.exports
```

所以下面两种写法的效果是一样的：

>```
>//1 mymodule.js
>exports.f = function(){ }
>exports.pi = 3.1415926
>```
>
>```
>//2 mymodule.js
>module.exports.f = function(){ }
>module.exports.pi = 3.1415926
>```



区别在于：

- 在引入某模块时，以该模块中module.exports指向的内容为准。
- 在定义模块时：
  - 在初始时，exports和module.exports是指向同一块内存区域，其内容都是一个空对象。
  - 如果直接给exports对象赋值（例如：exports={a:1,b:2}），此时，exports就不会再指向module.exports，而转而指向这个新对象，此时，exports与module.exports不是同一个对象。而在引入模块时，是以模块的中的module.exports为准，因此，此时写在exports上的对象是无法导出的。
- 在导出模块过程中，建议只用一种方式（建议直接使用module.exports）。



### 通过自定义模块对留言板案例进行改造





## npm使用

nodejs通过自带的`npm`(node package manager)工具来管理第三方模块，所以，在学习使用第三方模块时，我们先要学习npm的使用。

- `npm` 全称 `Node Package Manager`(node 包管理器)，它的诞生是为了解决 Node 中第三方包共享的问题。
- `npm` 不需要单独安装。在安装Node的时候，会连带一起安装`npm`。
- [官网](https://www.npmjs.com/)



当我们谈到npm时，我们在说两个东西：

- 命令行工具。这个工具在安装node时，已经自动安装过了。
- npm网站。这是一个第三方模块的"超市"，我们可以自由地下载，上传模块。

### 包（package）与模块关系

![1562665731262](E:/待办事项/JS每日/2-nodejs/node-material.assets/1562665731262.png)

nodejs中一个模块就是一个单独的js文件

- 包是多个模块的集合。一个模块能够解决的问题比较单一，一个包中有多个模块。
- npm 管理的单位就是包

类似于网站和网页的区别：一个网站一般会包含多个网页。

### 通过npm命令行下载第三方模块（包）

分成三步：

- 初始化项目。如果之前已经初始化，则可以省略
- 安装包。 npm install 包
- 引入模块，使用。

#### 第一步：初始化项目

进入到项目所在的根目录下，启动小黑窗（按下shift键，点击右键，在弹出的菜单中选择 在此处打开命令行）

输入如下命令：

```javascript
npm init --yes
// 或者是 npm init -y
```

init命令用来在根目录下生成一个package.json文件，这个文件中记录了我们当前项目的基本信息。它是一切工作的开始。

#### 第二步：安装包

生成了package.json文件之后，我们就可以来安装第三方包了。在npm官网中，有上百万个包，供我们使用。

![1562724829170](E:/待办事项/JS每日/2-nodejs/node-material.assets/1562724829170.png)

根据我们遇到的实际问题，我们来引入相应的包来解决它们。例如，我们在开发一个项目，其中涉及一些对货币金额的计算，格式化等问题。需要一些功能：

- 对货币数值进行格式化
- 精确运算货币数值

```
1234567元  ---> ￥1,234,567
0.1 + 0.2  ---> 0.3
```

此时，我们就可以去使用currency.js这个包。

npm地址：<https://www.npmjs.com/package/currency.js> 主页：<https://currency.js.org/>



##### 安装currency.js包

```
npm install  currency.js
```

注意：

- currency.js是包名。不要省略.js，它也是有效包名的一部分。（ 不要认为这是后缀名。如果你写currency其实表示另一个包）。

#### 第三包：使用包

当我们已经下载好一个包之后，就可以向使用核心模块一样去使用它。

格式是：`const 常量名 = require('包名')`

```javascript
// 1. 引入包
const currency = require('curency.js')

// 先打出来看看
console.log(currency)

// 2. 使用包
console.info(currency(1.23, { formatWithSymbol: true }).format());
```

### npm init 命令

在某个目录下开启小黑窗，输入如下命令：

```
npm init 
```

它会启动一个交互式的程序，让你填入一些关于本项目的信息。最后会生成一个package.json文件。

如果你希望直接采用默认信息，可以使用:

```javascript
npm init --yes
// 或者是 npm init -y
```

说明：

- 这个命令只需要运行一次，它的目的仅仅是生成一个package.json文件。而这个package.json文件在后期是可以手动修改的。
- 如果项目根目录下已经有了package.json文件，就不需要再去运行这个命令了
- 一般我们从网上clone下来的项目都会包含这个文件。

#### package.json文件

它整体是一个json字符串，对当前项目的整体描述。其中最外层可以看作是一个js的对象（每一个属性名都加了""，这就是一个典型的json标记）。这个文件中有非常多的内容，我们目前学习如下几个：

- name

  表示这个项目的名字。如是它是一个第三方包的话，它就决定了我们在require()时应该要写什么内容

- version

  版本号

参考

1.http://javascript.ruanyifeng.com/nodejs/packagejson.html

2.http://caibaojian.com/npm/files/package.json.html

### node_modules文件夹

这个文件夹中保存着我们从npm中下载来的第三方包。在使用npm install 命令时，会修改这个文件夹中的内容。具体如下来说，当键入`npm install XXX`之后（这里假设这个XXX包是存在的，也没有出现任何的网络错误）：

1. 如果有package.json

   (1) 修改package.json文件。根据开发依赖和生产依赖的不同，决定把这句记录在加在devDependencies或者是dependencies列表中。

   (2) 修改node_modules文件夹

   1. 如果有node_modules文件夹，则直接在下面新建名为XXX的文件夹，并从npm中下来这个包
   2. 如果没有node_modules，则先创建这个文件夹，再去下载相应的包

2. 如果没有package.json。会给一个警告信息

说明：

```
- 建议先创建package.json之后，再去install
- 在分享代码时，我们一般不需要把node_modules也给别人（就像你不需要把jquery.js给别人，因为他们可以自己去下载）。对方拿到我们的代码之后，先运行`npm install`(后面不接任何的包名)，自己去安装这些个依赖包。
```

### 全局安装包和本地安装包

我们通过`npm install` 命令来安装包，简单说就是把包从npm的官网上下载到我们自己的电脑中。具体这个包下载到哪里了，还是有一点讲究的。

分成两类：

- 全局安装: 包被安装到了系统目录（一般在系统盘的node_modules中），本机都可以使用使用。

  - 命令：`npm install -g 包名`

  - 辅助提示：

    - ```
      which node   // 查看node的安装目录
      which npm   // 查看npm的安装目录
      npm root -g // 查看全局包的安装目录
      npm list -g --depth 0 //查看全局安装过的包
      ```

- 局部安装（或者叫本地安装)，包并安装在当前项目的根目录下，与package.json同级目录的node_modules。就只在这个项目中可以使用。

  - ​	命令：`npm install 包名`

#### 全局安装nrm包

因为下载包时，默认是从npm官网（国外的网站）下载，速度可能会比较慢。在npm有一个工具可以来手动设置从哪里去下载包。这个工具就是nrm。这个工具是帮助我们切换安装包的来源的，不应该只限于某个具体的项目，所以我们采用全局安装的方式来安装它。

nrm包的地址：<https://www.npmjs.com/package/nrm>

nrm的使用方法。

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

- 全局安装的包一般可提供直接执行的命令。我们通过对一些工具类的包采用这种方式安装，如：

  gulp, nodemon, live-server,nrm等。

- 本地安装的包是与具体的项目有关的， 我们需要在开发过程中使用这些具体的功能。




一个经验法则：

- 要用到该包的命令执行任务的就需要全局安装
- 要通过require引入使用的就需要本地安装



### 开发依赖和生产依赖(了解)

在本地安装包时，表示我们这个项目要用到这个包，换句话说，我们这个项目要想成功运行，要依赖于这些个包。

但在，具体在项目进行的哪一阶段依赖于这些包呢？也有具体的差异。

#### 理解

举个生活中建房子的场景：

在建房子时，我们依赖：

- 辅助工具：尺子，水平仪，脚手架
- 原材料：钢筋，水泥

在住房子时，我们依赖：

- 原材料：钢筋，水泥

在房子进入到了使用阶段时，我们就不再需要尺子，水平仪，脚手架等这些个辅助工具了。我们买一所房子时，也不应该支付巨型脚手架的费用。  在开发前端项目的过程中也存在类似的问题：我们的开发过程和使用过程是分开的，开发项目时需要用到的包可能在使用项目时就不需要用到了。

假设有这么两个包：

- gulp-htmlmin。这个工具是用来把html代码进行压缩的（去掉空格，换行等），我们需要在开发时使用它，而项目一旦上线，我们就不再需要它了。，因此将它归类为"开发依赖"。
- jquery。在开发时参与源码编写，在发布上线的生产环境中也是需要它的。不仅在开发环境编写代码时要依赖它、线上环境也要依赖它，因此将它归类为"生产依赖"。



![1562728491126](E:/待办事项/JS每日/2-nodejs/node-material.assets/1562728491126.png)

这个差异就表现在，我们在打包项目时，就不需要打包“开发依赖”的包，这样减少成本。



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

在我们使用一个模块时，我们会使用require命令来加载这个模块。以加载一个自定义模块为例，require(文件名)的效果是：

1. 执行这个文件中的代码
2. 把这个文件中的module.exports对象中的内容返回出来。

以如下代码为例：

```
// moudule1.js
var a = 1;
var b = 2;
console.log(a+b);
var c = a+b;
module.exports = {
	data: c
}
```

在index.js中使用模块

```
// index.js
const obj = require('./moudule1.js');
console.log(obj);

这里的obj对象就是moudule1.js中的module.exports对象
```



- `require` 优先加载**缓存**中的模块
- 如果是**相对路径**，则根据路径加载**自定义模块**，并缓存
  - `require('./main')`  省略扩展名的情况
  - 先加载 `main.js`，如果没有再加载 `main.json`，如果没有再加载 `main.node`(c/c++编写的模块)
- 如果不是相对路径，则加载核心模块，并缓存
- 如果不是自定义模块，也不是核心模块，则加载**第三方模块**
  - node 会去本级 node_modules 目录中找`
  - 如果在 node_modules 目录中找到 `moment` 目录，则加载该模块并缓存
  - 如果过程都找不到，node 则取上一级目录下找 `node_modules` 目录，规则同上
  - 如果一直找到代码文件的文件系统的根路径还找不到，则报错



### npm 常用命令

- 查看

  ```bash
  npm --version
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
- 链接
  - [Express 官网](http://expressjs.com/)
  - [Express 中文文档（非官方）](http://www.expressjs.com.cn/)
  - [Express GitHub仓库](https://github.com/expressjs/express)

### 运行第一个express程序

由于它是第三方框架，我们需要先安装它。

#### 安装

> 参考文档：http://expressjs.com/en/starter/installing.html

```shell
# 在你的项目根目录下，打开小黑窗

# 1. 初始化 package.json 文件
npm init -y

# 2. 本地安装 express 到项目中
# npm install express
npm i express
```

注意：

- 项目目录名字不要取中文，也不要取express
- 如果安装不成功
  - 换个网络环境
  - 运行下`npm cache clean -f`，再重装试试

#### 使用

> 参考文档：http://expressjs.com/en/starter/hello-world.html



在项目根目录下新建一个js文件，例如app.js，其中输入代码如下：

```javascript
// 0. 加载 Express
const express = require('express')

// 1. 调用 express() 得到一个 app
//    类似于 http.createServer()
const app = express()

// 2. 设置请求对应的处理函数
//    当客户端以 GET 方法请求 / 的时候就会调用第二个参数：请求处理函数
app.get('/', (req, res) => {
  res.send('hello world')
})

// 3. 监听端口号，启动 Web 服务
app.listen(3000, () => console.log('app listening on port 3000!'))
```

说明：

- app.get('/')相当于添加个事件监听：当用户以get方式求"/"时，它后面的回调函数会执行，其回调函数中的req,res与前面所学http模块保持一致。
- res.send()是exprss提供的方法，用于结束本次请求。类似的还有res.json(),res.sendFile() 。



### 托管静态资源

参考文档：http://expressjs.com/en/starter/static-files.html

让用户直接访问静态资源是一个web服务器最基本的功能。

```javascript
http://localhost:3000/1.png
http://localhost:3000/css/style.css
http://localhost:3000/js/index.js
```

例如，如上url分别是请求一张图片，一份样式文件，一份js代码。我们实现的web服务器需要能够直接返回这些文件的内容给客户端浏览器。



在前面学习http模块时，我们已经实现了这些功能了，但是要写很多代码，现在使用express框架，只需一句代码就可以搞定了，这句代码是  `express.static('public')`

#### 忽略前缀

```javascript
// 0. 加载 Express
const express = require('express')

// 1. 调用 express() 得到一个 app
//    类似于 http.createServer()
const app = express();

// 2. 设置请求对应的处理函数
app.use(express.static('public'))


// 3. 监听端口号，启动 Web 服务
app.listen(3000, () => console.log('app listening on port 3000!'))
```

此时，所有放在public下的内容可以直接访问，注意，此时在url中并不需要出现public这级目录

- 在public下新建index.html。可以直接访问到。

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





### 写get接口

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
});
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

![1563331737144](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563331737144.png)



一般要先下载body-parser这个包。

```javascript
npm install body-parser
```

在 express4中，已经预先下载安装过了（在npm install exprss 时，就已经安装了body-parse，你可以在node_modules中查看到），这样就可以直接使用了

![1563331908506](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563331908506.png)

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

注意：

- app.use(....)之后，在res.body中就会多出一个属性res.body。



#### 文件上传

如果post涉及文件上传操作，则会要使用`multer`这个包来获取上传的信息。

```html
enctype="multipart/form-data"
```

对应postman的操作如下：

![1563331805546](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563331805546.png)

##### 步骤

1.安装

```javascript
npm install multer
```

2.使用

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

说明：

- 如果当前目录下没有uploads，它会自动创建uploads这个文件夹



### 中间件技术

在实际的工作中，我们需要对某些请求（或者某一类请求）进行特殊的处理，例如：要记录每一次请求的详细信息。需求：在调用某个接口时，打印出调用者的ip地址及调用时间。此时需要使用到中间件技术。同时对express而言，中间件是它的一个非常重要的概念，掌握中间件的思想对于理解学习express，提升编程水平都有很大的帮助。

#### 生活中的中间件

![1563350886257](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563350886257.png)

在上图中，自来水厂从获取水源到净化处理交给用户，中间经历了一系列的处理环节。

- 一个流程结束之后，按顺序进入下一个流程；
- 一个流程如果出了问题，下一个流程也会受影响。
- 我们可以很方便地插入某一个特殊的处理环节，而不需要对原有环节造成影响。这样做的目的既提高了生产效率也保证了可维护性。

我们可以称其中的每一个处理环节就是一个中间件。



#### express中间件

中间件**是**一个特殊的url地址处理**函数**

- 中间件是 express 的最大特色，也是最重要的一个设计。`Express是一个自身功能极简，完全是路由和中间件构成一个web开发框架：从本质上来说，一个Express应用就是在调用各种中间件。`
- 一个 express 应用，就是由许许多多的中间件来完成的

分类：

- 应用级中间件。 [Application-level middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.application)
- 路由级中间件。[Router-level middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.router)
- 错误处理中间件。[Error-handling middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.error-handling)
- 内置中间件。[Built-in middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.built-in)
- 第三方中间件。[Third-party middleware](http://www.expressjs.com.cn/guide/using-middleware.html#middleware.third-party)

#### 格式及基本示例

##### 格式

```js
// 具名函数格式：
const handler1 = (req, res, next) => {
  console.log(Date.now());
  next();
}
app.use(handler1);

// 匿名函数格式：
app.use((req, res, next) => {
  console.log(Date.now());
  next();
});
```

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



#### 中间件的执行流程

![1563354608948](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563354608948.png)



#### 中间件的应用

模拟body-parser

```javascript
app.use((req, res, next) => {
  if (req.method === 'POST') {
    let bodyStr = '';
    req.on('data', chunck => {
      bodyStr += chunck;
    });
    req.on('end', () => {
      req.body = qs.parse(bodyStr);
      next();
    });
  }
});
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



## 会话技术

有很多的网站都有登录的功能：

```
|--login.html (登录页)
|--index.html(主页)
|--setting.html(设置页)
```

实际开发，我们必须解决页面之间的数据共享问题：例如用户从login.html页面登陆之后，再去访问index.html或者setting.html页面时，应该还是能够获取用户的登陆信息。 

由于 http是无状态的，就是无记忆的，对于HTTP协议而言，无状态同样指每次request请求之前是相互独立的，当前请求并不会记录它的上一次请求信息。每次请求都是独立的，没有关联的，所以服务器和客户端都不知道是否是登录过的。

>无状态的理发店：理发店剪头发，店长不记忆是否是老客户，每人每次25元。这就是无记忆的。
>
>
>
>有状态的理发店：理发店剪头发，店长给你办理会员，下次你再来就记得你。这就是有记忆的。
>
>店长能够知道你是谁，有两种记录会员的信息：
>
>- 第一次理发之后，给你一张会员片，下次再来的话，带上会员卡。（ cookie ：把信息保存在浏览器端）
>- 第一次理发之后，把你的电话号码留下来，然后在**本子**上做记录。下次理发时，报出电话号码，他去查本子上的信息。（session：把信息保存在服务器上）
>
>理发店：服务器
>
>顾客：浏览器

### 什么是会话控制

会话控制就是用来弥补http无记忆的缺陷的一种技术。它能够将数据持久化（保存数据）的保存在客户端(浏览器)或者服务器端，从而让浏览器和服务器进行多次数据交换时，产生连续性。

让每一次的请求和响应都知道对方是谁。

![1566131019358](E:/待办事项/JS每日/2-nodejs/node-讲义.assets/1566131019358.png)

### 会话控制的分类

- cookie： 将数据保存到**客户端**（浏览器）
- session： 将数据保存到**服务器端**



### cookie（饼干，甜点）

#### 查看cookie

在浏览器中查看

- 在application--> cookie中查看。

在发送请求时的请求头中查看

#### 理解cookie

- cookie是将数据持久化（保存）存储到客户端（浏览器）的一种技术
- cookie是**键值对格式的字符串**
- 可以通过浏览器查看某个网站的cookie
- 如果浏览器保存了cookie，则向服务器发请求时，就会**自动带上这个cookie**。把cookie放在请求头中，发送给服务器。



![1564563169563](E:/待办事项/JS每日/2-nodejs/node-material.assets/1564563169563.png)



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

expires字段来用设置这个cookie在哪个时间内是有效的。值得注意的是，时间格式是UTC时间格式（ 不是中国时间）。

具体的语法是：

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

#### 原理

session 从字面上讲，就是会话。这个就类似于你和一个人交谈，你怎么知道当前和你交谈的是张三而不是李四呢？对方肯定有某种特征（长相等）表明他就是张三。

session 也是类似的道理，服务器要知道当前发请求给自己的是谁。为了做这种区分，服务器就要给每个客户端分配不同的“身份标识”，然后客户端每次向服务器发请求的时候，都带上这个“身份标识”，服务器就知道这个请求来自于谁了。至于客户端怎么保存这个“身份标识”，可以有很多种方式，对于浏览器客户端，默认采用 cookie 的方式来保存这个身份标记。

服务器使用session把用户的信息临时保存在了服务器上，用户离开网站后session会被销毁。这种用户信息存储方式相对cookie来说更安全，可是session有一个缺陷：如果web服务器做了负载均衡，那么下一个操作请求到了另一台服务器的时候session会丢失。或者服务器重启了session数据也会丢失。

![1566197324554](E:/待办事项/JS每日/2-nodejs/node-material.assets/1566197324554.png)

#### 安装包

在express框架下， 我们可以通过安装  `express-session` 包来实现session的功能。

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

跨域问题是我们前端开发中经常会遇到的问题，也是面试中的高频题目。通过这一节的学习，我们就能解决这类问题啦。

### 问题演示

![chrome跨域插件](E:/待办事项/JS每日/2-nodejs/node-material.assets/chrome跨域插件.gif)

```
/cors_server/
/cors_server/server.js

/cors_front/
/cors_front/index.html
/cors_front/jquery.js
```



参考代码

```javascript
// cors_server/server.js
// 后端服务器，提供接口
const express = require('express');

const app = express();

app.use(express.static('public'));
app.get('/getname', (req, res) => {
  res.json(['张三', '明月']);
});

app.listen(3000, () => {
  console.log(3000);
});
```



cors_front/index.html

通过ajax调用接口

```html
cors_front/index.html. 通过ajax调用接口
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>index.html</title>
    <style>
      .container {
        width: 800px;
        padding: 2em;
        margin: 40px auto;
        border: 1px solid #ccc;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <h1>标题</h1>
      <button id="btn">请求/getname接口</button>
      <div></div>
    </div>
    <script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.js"></script>

    <script>
      $('#btn').on('click', function() {
        $.ajax({
          url: 'http://localhost:3000/getname',
          type: 'get',
          success: function(result) {
            console.log(result);
          }
        });
      });
    </script>
  </body>
</html>

```





![1563502065924](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563502065924.png)



![1566201526753](E:/待办事项/JS每日/2-nodejs/node-讲义.assets/1566201526753.png)

### 原因

不同源的ajax请求 -------- 跨域错误。



一个请求同时满足如此三个条件时，就会出现跨域问题，从而导致ajax请求失败：

- 你的浏览器多管闲事了。
  跨域问题出现的基本原因是浏览器出于安全性的考虑------同源策略：ajax请求必须是同源，封杀了你跨域请求。

- 发出请求不符合同源策略要求。

  - 发请求的页面的url和接口的url必须是同源的。

  - 同源是指：`协议相同`，`域名相同`，`端口相同`。

  - 在前后端分离开发的场景下，前端的页面和后端的服务经常是分开部署的。

    ![1566136177994](E:/待办事项/JS每日/2-nodejs/node-讲义.assets/1566136177994.png)

- 你的请求是xhr请求。就是常说的ajax请求。

### 实现跨域请求的方案--JSONP

#### JSONP简介

**JSON** with **P**adding，是一种借助于 `script` 标签发送跨域请求的技巧。

其原理:

- script的src标签是可以发跨域请求的，借助 `script` 标签src请求服务端上的接口
- 服务端的接口返回JavaScript 脚本，并附上要返回的数据。

以后绝大多数情况都是采用 JSONP 的手段完成不同源地址之间的跨域请求，它其实并**不是ajax请求**。

![1566202959673](E:/待办事项/JS每日/2-nodejs/node-讲义.assets/1566202959673.png)

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
$.ajax({
   type: 'GET',
   url: 'http://localhost:4000/getTime', 
   success: function (result) {
      console.log(result);
   },
   dataType: 'jsonp' // 必须要指定dataType为jsonp
});
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

![1563504797676](E:/待办事项/JS每日/2-nodejs/node-material.assets/1563504797676.png)

- 这里有一段模拟代码(面试，手写jsonp)

```php+HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>html页面</title>
  </head>
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

[参考](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)

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



自行下载使用 npm cors https://www.npmjs.com/package/cors



### jsonp vs cors 对比

jsonp：

- 不是ajax
- 只能使用`get方式`传参
- 兼容性好 

cors:

- 就是ajax
- 支持各种方式的请求(post,get....)
- 浏览器的支持不好



# nodejs相关概念说明

- **nodejs环境中的javascript与浏览器中的javascript的区别：**
  - nodejs本质上就是一个独立的js解析器，无法执行html和css也无法执行webAPI
    - ECMAScript
    - node中的特殊功能
      - 可以进行文件的读写操作  
      - 可以设置web服务器功能
      - 可以操作数据库



# 模块

> 模块是我们对某个独立功能的称呼，任意的一段独立的功能代码都可以称为是一个模块。

- 模块的分类
  - 内置模块
  - 自定义模块
  - 第三方模块
- nodejs中也具有模块的概念，分类方式与上面是完全一样的。



## 模块的特点和设置方式

- 特点：

  - 每个模块中的功能都是独立的，不会影响到其他模块。
  - 模块与模块之前可能会出现**依赖**的情况
    - 需要考虑文件的引入的情况

- 设置方式：

  - ES6之前采用自调用函数，并结合暴露操作
    - 例如之前书写的  tools.js
  - 使用一些js库
    - sea.js
    - require.js
    - webpack 进行模块化操作 - vue部分
  - ES6中提供了单独的模块设置方式


## ES6中的模块设置方式

- 基本格式：require(模块的地址或内置模块的名称); 
- 具体操作步骤：
  - 被其他模块引入的模块中操作： demo1.js
    - 将需要被其他模块使用的数据进行暴露(导出)
    - module.exports = { 数据 };
    - exports.数据名 = 数据;  // 可以设置多个
  - 使用其他模块的那个模块中操作: demo2.js
    - 通过require(要引入的模块的地址)
    - 通过常量接收，防止不小心被修改了。
    - 使用常量内部的功能即可。。。



# nodejs中的内置模块

- nodejs中内置模块与浏览器中的js内置功能的区别
  - window
    - 浏览器中的功能都是可以直接访问的，都是全局的功能，操作时需要自己进行改进处理
    - document
    - console
  - nodejs
    - nodejs中的内置模块都是独立的功能，如果不进行引入就无法使用
    - 所以操作时，如果希望使用内置模块需要先进行引入操作。

## fs模块

> 是node中用来进行文件操作的模块

### readFile() 读取文件

- 是一个异步的读取文件方法

  ```javascript
  // 1 引入fs模块，才能使用内部的功能
  //    - 内置模块引入时，直接书写模块名称即可
  const fs = require('fs');
  
  
  // 2 使用readFile()读取一个文件的内容
  //   参数1： 文件路径
  //   参数2： 字符集  'utf8'
  //   参数3： 回调函数，会在文件读取完毕后执行
  //      - 参数1：err  错误信息
  //      - 参数2：data 文件的内容
  //   如果读取文件成功：
  //      - err为null，  data为文件的内容
  //   如果读取文件失败
  //      - err为错误对象， data为undefined
  
  fs.readFile('./demo.txt', 'utf8', (err, data) => {
    if (err) {
      // 我们管设置的报错称为 '抛异常'
      throw 'your file is bad bad';
    }
    console.log(data);
  });
  
  
  // 没有设置字符集参数时，读取的内容时buffer形式，可以通过toString进行处理
  fs.readFile('./demo.txt', (err, data) => {
    if (err) {
      // 我们管设置的报错称为 '抛异常'
      throw 'your file is bad bad';
    }
    console.log(data); // buffer
    console.log(data.toString()); // 字符串
  });
  ```



- 问题和改进方式
  - 终端在不同目录下执行 04.js 时，文件的读取效果不同（某些情况下找不到正确的文件，出现报错）
  - 原因：相对路径是相对的终端窗口
  - 修改方式：将相对路径设置为绝对路径
    - 打开目录复制粘贴处理太麻烦
    - 通过__dirname进行处理，代码书写略嫌麻烦
    - 最后使用path模块进行改进
- __dirname  获取当前文件所在目录的绝对路径
- __filename 获取当前文件的绝对路径（比上面的多了一个文件名称）

## path模块

- path是一个node的内置模块，引入后使用

- path.join() 用于进行路径信息的合并处理

  - 参数：传入各种各样的地址（可以含有相对路径和绝对路径）

  - 返回值：处理后的可以使用的地址

  - 以后进行文件操作的地址设置方式:

    ```javascript
    fs.readFile(path.join(__dirname, '我们最习惯的相对路径'), 'utf', () => { //... });
    ```

## http模块

### HTTP协议

- 作用：用来对请求响应发送方式设置的一种约定。
- 组成：
  - 请求：是由客户端发起的，由服务端接收处理
  - 响应：是由服务端发起的，由客户端接收处理
- 内容形式：
  - 请求时发送的内容称为**请求报文**：
    - 请求报文由3部分组成：  请求行， 请求头， 请求体
      - 请求行：  GET     /     HTTP/1.1
      - 请求头： 包含了请求发送时的一个附加数据
        - Content-Type  请求发送数据的内容类型
        - User-Agent 客户端设备的相关信息
      - 请求体：包含了请求发送的请求参数
        - 发送get请求时，请求体为空
          - 因为get请求的请求参数在请求行中传递
        - 发送post请求时，请求参数都包含在请求体中
  - 响应时发送的内容称为 **响应报文**：
    - 响应报文由3部分组成： 状态行，响应头， 响应体
      - 状态行： HTTP/1.1   200   OK
      - 响应头：响应发送时的一些附加数据
      - 响应体：就是服务端响应的数据内容
