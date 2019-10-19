### DOM

DOM就是处理可扩展标记语言（html、xml）的编程接口

```javascript
//获取body元素
document.body
//获取HTML元素
document.documentElement
//获取浏览器屏幕的宽度和高度（兼容所有浏览器）
document.documentElement.clientWidth || document.body.clientWidth
document.documentElement.clientHeight || document.body.clientHeight

element.classList   设置多个样式
- 添加类 element.classList.add('类名1','类名2','类名3')
- 移除类 element.classList.remove('类名1','类名2','类名3')
- 切换类 element.classList.toggle('类名')  :元素存在该属性删除该属性，不存在该属性添加该属性       
```



### DOM节点

> 节点 ： Node （页面中所有的东西都是节点）
>
> 节点集合：NodeList  （getElementsByName / querySelectorAll 获取的都是节点集合）

- 元素节点 （元素标签）
  - nodeType：1
  - nodeName : 大写的标签名
  - nodeValue ：null
- 文本节点
  - nodeType：3
  - nodeName : '#text'
  - nodeValue ：文本内容
- 注释节点
  - nodeType：8
  - nodeName : '#commen'
  - nodeValue ：注释内容
- 文档节点 document
  - nodeType：9
  - nodeName : '#document'
  - nodeValue ：null

描述这些节点之家关系的属性

```javascript
// childNodes ：获取所有的子节点 包含元素节点和文本节点等
// children：获取所有的元素子节点（子元素标签集合） 
// children[0]实际开发中选取第一个子元素 / children[父.children.length - 1]
// parentNode：获取父亲节点
// firstChild：获取第一个子节点
// lastChild：获取最后一个子节点
// firstElementChild / lastElementChild ：获取第一个和最后一个元素子节点 （兼容IE9+）找不到返回null
// previousSibling：获取上一个兄弟节点
// nextSibling：获取下一个兄弟节点  包含元素节点和文本节点等
// 解决兼容性
function getNextElementSibling(e){
  while(e = e.nextSibling){
    if(e.nodeType === 1){
      return e;
    }
  }
  return null;
}
// previousElementSibling / nextElementSibling ：获取兄弟元素节点（不兼容IE6~8）找不到返回null

// createElement('')  创建节点
// node.appendChild(child)  node是父级 child是子级 是后面追加元素
// insertBefore: 
// 把一个元素对象插入到指定容器中某一个元素标签之前 [container].insertBefore([newEle],[oldEle])

// node.removeChild（child）  删除节点
// node.cloneNode()  复制节点
// 如果括号参数为空或者false，是浅拷贝，只复制节点本身，不克隆里面的子节点
// 括号为true 深拷贝 复制标签和里面的内容
```



### 表单属性设置

```javascript
//表单里面的值 文字是通过 value 来修改的
input.value = '';
//想要某个表单被禁用 不能再点击 disabled
btn.disabled = true;
//转换输入框的类型
input.type = 'text'/'password';
```



### 样式属性操作

```javascript
//JS修改style样式操作，产生的是行内样式，权重比css高
//精灵图背景位置
lis[i].style.backgroundPosition = '10px 10px';
```

className

```javascript
//className 会直接更改元素的类名，会覆盖原先的类名
//如果想要保留原先的类名，可以用多类名选择器
this.className = 'first change';
```



### h5操作自定义属性

- 添加自定义属性：`<p data-自定义属性名='属性值'></p>`
- 获取自定义属性值：element.dataset.自定义属性名
- 注意：自定义属性名如果有 -   获取时要用驼峰方式




### DOM事件

**DOM0级事件**

- 语法：element.on+type = 函数名/匿名函数
- 特点：同一个元素只能注册一次相同类型的事件，注册多次，只有最后一次生效
- 事件解绑：
  - 语法：element.on+type = null
  - 原理：DOM0级绑定多次相同类型的事件，只有最后一次生效
- 阻止默认行为：
  - e.preventDefault();      是个方法     普通浏览器
  - e.returnValue;              是个属性     低版本ie678
  - return false;                  没兼容性问题     但是renturn后面的代码不执行

**DOM2级事件**

- 语法：element.addEventListener('事件类型'，函数名/匿名函数)
- 特点：同一个元素能注册多个相同类型的事件，注册多次，按照注册顺序依次执行
- 事件解绑：
  - 语法：element.removeEventListener('事件类型'，函数名)
  - 注意：给一个元素添加了DOM2级事件，又想给事件移除，在添加时应该使用函数名作为事件处理程序
- 阻止默认行为：
  - e.preventDefault();      dom标准写法




