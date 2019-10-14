### 理解

jQuery是一个免费的开源的轻量级的js库，兼容css3和各种浏览器，jQuery 2.0以后的版本不支持IE6、7、8。宗旨是write less，do more ，可提供API让开发者编写插件



### 入口函数

```javascript
$(function(){
    //DOM加载完成的入口
})
$(document).ready(function(){
    //DOM加载完成的入口
})
```

- 等着DOM结构渲染完毕即可执行代码，不必等到所有外部资源加载完成，相当于js中的DOMContentLoaded
- 不同于load事件：页面文档、外部的js文件、css文件、图片加载完毕才能执行内部代码



### 顶级对象 $

- \$是JQuery的别称，可以使用JQuery代替$
- \$是JQuery的顶级对象，相当于JS中的window。把元素利用$包装成JQuery对象，就可以调用JQuery的方法



### JQuery对象和DOM对象

1. 用原生JS获取的对象是DOM对象
2. 用JQuery方法获取的元素是JQuery对象
3. JQuery对象的本质：利用$对DOM对象包装后产生的对象（伪数组形式存储）

**相互转换**

1. DOM→JQuery

   $('div')   /   \$(mydiv)

2. JQuery→DOM

   $('div')[index]     /   \$('div').get(index)    index是索引号



### 选择器

| 用法            | 描述                                                 |
| --------------- | ---------------------------------------------------- |
| $('#id')        | 获取指定ID的元素                                     |
| $('*')          | 匹配所有元素                                         |
| $('.class')     | 获取同一类class的元素                                |
| $('div')        | 获取同一类标签的所有元素                             |
| $('div,p,li')   | 选取多个元素                                         |
| $('li.current') | 交集元素                                             |
| $('ul>li')      | 获取亲儿子层级的元素。并不会获取孙子层级的元素       |
| $('ul li')      | 使用空格，后代选择器，获取ul下的所有li元素，包括孙子 |
| $('li:first')   | 获取第一个li元素                                     |
| $('li:last')    | 获取最后一个li元素                                   |
| $('li:odd')     | 获取到li元素中索引号为2的元素，索引号从0开始         |
| $('li:even')    | 获取到的li元素中，选择索引号为奇数的元素             |
| $('li:eq(2)')   | 获取到的li元素中，选择索引号为偶数的元素             |



### 隐式迭代

遍历内部DOM元素（伪数组形式存储）的过程叫==隐式迭代==

给匹配到的所有元素进行循环遍历，执行相应的方法，而不用再进行循环，方便调用



### 筛选方法

| 语法               | 说明                                     |
| ------------------ | ---------------------------------------- |
| parent()           | 查找父级                                 |
| children(selector) | 相当于$('ul>li'),最近一级（亲儿子）      |
| find(selector)     | 相当于$('ul li')后代选择器               |
| siblings(selector) | 查找兄弟节点，不包括自己本身             |
| nextAll([expr])    | 查找当前元素之后所有的同辈元素           |
| prevAll([expr])    | 查找当前元素之前所有的同辈元素           |
| hasClass(class)    | 检查当前元素是否包含某个类，有就返回true |
| eq(index)          | 相当于$('li:eq(2)')   index从0开始       |



### 操作CSS方法

1. 只写属性名，返回属性值

​    `$(this).css('color');`

2. 参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号

   `$(this).css('color','red')`

3. 参数可以是对象形式，方便设置多组样式。属性可以不加引号

   `$(this).css({color:'red',font-size:'20px'})`



### 设置类样式方法

1. 添加

   `$('div').addClass('current');`

2. 移除

   `$('div').removeClass('current');`

3. 切换

   `$('div').toggleClass('current');`



### 自定义动画animate

animate(params,[speed],[easing],[fn])

params:想要更改的样式属性，以==对象==形式传递，必须写。属性名可以不用带引号，复合属性要采用驼峰命名法



### 属性操作

**设置或获取元素固有属性值 prop()**

**设置或获取元素自定义属性值 attr()**

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                

### 内容文本值

**普通元素内容** html()（相当于原生inner HTML)

​	获取：html()   // 获取元素的内容

​	设置：html(''内容'')   // 设置元素的内容

**普通元素文本内容** text()   (相当与原生innerText)

​	获取：text()   // 获取元素的文本内容

​	设置：text(''文本内容'')   // 设置元素的文本内容

**表单的值** val()（ 相当于原生value)

​	获取：val()   // 获取表单的值

​	设置：val(''内容'')  // 设置表单的值



### **数据缓存** **data()**【了解】

```
data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构，所以元素上无法查看。一旦页面刷新，之前存放的数据都将被移除。
```

 **附加数据语法**

data(''name'',''value'')   // 向被选元素附加数据   

**获取数据语法**

date(''name'')             //   向被选元素获取数据  



### 遍历元素

jQuery 隐式迭代是对同一类元素做了同样的操作。如果想要给同一类元素做不同操作，就需要用到遍历

