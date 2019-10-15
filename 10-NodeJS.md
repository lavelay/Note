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



## 能做什么

- Web服务器后台
- 命令行工具
  - npm	（node）
  - git （C语言）
  - hexo （node）



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

