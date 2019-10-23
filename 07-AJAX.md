## 服务器（server）

免费的服务器网站	：	**http://free.3v.do**

服务端无法主动对客户端发起请求

> 服务器 = 硬件配置高的电脑 + 安装特殊软件

根据服务器提供的服务类型不同，服务器又分为**文件服务器**、**数据库服务器**、**应用程序服务器**、**web服务器**

Web服务器根据网络中所在的位置分为**本地服务器**和**远程服务器**



## 客户端（client)

客户端：连接到服务器，享受服务的设备，就是客户端。

基本流程

1. 确认地址。用户在浏览器（客户端）地址栏输入要访问的网站网址（URL）
2. 发送请求。浏览器向服务器发送请求(request)，告知服务器要获取的内容
3. 获取响应。服务端收到浏览器发送的请求，并把处理的结果返回给浏览器(response)
4. 显示内容。浏览器将服务端返回的结果显示到界面上



## 常见的请求方式

- 标签的href和src(无法由用户进行控制)

- 在浏览器地址栏输入网址回车

- **location.href**

  - 如果请求服务端的某个页面，记得设置http://部分

- **form标签**

  - form的action表示表单提交给那个地址处理

  - 表单元素必须设置name属性，否则数据无法正常提交

  - 提交按钮的使用：

    - input[type=submit] 提交按钮

    - button[type=submit] 提交按钮 （默认type就是submit，设置时可以不写）

    - button[type=button] 普通按钮

    - input[type=button] 普通

      统一的特点：**页面会发生跳转**。



## ajax是什么 

AJAX ，全称是：**A**synchronous **J**avaScript **A**nd **X**ml 。 

- 异步的JavaScript和XML。
- 特点：不会造成页面刷新
- 是一种创建交互式网页应用的网页开发技术。不是一种新技术，而是一种解决方案，在1998年就开始使用
- 异步表示不阻塞：浏览器在请求数据时，不会阻塞用户后续的操作
- XML表示一种数据格式，最初设计AJAX时，服务器返回的数据是XML格式，后面慢慢**被JSON数据格式取代**
- `浏览器`通过 **内置对象** `XMLHttpRequest`  向服务器发起请求，并接收服务器返回的数据，这一过程或实现这一过程的技术就是Ajax



## get和post区别

- 不同点：
  - get  ：获取，得到。这种方式请求用于向服务器请求资源（图片，文件，数据....）。它是最常见的请求方式。它的重点在于，它只是请求，而`不会改变`服务器上的资源。
  - post：派送，投递。这种方式的请求用于向服务器上提交数据，它的重点在于，它`可能会修改`服务器上的资源。
- 相同点
  - get和post请求都可以在发请求时附带一些数据。
  - get和post请求都能够从服务器上获取返回的数据。

- get请求：
  - 请求参数：通过请求发送的数据被称为请求参数。
  - get的请求参数被浏览器自动的**连接到url后面**
  - 请求参数的格式为：  名1=值1&名2=值2&...
    - 这种书写格式称为： urlencoded   url编码格式
      - 通过location.search 可以获取当前url ?以及后面的请求参数内容
        - 注意：中文获取时会被浏览器转码（不用管，不影响任何的操作）

  - 可发送的数据大小：
    - 由于get请求的参数在地址中传递，受限于浏览器的设置（2k左右）
  - 可发送的数据格式：
    - 只能发送文本形式的数据（不能发送图片、文件...）
  - get请求可以被缓存：
    - 原因：因为get请求的信息都在地址中显示，如果将地址保存，这个请求的所有信息就都保存了。
- post请求：
  - 语义：如果希望给服务端发送数据，使用post请求。
  - 发送数据的方式：
    - post请求的请求参数没有在url后面，而是在一个**隐秘的位置**传递的。
      - 如果发送一些隐私数据时，必须使用post方式发送
        - 注意：这里是一种相对的说法，post方法比起get来说，安全一些，但不是绝对的安全。
  - 可发送的数据大小：
    - post的请求参数大小理论上没有限制。
      - 实际上受限于服务端的设置。
        - 服务端会根据功能设置限制，或者服务端根据处理性能进行限制。
  - 可发送的数据形式：
    - 数据类型不限，如果需要发送文件时，只能采用post方式发送。
  - post请求无法被缓存。
    - 因为post没有在地址中传递数据，无法被缓存。

### 原生ajax中get 和 post 区别

- get
  - 参数拼接在url（`url?name=1&age=30`）
  - 由于浏览器对url长度的支持（各个浏览器均不同）是有限，所以，它只能附加少量的数据。