### 三种创建元素的区别

 ```javascript
1.  document.write() //创建元素 如果页面文档流加载完毕 再调用这句话会导致页面重绘
2.  innerHTML  //创建元素 采用数组形式拼接时效率更高，字符串拼接时效率低，结构复杂
3.  document.createElement() // 创建元素 效率稍微低一点点，结构更清晰	
//不同浏览器下，innerHTML（采用数组拼接）效率要比createElement高
 ```

  

### DOM事件流

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程就是DOM事件流

- JS代码只能执行捕获或冒泡其中的一个阶段
- onclick和attachEvent只能得到冒泡阶段
- addEventListener（type，listener，useCapture）第三个参数如果是true，表示在事件捕获阶段调用事件处理程序，如果是false（不写默认是false），表示在事件冒泡阶段调用事件处理程序




### 事件对象

e.target  返回的是触发事件的对象（元素）

this 返回的是绑定事件的对象（元素）

区别：e.target 点击了哪个元素就返回哪个元素，this是哪个元素绑定了这个点击事件，就返回谁



### 阻止事件冒泡

- IE：e.cancelBubble = true
- 标准写法： e.stopPropagation ()




### 事件委托

- 原理：不是每个子节点都单独设置事件监听器，而是事件监听器设置在父节点上，然后利用冒泡原理影响设置每个子节点
- 作用：只操作了一次DOM，提高了程序的性能




### 鼠标事件

```javascript
e.contextmenu()  //禁用右键菜单
e.selectstart()  //禁止选中文字

e.clientX  /  e.clientY  //返回鼠标相对于浏览器窗口可视区的坐标
e.pageX   /  e.pageY    //返回鼠标相对于文档页面的坐标  ie9+支持
e.screenX  /  e.screenY   //返回鼠标相对电脑屏幕的坐标
e.offsetX  / e.offsetY //光标相对于绑定事件元素的坐标
```



### 键盘事件

```javascript
onkeyup / onkeydown / onkeypress
onkeypress 不识别功能键，如左右剪头，ctrl shift等
执行顺序：keydown -- keypress -- keyup

keyCode  返回的是该键的ASCII值
onkeydown和onkeyup不区分字母大小写，onkeypress区分字母大小写
```



### BOM

BOM缺乏标准，JavaScript语法的标准化组织是ECMA，DOM的标准化组织是W3C，BOM最初是Netscape（网景公司）浏览器标准的一部分

```javascript
//BOM常见事件

//DOMContentLoaded   DOM 加载完毕 不包含图片 flash css 等就可以执行 加载速度比load更快
//resize 	浏览器窗口大小发生变化就会触发   
//window.innerWidth  是当前屏幕的宽度
//pageshow  重新加载页面时触发的事件
//scroll  滚动条滚动触发的事件
```



### 事件mouseover和mouseenter

- mouseover是鼠标经过自身盒子触发，经过子盒子还会触发
- mouseenter是只经过自身盒子触发
- mouseenter不会冒泡
- mouseleave是鼠标离开，同样不会冒泡



### 事件transitionend和animationend

- transitionend：元素的过渡动画结束的时候触发

- animationend：会在帧动画结束的时候触发

- 注意：1. **不能使用on的方式注册事件，只能使用addEventListener的方式注册**

  ​			2. 如果帧动画是无限次的，不会触发该事件animationend



### 定时器

```javascript
setTimeout(调用函数或函数名，延迟的毫秒数);  //只调用一次

clearTimeout(timeoutID);  //停止定时器

setInterval(回调函数，间隔的毫秒数)；  //每隔这个时间就会调用一次这个回调函数
//为防止第一次刷新有空白，在开启之前先调用一次

clearInterval(timeoutID);  //停止定时器
```



### this指向

- 作为方法时，this的最终指向的是那个调用它的对象
- 全局作用域或者普通函数中this指向全局对象window
- 定时器里面的this指向window
- 自执行函数中的this指向window
- 构造函数中this指向构造函数实例化的那个对象
- call、apply、bind时，this指向方法的第一个参数




### JS执行机制

- JS是单线程，同一时间只能做一件事。

- 缺点：如果js执行的时间过长，就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉


> **执行机制**
>
> 1. 先执行**执行栈中的同步任务**
> 2. 异步任务（回调函数）放入任务队列中
> 3. 一旦执行栈中的所有同步任务执行完毕，系统会按次序读取**任务队列**中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为**事件循环**



### JS内存回收机制

> 当栈内存被销毁，存储的那些基本值也就跟着销毁了

> 当堆内存释放销毁，那这个值彻底没了

> **堆内存的释放：**
>
> 当堆内存没有被任何的变量或者其他东西所占用，浏览器会在空闲的时候，自主的进行内存回收，把所有不被占用的堆内存销毁掉（谷歌浏览器）
>
> 利用计数器来记录还有没有被占用，当没有被占用的时候就会释放掉（IE浏览器）
>
> 记着记着记混了，导致有的释放不掉，这就是IE的内存泄漏问题



