## 1.任意数求和

```javascript
function sum () {
    var total = null;
    for(var i = 0; i < arguments.length; i++) {
        var item = arguments[i];
        item = parseFloat(item);
        !isNaN(item) ? total +=item : null;
    }
    return total;
}
```



## 2.获取页面中所有ID

获取页面中所有ID为HAHA的标签（兼容所有浏览器，不能使用querySelecterAll）

```javascript
function queryAllById(id) {
    var nodeList = document.getElementsByTagName('*');
    var ary = [];
    for (var i = 0; i < nodeList.length; i++) {
        var item = nodeList[i];
        item.id === id ? ary.push(item) : null;
    }
    return ary;
}
console.log(queryAllById('HAHA'));
```

简单的方法：`console.log(HAHA);`

在JS中，默认会把元素的ID设置为变量（不用再获取设置），若ID重复，获取的结果就是一个集合，包括所有的ID项，不重复就是一个元素对象（类似于ById获取的结果）



## 3.代码题

```javascript
var a = 9;
function fn() {
    a = 0;
    return function (b) {
        return b+a++;
    }
}
var f = fn();  
console.log(f(5)); // 5
console.log(fn()(5));// 5
console.log(f(5));// 6
console.log(a);// 2
```



## 4.URL到页面渲染

DNS：把域名翻译成IP地址   域名系统

**1.DNS解析：将域名地址解析为ip地址**

 - 浏览器DNS缓存
- 系统DNS缓存
- 路由器DNS缓存
- 网络运营商DNS缓存
- 递归搜索：www.baidu.com
  - .com下查找DNS解析
  - .baidu下查找DNS解析
  - .www下查找DNS解析
  - 再找不到就会出错

**2.TCP连接：TCP三次握手**

 - 第一次，由浏览器发起，告诉服务器要发送请求了
- 第二次，由服务器发起，告诉浏览器准备好了，发送吧
- 第三次，由浏览器发起，告诉服务器，我要发了，接收吧

**3.发送请求**

​	- 请求报文：HTTP协议的通信内容

**4.接受响应**

​	- 响应报文

**5.渲染页面**

 - 遇见HTML标记，浏览器调用HTML解析器解析成Token并构建成dom树 
- 遇见style/link标记，浏览器调用css解析器，处理css标记并构建cssom树
- 遇见script标记，调用JavaScript解析器，处理script代码（绑定事件，修改dom树/cssom树）
- 将dom树和cssom树合并成一个渲染树
- 根据渲染树来计算布局，计算每个节点的几何信息（布局）
- 将各个节点颜色绘制到屏幕上（渲染）

==注意==：这5个步骤不一定按照顺序执行，如果dom树或cssom树被修改了，可能会执行多次布局和渲染，实际页面中，都会执行多次

**6.断开连接：TCP四次挥手**

 - 第一次：浏览器发起，告诉服务器，我东西发完了（请求报文），你准备关闭
- 第二次：服务器发起，告诉浏览器，我东西接受完了（请求报文），我准备关闭了
- 第三次：服务器发起，告诉浏览器，我东西发送完了（响应报文），你准备关闭吧
- 第四次：浏览器发起，告诉服务器，我东西接受完了，我准备关闭了（响应报文）



## 5.闭包

 - **什么是闭包？**
	1.闭包是密闭的容器，类似于set，map容器，存储数据的
	2.闭包是一个对象，存放数据的格式是键值对

  - **形成的条件？**
	1.函数嵌套
	2.内部函数应用外部函数的局部变量

  - **闭包的优点？**
	1.延长外部函数局部变量的生命周期

  - **闭包的缺点？**
	1.容易造成内存泄漏

`注意：`合理的使用闭包、用完闭包要及时销毁



## 6.宏任务、微任务

**宏任务**：setTimeout、setInterval
	1、宏任务所处的队列就是宏任务队列
	2、第一个宏任务队列中只有一个任务：执行主线程的js代码
	3、宏任务队列可以有多个
	4、当宏任务队列中的任务执行完毕后，查看是否有微任务队列，若有先执行微任务队列中的所有任务，如果没有就查看是否有宏任务队列

**微任务**：new Promise().then()     process.nextTick(node中的)
	1、微任务所处的队列就是微任务队列
	2、只有一个微任务队列
	3、在上一个宏任务队列执行完毕后如果有微任务队列就会执行微任务队列中的所有任务