- post
  - 要设置请求头: `xhr.setRequestHeader('content-type','application/x-www-form-urlencoded')`
  - 参数写在send()方法中:`send('name=1&age=30')`
  - 相对于get 来说，没有传参大小的限制。



## 如何检测服务端响应的内容类型

- 服务端的响应信息中除了有主要的数据外，还有一些**额外信息**，称为 **Response Headers 响应头**

```javascript
xhr.getAllResponseHeaders(); // 获取所有信息
xhr.getResponseHeader('传入某个具体的响应头名称'); // 获取某个信息，常用
```



## onreadystatechange、onload

`onload` 是 HTML5 （2014年9月）以后新增的方便获取响应的事件，ie6,ie7,ie8对onload不支持

在html5之前，获取服务器返回内容的时候使用的是 `onreadystatechange`事件，这事件是在xhr对象状态变化时被触发，而一次请求过程中，`XMLHttpRequest`对象的状态会发生`多次变化`，也就意味着这个事件会被触发多次。

```javascript
var xhr = new XMLHttpRequest()
// open 方法的第一个参数的作用就是设置请求的 method
xhr.open('get', 'common/getCurrentTime')
xhr.onload = function () {
    alert('ok')
}
xhr.send()
```



## xhr 对象的状态

| readyState | 状态描述         | 说明                                                      |
| ---------- | ---------------- | --------------------------------------------------------- |
| 0          | UNSENT           | XHR被创建，但尚未调用 `open()` 方法。                     |
| 1          | OPENED           | `open()` 方法已经被调用，建立了连接。                     |
| 2          | HEADERS_RECEIVED | `send()` 方法已经被调用，并且已经可以获取状态行和响应头。 |
| 3          | LOADING          | 响应体下载中， `responseText` 属性可能已经包含部分数据。  |
| **4**      | **DONE**         | 响应体下载完成，可以直接使用 `responseText`               |



## get请求在IE 中的缓存问题

出现的原因：

- 每次请求的地址都一样，浏览器自作聪明去使用了第一次请求的结果。

解决方法

- 骗浏览器，让它以为`每次的请求都不一样`

- `http://localhost:3005/common/getCurrentTime?_t=1559038330427`

```javascript
document.getElementById('btn').onclick = function() {
          var xhr = new XMLHttpRequest();
          console.log(xhr.readyState);
          // open 方法的第一个参数的作用就是设置请求的 method
          var time = Date.now(); // 附加一个变化的值
          xhr.open('get', 'common/getCurrentTime?_t=' + time);
          console.log(xhr.readyState);
          xhr.send();
          // 更改事件为onreadystatechange
          xhr.onreadystatechange = function() {
            // 表示从服务器端返回的数据已经全部ok了。
            if (xhr.readyState == 4) {
              document.getElementById('lblTimer').innerHTML = xhr.responseText;
            }
          };
        };
```



## 使用FormData

```javascript
document.getElementById('btn').onclick = function() {
    //收集用户信息
    var fd = new FormData(document.getElementById('myform'));
    // 通过post传值
    var xhr = new XMLHttpRequest();
    xhr.responseType = 'json';
    xhr.open('post', 'common/post');
    // 不用设置请求头 
    xhr.send(fd);
    xhr.onload = function() {
        console.info(xhr.response);
    };
};
```

- FormData对象内部有一个键值对集合，键名就是表单元素的name属性名，值就是这表单元素当前的值。

### 通过FormData进行文件上传

```javascript
	// 注意结构设置中的input[type=file]的name必须跟接口文档一致。
      $.ajax({
        type: 'post',
        url: 'http://localhost:3005/formData/upload',
        data: new FormData($('#form')[0]),
        contentType: false,// jquery会自动给post请求设置请求头
        processData: false,// 不需要jquery去处理上传数据
        success: function (res) {
          console.log(res);
        }
      });
```

### FormData对象的api

<https://developer.mozilla.org/zh-CN/docs/Web/API/FormData>

```javascript
var fd = new Formdata();
fd.append(key,value);
// 向 FormData 中添加新的属性值，如果FormData 对应的属性值存在则覆盖原值，否则新增一项属性值。
fd.delete(key);
// 从 FormData 对象里面删除一个键值对。
fd.entries()
// 返回一个包含所有键值对的iterator对象。
fd.get(key)
//返回在 FormData 对象中与给定键关联的第一个值。
fd.getAll(key)
//返回一个包含 FormData 对象中与给定键关联的所有值的数组。
fd.has(key)
//返回一个布尔值表明 FormData 对象是否包含某些键。
fd.keys()
//返回一个包含所有键的iterator对象。
fd.set(key,value)
//给 FormData 设置属性值，如果FormData 对应的属性值存在则覆盖原值，否则新增一项属性值。
fd.values()
//返回一个包含所有值的iterator对象。
```