### location对象

window对象提供了一个location属性用于获取或设置窗体的URL，并且可以解析URL，这个属性称为location对象

控制台location，能看到location属性 

```javascript
location.href     //获取或设置整个URL       			重点
location.host	  //返回主机（域名）
location.port	  //返回端口号  如未填写返回空字符串
location.pathname //返回路径
location.search   //返回参数						  重点
location.hash	  //返回片段  #后面内容 常用于链接锚点
```

location方法

```javascript
location.assign()    // 跟href 一样，可以回退页面
location.replace()	 // 替换当前页面，因为不记录历史，所以不能后退页面
location.reload()	 // 重新加载页面，相当于刷新    如果参数true 则是强制刷新
```



**URL**

一般语法格式：`protocol://host[:port]/path/[?query]#fragment`

| 组成       | 说明                                       |
| -------- | ---------------------------------------- |
| protocol | 通信协议 常用的http， ftp， maito等                |
| host     | 主机（域名）  www.baidu.com                    |
| port     | 端口号  可选  省略时使用方案的默认端口 如http的默认端口为80      |
| path     | 路径  有零或多个 ‘ / ’ 符号隔开的字符串  一般用来表示主机上的一个目录或文件地址 |
| query    | 参数  以键值对的形式 通过&符号分隔                      |
| fragment | 片段 #后面内容 常见于链接 锚点                        |



### navigator 对象

navigator 对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以返回由客户机发送服务器的user-agent头部的值

```javascript
// 判断用户哪个终端打开页面，实现跳转
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mibile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows phone)/i))){
    window.location.href = "";  // 手机
} else {
    window.location.href = "";	// 电脑
}
```



### history对象

与浏览器历史记录进行交互（包含访问过的URL）

| 方法        | 作用                              |
| --------- | ------------------------------- |
| back()    | 可以后退功能                          |
| forward() | 前进功能                            |
| go(参数)    | 前进后退功能 参数如果是1前进一个页面如果是-1则后退1个页面 |

```javascript
history.back();
history.forward();
history.go(1);
```



### offse元素偏移量

==返回的数值都不带单位==

| 属性           | 作用                                                  |
| -------------- | ----------------------------------------------------- |
| e.offsetParent | 返回作为该元素带有定位的父级元素 父级没定位则返回body |
| e.offsetTop    | 返回元素相对带有定位父元素上方的偏移                  |
| e.offsetLeft   | 返回元素相对带有定位父元素左边框的偏移                |
| e.offsetWidth  | 返回自身包括padding、边框、内容区的宽度               |
| e.offsetHeight | 返回自身包括padding、边框、内容区的高度               |



### offset和style的区别

| offset                            | style                            |
| --------------------------------- | -------------------------------- |
| offset可以得到任意样式表中的样式值              | style只能得到行内样式的样式值                |
| offset系列获得的数值没单位                  | style.width获得的是带有单位的字符串          |
| offsetWidth包含padding+border+width | style.width获得不包含padding和border的值 |
| offsetWidth等属性是只读的 只能获取不能赋值       | style.width是可读可写 可获取也可赋值         |
| 想获取元素大小位置 offset更合适               | 想给元素更改值 需要用style改变               |



### client元素可视区

| 属性             | 作用                                |
| -------------- | --------------------------------- |
| e.clientTop    | 返回元素上边框的大小                        |
| e.clientLeft   | 返回元素左边框的大小                        |
| e.clientWidth  | 返回自身包括padding、内容区的宽度 不含边框，返回值不带单位 |
| e.clientHeight | 返回自身包括padding、内容区的高度 不含边框，返回值不带单位 |



### scroll元素滚动

| 属性             | 作用                               |
| -------------- | -------------------------------- |
| e.scrollTop    | 返回被卷去的上侧距离，数值不带单位                |
| e.scrollLeft   | 返回被卷去的左侧距离，数值不带单位                |
| e.scrollWidth  | 返回自身内容的实际宽度（含超出），不含边框，返回的数值不带单位  |
| e.scrollHeight | 返回自身内容的实际高度（含超出） ，不含边框，返回的数值不带单位 |



### 三大系列用法总结

1. offset系列用于获取元素位置  offsetLeft  offsetTop
2. client系列用于获取元素大小  clientWidth    clientHeight
3. scroll系列用于获取滚动距离  scrollTop   scrollLeft
4. **注意页面滚动距离获取用  window.pageYOffset**
5. 获取的都是数字不带单位
6. 获取的都是整数不出现小数（一般四舍五入）




### 本地存储

```javascript
setItem(key,value); //存储数据
getItem(key);	   //获取数据
removeItem(key);	   //删除数据
clear();			   //删除所有数据
```

sessionStorage：

1. 生命周期为关闭浏览器窗口
2. 在同一个窗口（页面）下数据可以共享
3. 以键值对的形式存储使用