> 语法1：$("div").each(function(index, domEle) { xxx; }）

```
1. each() 方法遍历匹配的每一个元素。主要用DOM处理。 each 每一个
2. 里面的回调函数有2个参数：  index 是每个元素的索引号;  demEle 是每个DOM元素对象，不是jquery对象
3. 所以要想使用jquery方法，需要给这个dom元素转换为jquery对象  $(domEle)
```

语法2：$.each(object，function(index, element){ xxx;}）

```
1. $.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象
2. 数组的话：index 是每个元素的索引号;  element  遍历内容
3. 对象的话：index 是属性名;  element 是属性值
```



### 操作元素

- **创建元素**

> 语法：$(''<li></li>'');    

- **内部添加**

> element.append(''内容'') [把内容放入匹配元素内部最后面，类似原生 appendChild。]
>
> element.prepend(''内容'') 把内容放入匹配元素内部最前面。

- **外部添加**

> element.after(''内容'') // 把内容放入目标元素后面
>
> element.before(''内容'')    //  把内容放入目标元素前面 

- **删除元素**

> element.remove()   //  删除匹配的元素（本身）
>
> element.empty()    //  删除匹配的元素集合中所有的子节点
>
> element.html('')   //  清空匹配的元素内容



### **jQuery 尺寸**

> width()、height()【只算width和height】
>
> innerWidth()、innerHeight()【包含padding+width】
>
> outerWidth()、outerHeight()【包含padding、border、width】
>
> outerWidth(true)、outerHeight(true)【包含padding、border、margin、width】

```
以上参数为空，则是获取相应值，返回的是数字型。
如果参数为数字，则是修改相应值。
参数可以不写单位。
```



### **jQuery 位置**

> 位置主要有三个： offset()、position()、scrollTop()/scrollLeft();

**offset()设置或获取元素偏移**

```
①offset() 方法设置或返回被选元素相对于文档的偏移坐标，跟父级没有关系。

②该方法有2个属性 left、top 。offset().top  用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离。

③可以设置元素的偏移：offset({ top: 10, left: 30 });
```

**position()** 获取元素偏移

①position() 方法用于返回被选元素相对于**带有定位的父级**偏移坐标，如果父级都没有定位，则以文档为准。

②该方法有2个属性 left、top。position().top 用于获取距离定位父级顶部的距离，position().left 用于获取距离定位父级左侧的距离。

**注意：该方法只能获取。**

scrollTop()、scrollLeft()设置或获取元素被卷去的头部和左侧

①scrollTop() 方法设置或返回被选元素被卷去的头部。

②不跟参数是获取，参数为不带单位的数字则是设置被卷去的头部。

 **案例带有动画的返回顶部**

```
 $('body,html').animate({scrollTop: 0})
```



### **事件处理on()绑定事件**

> on() 方法在匹配元素上绑定一个或多个事件的事件处理函数

> 语法：element.on(events,[selector],fn)

**on() 方法优势1：**

1、可以绑定多个事件，多个处理事件处理程序。 

```
 $(“div”).on({
  mouseover: function(){}, 
  mouseout: function(){},
  click: function(){}  
});       
```

**on() 方法优势2：**

> 可以事件委派操作。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。

```
$('ul').on('click', 'li', function() {
  alert('hello world!');
});    
```

> 在此之前有bind(), live()，delegate()等方法来处理事件绑定或者事件委派，最新版本的请用on替代他们。  

**on() 方法优势3：**

> 动态创建的元素，click()没有办法绑定事件，on() 可以给动态生成的元素绑定事件



### **事件处理** **off()** **解绑事件**

> off() 方法可以移除通过 on() 方法添加的事件处理程序。

```
$("p").off() // 解绑p元素所有事件处理程序
$("p").off( "click")  // 解绑p元素上面的点击事件 后面的 foo 是侦听函数名
$("ul").off("click", "li");   // 解绑事件委托
```

> **如果有的事件只想触发一次， 可以使用 one()来绑定事件**



### 自动触发事件trigger()

> 有些事件希望自动触发, 不必鼠标点击触发

> element.click()  // 第一种简写形式

> element.trigger("type")//第二种自动触发模式

```
$("p").on("click", function () {
  alert("hi~");
}); 
$("p").trigger("click"); // 此时自动触发点击事件，不需要鼠标点击
```

> element.triggerHandler(type)  // 第三种自动触发模式

> triggerHandler模式不会触发元素的默认行为



### jQuery事件对象

> 事件被触发，就会有事件对象的产生。

```
element.on(events,[selector],function(event){})       
```

```
阻止默认行为：event.preventDefault() 或者 return false 
阻止冒泡： event.stopPropagation()      
```



### 多库共存

- 问题概述：

  > JQuery是用$作为表示符，随着JQuery的流行，其他js库也会用\$作为标识符，就会有冲突

- 解决冲突，让不同的库可以同时存在，叫做**多库共存**

- 解决方案：

  > 1. 把$统一改为jQuery
  > 2. JQuery变量规定新的名称： $.noConflict()      /      var xx = \$.noConflict();



### jQuery对象拷贝

语法：`$.extend([deep],target,obj1,[objN]);`

1. deep:默认false 浅拷贝     设为true为深拷贝
2. target：要拷贝的目标对象
3. obj1：待考贝到目标对象的对象
4. objN：待考贝到目标对象的第N个对象
5. 浅拷贝是把被拷贝的对象==复杂数据类型中的地址==拷贝给对象，修改目标对象==会影响==被拷贝对象
6. 深拷贝，前面加true，完全克隆（拷贝的对象，而不是地址），修改目标对象==不会影响==被拷贝对象



### jQuery插件

```
 jQuery插件常用的网站：
  jQuery 插件库  http://www.jq22.com
  jQuery 之家   http://www.htmleaf.com
```



### 图片懒加载（BOOTSTRAP插件）

图片使用延迟加载在可提高网页下载速度。它也能帮助减轻服务器负载

**注意：**

​	1、要引入JQuery

​	2、插件JS【js引入文件和js调用必须写到 DOM元素（图片）最后面】

​	3、将图片 src 替换为 data-lazy-src

​	4、调用lazyLoadInit(）