## 上传文件进度条onprogress

- xhr对象中有一个子对象upload，upload对象中有一个事件 onprogress。
- onprogress事件大约每100ms触发一次，其回调函数第一个参数是一个事件对象，这个事件对象中有两个属性 loaded 和 total
  - loaded：表示已上传文件的大小
  - total： 表示文件总大小

实现思路：

- 制作进度条，使用两层嵌套的div即可：第一层是进度条的外边框，第二层才是进度条
- 每次onprogress事件触发时：
  - 都计算当前已上传文件大小的百分比
  - 根据百分比去重绘进度条长度（宽度值可以是百分比值）

参考资料：静态页面中的样式

```html
.outer {
    height: 20px;
    background: #171b3c;
    border-radius: 20px;
    box-shadow: 0 2px 2px #4f4c4c;
    margin-bottom: 40px;
    position: relative;
}
.inner {
    position: absolute;
    border-radius: 20px;
    width: 0%;
    height: 20px;
    background: #ef2d56;
}
```

```javascript
document.getElementById('btn').onclick = function() {
    var innerDom = document.getElementById('inner');
    var fd = new FormData(document.getElementById('myForm'));
    var xhr = new XMLHttpRequest();
    xhr.open('post', 'formdata/upload');
	xhr.onload = function() {
        console.info(xhr.responseText);
    };
    xhr.upload.onprogress = function(ev) {
        console.info(Date.now());
        // 已上传 / 总大小
        console.info((ev.loaded / ev.total) * 100 + '%');
        // 设置百分比值
        innerDom.style.width = (ev.loaded / ev.total) * 100 + '%';
    };
    xhr.send(fd);
};
```



## ajax定义同步和异步

```javascript
xhr.open(参数1 ，参数2，参数3)
- 参数1 ：请求的方式.  get，post
- 参数2 ：请求的url地址。
- 参数3 ：是否启用异步模式，默认为true，即异步， `如果设置为false，就是同步`。
```

以请求黑盒服务器的接口sleep为例（这个接口已经预先写好了，直接调用即可）

```javascript
// 创建ajax，设置，并发送请求
var xhr = new XMLHttpRequest();
xhr.open('get', 'common/sleep');// 第三个参数不写，默认是异步
xhr.onload = function() {
    console.info('现在的时间是：', new Date().toLocaleTimeString());
};
xhr.send();// 发送。
```

#### 进程：进行中的程序

#### 线程：CPU最小执行单元

### 同步的ajax

- 同步代码中，onload必须写在send之前。
- 同步执行流程：
  - 浏览器：输出1
  - 浏览器：执行send(),发现是同步，`只能死等`。 整个代码块卡在send这句。
  - 浏览器：输出3

如果你设置成了同步的方式，你会在浏览器看到如下的错误信息：

[deprecation]由于主线程上的同步xmlhttpRequest对最终用户的体验有不利影响，因此不推荐使用它。



## $.ajax的其它选项

- data：需要传递到服务端的数据。字符串和对象均可。如果是对象会自动拼接成字符串

- cache: 设置ie浏览器的缓存问题。默认为true，表示缓存。  cache: false 不缓存。

- dataType：预期服务端返回的数据方式。是设置响应

- contentType：请求体内容方式，默认 `application/x-www-form-urlencoded`

- timeout：请求超时时间。

- beforeSend：在所有（open、send）请求发起之前触发执行

- complete：请求完成触发（不管成功与否）

- error：请求失败触发

- processData: boolean值。是否让jquery帮助处理传到服务器的数据

```javascript
 $.ajax({
        type: 'get',
        url: 'http://localhost:3005/common/get',
        data: {
          username: 'jack'
        }
      })
      // then() 成功时的处理函数，相当于success
      .then(function (res) {
        // ...
      })
      // fail() 失败时的处理函数，相当于error
      .fail(function (err) {
        // ...
      })
      // always() 无论成功还是失败都会执行，相当于complete
      .always(function () {
        // ...
      });
```



## $.getJSON