localStorage:

1. 生命周期永久有效，除非手动删除，否则关闭页面也会存在
2. 可以多窗口（页面）共享（同一浏览器可以共享）
3. 以键值对的形式存储使用




### JSON

JSON是有一定格式的**字符串**，是一种数据格式

- 特点：
  - **键必须使用双引号包起来**
  - **字符串也必须是双引号**
  - 只有数字和字符串两种类型
  - 只是记录数据


- **将复杂数据类型数据转换成JSON格式**：`JSON.stringify(对象);`
  - 参数：js数据类型
  - 返回：JSON格式的数据
- **将JSON格式的数据转换为对象**:   `JSON.parse(json格式字符串);`
  - 参数：json格式字符串
  - 返回：js数据类型
  - **注意**：**如果参数不是JSON格式的数据就会报错**




### 动画效果

匀速动画：盒子当前的位置  +  固定的值

减速动画：盒子当前的位置  +  （目标值 - 现在的位置）/ 10



### 节流阀

- 防止轮播图按钮连续点击造成播放过快
- 目的：当上一个函数动画内容执行完毕，再执行下一个动画
- 核心思路：利用回调函数，添加一个变量来控制，锁住函数和解锁函数
- 开始设置一个变量var  flag = true;
- if(flag){flag = false;do something}  关闭水龙头
- 利用回调函数 动画执行完毕   flag = true  打开水龙头



### 移动端事件

触摸事件对象：

```javascript
touches			//正在触摸屏幕的所有手指的一个列表
targetTouches	//正在触摸当前DOM元素上的手指的一个列表		（常用）
changedTouches  //手指状态发生了改变的列表，从无到有，从有到无的变化
```

- touchstart时：推荐使用touches或targetTouches
  - 平常都用touches
  - 若是只能被某个执行元素操作，改为targetTouches
- touchmove和touchend时：推荐使用changedTouches

==`event.targetTouches[0]就可以得到正在触摸dom元素的第一个手指的相关信息`==



### 点击tap手势的实现

- 规则：

  - 坐标的规则：设置30~50px以内较为合理
  - touchstart和touchend间隔时间的规则：一般在300ms左右

  

### Zepto

用来进行移动端开发使用的，pc端不使用这个库

中文网：<https://www.zeptojs.com.cn/>  

- Zepto为了开发者使用功能更加灵活，将主体功能划分为多个部分（多个js文件）
- 我们可以根据需求去下载并引入对应的模块进行操作
  - 主体模块必须引入：  zepto.js
  - 然后再引入其他模块，例如touch.js

```javascript
// zepto的touch模块实现了各种移动端的手势，使用方式类似于事件
    // 1 使用zepto手势时，元素必须采用特殊的获取方式
    var $box = $('#box');
    /* $box.on('tap', function () {
      console.log('这是一个普通的tap手势');
    });

    $box.on('singleTap', function () {
      console.log('这是一个singleTap手势');
    });

    $box.on('doubleTap', function () {
      console.log('这是一个doubleTap手势');
    }); */
    $box.on('swipe', function () {
      console.log('swipe');
    });
    $box.on('swipeLeft', function () {
      console.log('swipeLeft');
    });
    $box.on('swipeRight', function () {
      console.log('swipeRight');
    });
    $box.on('swipeUp', function () {
      console.log('swipeUp');
    });
    $box.on('swipeDown', function () {
      console.log('swipeDown');
    });
```



### Swiper

**其他插件：superslider、iscroll**

| 配置项       | 描述         | 备注                     |
| ------------ | ------------ | ------------------------ |
| `direction`  | 方向切换选项 | 默认：`'horizontal'`水平 |
| `loop`       | 循环模式选项 | 默认：`false`            |
| `pagination` | 分页器选项   |                          |
| `navigation` | 前进后退按钮 |                          |
| `autoplay`   | 自动播放     | 默认：`false`            |
| `effect`     | 效果         | 默认：`'slide'`          |



### 拖拽元素

```javascript
var div = document.querySelector('div');
var startX = 0; //获取手指初始位置
var startY = 0;
var x = 0; // 获得盒子原来的位置
var y = 0;
div.addEventListener('touchstart',function(e){
    startX = e.targetTouches[0].pageX;
    startY = e.targetTouches[0].pageY;
	x = this.offsetLeft;
    y = this.offsetTop;
});
div.addEventListener('touchmove',function(e){
    var moveX = e.targetTouches[0].pageX - startX;
	var moveY = e.targetTouches[0].pageY - startY;
    this.style.left = x + moveX + 'px';
    this.style.top = y + moveY + 'px';
    e.preventDefault(); // 阻止屏幕滚动的默认行为
});
```



### 移动端视频插件

==zy.media.js==