```javascript
$.getJSON(url,[,data][,success]);
参数：
 - url     ：字符串方式。指要请求的 URL 地址
 - data    : js对象，或者字符串方式。 可选的。 指发请求带给服务器的信息
 - success : function(json){} 是一个回调函数，当请求成功时被调用，参数是从服务器返回的JSON数据
```



## 表单中的文件控件

- multiple:是否可以多选
- accept:设置默认筛选的格式

```html
<input type="file" multiple />
```

- 设置只显示图片

  ```html
  // 只允许看到jpeg图片
  <input type="file" accept="image/jpeg" />
  // 只允许看到png图片
  <input type="file" accept=".png" />
  // 允许所有的图片
  <input type="file" accept="image/*" />
  ```



## 本地图片预览

文件控件选中图片后，文件控件中会保存图片信息它的files属性中。files属性是一个数组，如果只选中了一张图片，这张图片就放在files[0]中，如选了多张图片，则类似后推。

通过`window.URL.createObjectURL()`来创建一个临时的路径，

```javascript
// input_avatar就是file控件的内容发生变化执行
$('#input_avatar').change(function () {
    // 如果没有选择文件，返回
    if (!this.files[0]) return;
    var url = URL.createObjectURL(this.files[0]);
    $('#avatar').attr('src', url);
});
```



## 模板引擎

1. 引入template-web.js文件

2. 定义模板,指定script的id和type属性

   - 使用script标签type的推荐设置方式： text/html或text/template


- tempalte函数语法：`var html = template(模板id,  Object)`

#### 输出普通数据（字符串，数值）

```js
// 模板写法
{{ var }}
// template 函数写法
var html = template('id', {
	var： 'hello world'
});
```

#### 条件

```javascript
// 模板写法
{{if age > 18}}
	大于18
{{else}}
	小于18
{{/if}}
// template函数写法
var html = template('id', {
    age: 20
});
```

#### 循环

```javascript
// 模板写法1
{{each arr}}
	{{$index}} -- 数组的下标
	{{$value}} -- 数组的值
{{/each}}
// 模板写法2
{{each arr v i}}
	{{i}} -- 数组的下标
	{{v}} -- 数组的值
{{/each}}
// 设置了v和i两个位置，$index和$value就不能使用了
```



## axios库

jquery中封装了ajax功能，但体积比较大，若只用ajax功能，不需要dom操作，可以使用axios库

中文网站：<http://www.axios-js.com/zh-cn/docs/>

- 特性
  - 从浏览器中创建 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
  - 从 node.js 创建 [http](http://nodejs.org/api/http.html) 请求
  - 支持 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API （nodejs中学习）
  - 拦截请求和响应
  - 转换请求数据和响应数据
  - 取消请求
  - 自动转换 JSON 数据

```javascript
 // axios的使用:
    axios({
        method: 'get', // 请求方式
        url: 'http://localhost:3005/common/get',
        params: { / 请求参数       *********如果请求方式是post，请求参数用data********
          username: 'jack',
          userAge: 18
        }
      })
      // then() 成功时的处理函数
      //    - axios的res与jQuery不太相同，多包裹了一层对象
      //      - axios中的res.data相当于jQuery中的res，是一样的
      .then(function (res) {
         // 访问服务端响应的数据内容
      })
      // catch() 失败时的处理函数
      .catch(function (err) {
        // ...
      })
      // finally() 无论成功还是失败时都会执行
      .finally(function () {
        // ...
      });
```

```javascript
   //  axios.get() 的使用
    //   - get()中的请求参数，需要通过一个对象中设置的params传递
    axios.get('http://localhost:3005/common/get', {
      params: {
        username: 'jack'
      }
    }).then(function (res) {
      // ...
    });

    //  axios.post() 的使用
    axios.post('http://localhost:3005/common/post', {
        username: 'rose'
      })
      .then(function (res) {
        // ...
      });

    // axios.post() 和 axios()post方式上传文件
    //  - 发送文件时使用FormData无需进行额外处理，与普通post参数发送方式相同
    btn.onclick = function () {
      var fd = new FormData(form);
      
      //  post方式发送请求，无需额外处理
       axios.post('http://localhost:3005/formData/upload', fd)
        .then(function (res) {
          // ...
        }); 
------------------------------------------------------------------
      axios({
          method: 'post',
          url: 'http://localhost:3005/formData/upload',
          data: fd
        })
        .then(function (res) {
          console.log(res.data);
        });
      // 如果在网站看文章，有人让你改源码设置FormData操作，不用管，axios已经进行处理了
    };
```

