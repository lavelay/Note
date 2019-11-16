## vue-介绍

Vue.js (view)是一套构建用户界面的前端<font color=red>框架</font>技术

Vue只关注**视图**（页面）层的开发，文档非常丰富、易于上手，流行度高，拥抱经典的web技术、早起灵感来源于angular

Vue.js 不支持 IE8 及其以下版本



### 插值表达式

如果{{}}使用中有冲突，想更换为其他标记，可以这样：

```js
delimiters:['${'，'}$']  // 标记符号变为${}$了 
```

1. 在插值表达式中 只能设置**简单**的javascript表达式语句，不能设置**复杂**表达式(例如for循环)
2. 在不改变vue变量值大小的前提下，可以进行一般的 **算术**运算、**比较**运算、**逻辑**运算、**三元**操作符 等运算使用，也可以通过**常量**进行数据体现
3. 插值表达式只能用在html标签的**内容区域**；不能用在其他地方



### v-cloak

设置display：none，解决闪烁问题

### v-text

v-text与{{}}的作用是一样的，都是操控 标签的**内容区域**信息

```html
<标签 v-text="表达式"> </标签>
```

1. 虽然v-text 是标签的属性，但是属性值会添加到标签的内容区域中
2. v-text 的属性值一般要求是普通字符串，如果是html标签，标签的**<>箭头符号**会变为符号实体
3. 如果 标签 内容区域 有默认信息，则会被v-text覆盖掉
4. v-text 可以进行 变量、常量、算术符号、比较符号、逻辑符号、三元运算符号等运算

### v-text-闪烁

网速非常慢的时候，{{}}  有**闪烁**问题，而 v-text没有(属性就是不会显示出来的)

### v-html

v-html 与 v-text、{{ }} 的作用一样，都是操控 标签的**内容区域**

`v-html、v-text、{{ }}的异同`：

1. v-html对 **html标签** 和 **普通文本** 内容都可以设置显示

2. v-text、{{ }}  只针对  **字符串** 起作用，如果数据中有html标签，那么标签的箭头符号要做<font color=red>符号实体</font>转换，进而使得浏览器上直接"显示箭头"等标签内容，等同于不解析html标签内容

   > <  变为  \&lt;    // less than
   >
   > \> 变为  \&gt;     // great than

3. v-html和v-text没有闪烁问题

4. 它们都可以进行 **变量**、**常量**、**算术运算**、**比较运算**、**逻辑运算**、**三元运算**等技术应用

`默认内容`

```html
<p>{{score}}默认内容</p>
<p v-text="score">默认内容</p>
<p v-html="score">默认内容</p>
```

> 以上三者，v-text和v-html标签有默认内容，但是都会被覆盖掉，而 插值表达式 不会覆盖

1. v-html尽量避免使用(除非完全掌控)，否则会带来危险(XSS攻击 跨站脚本攻击)
2. 标签的默认内容会被v-html覆盖



#### 属性绑定-class属性

1. 数组

```
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>
```

2. 数组中使用三元表达式

```
<h1 :class="['red', 'thin', isactive?'active':'']">这是一个邪恶的H1</h1>
```

3. 数组中嵌套对象

```
<h1 :class="['red', 'thin', {'active': isactive}]">这是一个邪恶的H1</h1>
```

4. 直接使用对象

```
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```

通过数组方式给class绑定多个值，值如果不是 Vue成员、数值、布尔值，相反就是普通的字母字符串内容，则需要通过**单引号**圈选

### 使用内联样式

1. 直接在元素上通过 `:style` 的形式，书写样式对象

```
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```

2. 将样式对象，定义到 `data` 中，并直接引用到 `:style` 中

 + 在data上定义样式：

```
data: {
   h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
```



## v-for和key

1. 迭代数组

```js
  <li v-for="(item, i) in list">
  索引：{{i}} --- 姓名：{{item.name}} --- 年龄：{{item.age}}
	</li>
```

2. 迭代对象中的属性

```js
	<!-- 循环遍历对象身上的属性 -->
    <div v-for="(val, key, i) in userInfo">{{val}} --- {{key}} --- {{i}}</div>
```

3. 迭代数字

```js
<p v-for="i in 10">这是第 {{i}} 个P标签</p>
```

4. key属性

```js
 //		v-for 循环的时候，key 属性只能使用 number或string -->
  //  key 在使用的时候，必须使用 v-bind 属性绑定的形式，指定 key 的值 -->
    <p v-for="item in list" :key="item.id">
      <input type="checkbox">{{item.id}} --- {{item.name}}
    </p>
```



## v-if和v-show

> v-if 有更高的切换消耗    每次都会重新删除或创建元素 
>
> v-show 有更高的初始渲染消耗     只是切换了元素的 display:none 样式
>
> 如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好



### v-on(@)

#### 事件绑定-传递参数

1. 有声明()，也有传递实参，形参就代表被传递的实参
2. 没有声明()，第一个形参就是**事件对象**
3. 有声明(),但是没有传递实参，形参就是**undefined**

#### 事件绑定-访问data成员

根据业务需要，事件在执行过程中需要对Vue实例的data数据进行操作，通过<font color=red>this关键字</font>实现，

this代表Vue实例对象，并且针对data或methods成员都可以直接进行调用

#### 事件绑定-this是谁

在Vue实例内部包括不限于methods方法中，this关键字 是对象，具体与 new Vue() 是一样的

> this ===  vm 

并且其可以对 **data** 和 **methods**成员进行直接访问



### v-model

v-model是vue中 唯一实现 <font color=red>双向数据绑定</font>  指令

v-bind<font color=red>单向</font>数据绑定，只是使得vue的数据渲染给页面元素，页面对数据进行修改，vue不会感知到

v-model<font color=red>双向</font>数据绑定，数据从vue里边渲染给页面，页面对其进行修改，Vue内部会立即感知

```html
<标签 v-model="data成员"></标签>
```

2. v-model只针对**value属性**可以绑定，因此经常用在form表单标签中，例如input(输入框、单选按钮、复选框)/select(下拉列表)/textarea(文本域)

3. v-model只能绑定**data成员**，不能设置其他表达式，否则错误

   > 例如 
   >
   > v-model="score+100"  错误
   >
   > v-model="120"  错误
   >
   > v-model="score" 正确的



#### 响应式

vue实例的data数据如果发生变化，那么页面上用到的地方会重新编译执行，这样就把更新后的内容显示出来了

这个过程就是“响应式”

`步骤`：

1. 页面初始加载，vue的数据<font color=red>渲染</font>给div容器

2. 通过v-model修改数据，修改的信息会直接反馈给vue内部

3. vue的数据发生变化，页面上(也包括Vue实例本身)用到该数据的地方会<font color="red">重新编译渲染</font>

   > 2和3 步骤在条件满足情况下会**重复**执行



#### 简易原理

给input输入框中定义oninput事件，在该事件中把用户输入的信息都给随时获得到，并对data成员进行赋值

data成员变化了，页面上用到的地方就重新渲染，达成简易双向绑定的效果

> oninput：是事件，可以随时感知输入框输入的信息

`具体设置`：

```html
<div id="app">
  <p>{{city}}</p>
  <p><input type="text" :value="city" ></p>
  <p><input type="text" @input="city=$event.target.value" :value="city">$event玩法</p>  
  <p><input type="text" @input="ganzhi" :value="city">methods玩法</p>  
</div
<script src="./vue.js"></script>
<script>
  var vm = new Vue({
    el:'#app',
    data:{
      city:'大连'
    },
    methods:{
      ganzhi(evt){
        // evt: 键盘事件对象
        // console.log(evt)  // InputEvent对象
        // evt.target:代表触发当前事件的html元素dom对象，具体是input框对象
        // evt.target.value: 随时感知输入框输入的信息

        // 把随时输入的信息赋予给city，这样city变化，由于“重新渲染”，页面上用到的地方就更新了
        // 就达成v-model双向绑定的效果了
        this.city = evt.target.value
      }
    }
  })
</script>
```

1. 事件声明没有小括号()，**第一个形参**就是 事件对象

2. 事件声明，本身可以直接使用**$event**,其也是事件对象




#### 其他表单域使用(自学)

- 绑定多行文本框

  ```php+HTML
  <textarea v-model="name"></textarea>
  <div>{{ name }}</div>
  ```
  
> 多行文本框中不要使用`{{ name }}`的方式绑定，如果这样就没有双向绑定效果了


- 绑定复选框

  - 绑定一个复选框

    ```html
    遵守协议：<input type="checkbox" v-model="xieyi">
    <div>{{ xieyi }}</div>    <!-- 体现 true 或  false信息-->
    <script>
        var vm = new Vue({
           el: '#app',
            data: {
                xieyi: true
            }
        })
    </script>
    ```
  
- 绑定多个复选框
  
  ```HTML
    吃饭：<input type="checkbox" value="eat" v-model="hobby"><br>
    睡觉：<input type="checkbox" value="sleep" v-model="hobby"><br>
    敲代码：<input type="checkbox" value="qiao" v-model="hobby"><br>
    {{ hobby }}    <!-- 体现数组信息  ['eat','sleep','qiao']-->
    <script>
        var vm = new Vue({
           el: '#app',
            data: {
                hobby: []
            }
        });
    </script>
  ```
  
  > 此种方式需要input标签提供<font color=red>value</font>属性
  >
    > hobby：体现 ['eat','sleep','qiao']的数组信息
  
- 绑定单选框

  ```html
  男<input type="radio" name="xingbie" value="男" v-model="sex">
  女<input type="radio" name="xingbie" value="女" v-model="sex">
  <p>{{sex}}</p>  <!-- 体现 男 或 女 的字符串信息-->
  <script>
      var vm = new Vue({
         el: '#app',
         data: {
           sex: ''
         }
      });
  </script>
  ```
  
- 绑定下拉列表

  ```html
  <div id="example-5">
    居住城市：
    <select v-model="mycity">
      <option disabled value="">请选择</option>
      <option value="B">北京</option>
      <option value="S">上海</option>
      <option value="G">广州</option>
    </select>
    <span>Selected: {{ mycity }}</span> <!--mycity: 体现为 B、S、G等字符串信息-->
  </div>
  <script>
      var vm = new Vue({
         el: '#app',
          data: {
              mycity: 'S'
          }
      });
  </script>
  ```
  



### 事件修饰符：

+ .stop       阻止冒泡

+ .prevent    阻止默认事件

+ .capture    添加事件侦听器时使用事件捕获模式

+ .self       只当事件在该元素本身（比如不是子元素）触发时触发回调

+ .once       事件只触发一次



## 过滤器

**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache 插值和 v-bind 表达式**。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符指示；

### 私有过滤器

1. HTML元素：

```
<td>{{item.ctime | dataFormat('yyyy-mm-dd')}}</td>
```

2. 私有 `filters` 定义方式：

```js
filters: { // 私有局部过滤器，只能在 当前 VM 对象所控制的 View 区域进行使用
    dataFormat(input, pattern = "") { // 在参数列表中 通过 pattern="" 来指定形参默认值，防止报错
      }
    }
  }
```



### 全局过滤器

```js
// 定义一个全局过滤器

Vue.filter('dataFormat', function (input, pattern = '') {
  
});
```

> 注意：当有局部和全局两个名称相同的过滤器时候，会以就近原则进行调用，即：局部过滤器优先于全局过滤器被调用！



## 键盘修饰符

### [2.x中自定义键盘修饰符](https://cn.vuejs.org/v2/guide/events.html#键值修饰符)

1. 通过`Vue.config.keyCodes.名称 = 按键值`来自定义案件修饰符的别名：

```
Vue.config.keyCodes.f2 = 113;
```

2. 使用自定义的按键修饰符：

```
<input type="text" v-model="name" @keyup.f2="add">
```

3. **ESC键** 被触碰就把已经输入的给做清除操作，取消添加

```html
<input type="text" v-model="newbrand" @keyup.esc="newbrand=''" />
```



## [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

1. 自定义全局和局部的 自定义指令：

```js
// 自定义全局指令 v-focus，为绑定的元素自动获取焦点：
    Vue.directive('focus', {
      inserted: function (el) { // inserted 表示被绑定元素插入父节点时调用
        el.focus();
      }
    });
// 自定义局部指令 v-color 和 v-font-weight，为绑定的元素设置指定的字体颜色 和 字体粗细：
     directives: {
       color: { // 为元素设置指定的字体颜色
         bind(el, binding) {
           el.style.color = binding.value;
         }
       },
      'font-weight': function (el, binding2) { // 自定义指令的简写形式，等同于定义了 bind 和 update 两个钩子函数
         el.style.fontWeight = binding2.value;
       }
     }

// 1. 声明全局指令
Vue.directive(指令名称,{ 配置对象成员 })

// 2. 声明私有指令
new Vue({
  directives:{
    指令名称:{ 配置对象成员 }
  }
})
配置对象：
inserted(m){m代表使用该指令的html标签dom对象，可以通过m进行业务需求实现}
```

2. 自定义指令的使用方式：

```
<input type="text" v-model="searchName" v-focus v-color="'red'" v-font-weight="900">
```



## vscod设置代码片段

vscode编辑器：设置--->User snippets---->html.json，配置如下内容

```json
"Print to Vue&html base code": {
		"prefix": "vh",
		"body": [
			"<!DOCTYPE html>",
			"<html lang=\"en\">",
			"<head>",
			"  <meta charset=\"UTF-8\">",
			"  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">",
			"  <meta http-equiv=\"X-UA-Compatible\" content=\"ie=edge\">",
			"  <title>Document</title>",

			"</head>",
			"<body>",
			"  <div id=\"app\">",
			"  </div>",
			"  <script src=\"./vue.js\"></script>",
			"  <script>",
			"    var vm = new Vue({",
			"      el:'#app',",
			"      data:{",
			"      },",
			"      methods:{",
			"      }",
			"     });",
			"  </script>",
			"</body>",
			"</html>",

			"",
		],
		"description": "Vue&html base code"
	}
}
```



## vue指令-v-if&v-else

在Vue中，v-if 、v-else-if 和 v-else 三个指令结合可以实现多路<font color=red>分支</font>结构

- v-if可以**单独**使用，形成单路分支结构
- v-if  和 v-else 也可以合作使用，实现**双路**分支结构
- v-if  、v-else-if 和 v-else 也可以合作使用，实现**多路**分支结构

`语法`：

```html
<标签 v-if="true/false"></标签>
<标签 v-else-if="true/false"></标签>
<标签 v-else-if="true/false"></标签>
<标签 v-else></标签>
```

> 以上4个标签只分支结构，最终只会走一个，第一个为true的那个标签会执行  或 执行else标签

判断品牌信息是否存在，并显示对应内容

```html
<table v-if="brandList.length>0">
  ……
</table>
<table v-else>
  <tr><td colspan="100">没有任何记录！</td></tr>
</table>
```



## computed计算属性应用

```js
new Vue({
  computed:{
    属性名称:function(){
      // 业务表达式实现，可以通过this操作data成员
      return  返回结果
    }
  }
})
```

`使用`：

形式上，如何应用data成员，就如何应用计算属性

```js
{{ computed计算属性名称 }}
```

`特点`：

1. 计算属性关联的data如果发生变化，会重新编译执行 获得 并 使用 对应新结果，即响应式

2. 计算属性内部可以使用this关键字，与Vue对象等效

3. 每个计算属性都需要通过return关键字返回处理结果

`与methods方法的区别`：

computed计算属性本身有“**缓存**”，在关联的data没有变化的情况下，后续会使用缓存结果，节省资源

methods方法没有缓存，每次访问 方法体 都需要加载执行，耗费资源



### template

```html
<div id="app">{{ city }}</div>
<script src="./vue.js"></script>
<script>
  var vm = new Vue({
    template: "<span>上海</span>",
    el: "#app",
    data: {
      city: "北京"
    }
  })
</script>
```

> 上述代码执行，页面上会看到“span上海”内容，相反“div北京”已经被覆盖了



### $mount

如果Vue没有提供`el`成员帮助找到div容器，那么可以调用$mount()方法

因此Vue实例与容器联系有两种方式：

1) el:'#app'

2) $mount方式

```js
vm.$mount('#app')
var vm = new Vue().$mount('#app')  // 连贯调用
```



### render成员

优先级关系：render >>>>> template >>>>>>默认容器

```html
<div id="app">{{ city }}</div>
<script src="./vue.js"></script>
<script>
  var vm = new Vue({
      el:'#app', // 使得Vue实例 与 div容器联系
      data:{
        city:'北京'
      },
      template:'<p>天津</p>',
      render:h=> h('span','广州')  // <span>广州</span>
  });
</script>
```

> 上述代码会看到 span广州 内容，相反 p天津 和 div北京 都被覆盖了



### console使用

```js
console.dir()   可以把dom对象的各个成员给打印出来
console.group()  对输出的信息做分组处理，更加清楚
console.log('%c%s',css样式设置, 被输出的信息)
c:css样式  与 第2个参数对应
s:string字符串 与  第3个参数对一个
console.log('%c%s','color:red', '你好')
```



## 生命周期

从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！

[生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)：就是生命周期事件的别名而已；

生命周期钩子 = 生命周期函数 = 生命周期事件

生命周期分为3个阶段，分别是[创建]()、[运行]()、[销毁]()

### 创建阶段分析

创建阶段一共有4个方法，它们与 el、data都是并列关系的

```js
new Vue({
  beforeCreate(){   },
  created(){  },
  
  beforeMount(){   },
	mounted(){  },
})
```

> beforeCreate：此时Vue对象刚创建好，没有任何成员，data、methods等都没有呢，只有this
>
> created：此时vue对象已经长大一点，内部已经完成了data、methods等成员的设置，也是data初始化的最好时机
>
> beforeMount：此时vue实例已经把div容器给获得到了，但是内部的vue指令等信息还没有被编译处理
>
> mounted：此时，vue获取到的div容器内部的原生指令已经被编译处理好了，并且也完成了容器的渲染工作，此时模板中已经看不到vue原始指令了



created: 一般用于页面"首屏"数据的获取操作(获取好的数据可以直接赋予给data使用，此方法已经把data做好了，其可以做到**第1 时间**就把数据赋予给data)

mounted: 一般用于初始页面dom元素操作使用

​	创建阶段各个方法不设置则以，设置后就会**自动**执行，并且会**顺序**只执行**一次**

### 运行和销毁阶段分析

`运行阶段`：

```js
new Vue({
	beforeUpdate(){ 可以感知到数据变化之前页面上关于该数据的样子 }
	updated(){ 可以感知到数据变化之后页面上该数据的样子 }
})
```

> 运行阶段方法**不会**自动执行，当data成员数据发生变化，就执行了，并且数据变化多次，方法也会**重复**执行多次

`销毁阶段`：

```js
new Vue({
	beforeDestroy(){ 实例销毁之前 }
	destroyed(){ 实例销毁之后 }
})
```

> 当vue实例被销毁后，就要执行以上两个方法，vm.$destroy()

1. **运行阶段**各个方法与创建阶段不同，本身**不会**自动执行，需要数据变化的条件触发才会执行
2. **销毁阶段**各个方法也不会自动执行，需要Vue实例对象调用$destroy()方法



### VirtualDOM

`什么是VirtualDOM`：

div容器 在 Vue实例中存在的状态，就是  VirtualDOM(虚拟dom内容)，具体是内存信息的体现

在Vue实例运行期间，该VirtualDOM始终存在

`VirtualDOM作用`：

1. 编译解析div容器，并渲染给浏览器
2. 响应式体现




## axios

```js
axios.get('请求地址', {params:{name:value,name:value。。。。}})
axios.post('请求地址', {name:value,name:value。。。。})
```

`注意`：

get()方法如果传递参数需要额外设置params，post()方法则不用



## axios-拦截器-interceptors

axios在客户端与服务端之间传递数据时候是有**时间消耗**的

网络好、服务器比较空闲，axios的执行速度快

网络不好、服务器比较繁忙，axios的执行速度慢(这时用户需要多等待)

axios无论执行速度快还是慢，用户都需要等待，如果在axios执行时页面给予一定的**提示**，那么用户体验就比较好，这时候[拦截器]()就可以应用上



axios本身有两种拦截器：[请求拦截]()、[响应拦截]()

- 请求拦截器：

​	axios每次<font color=red>开始</font>请求的时候先执行此处逻辑，在这个地方可以给axios做出发前的配置，也可以做出发前的检查工作，检查ok的情况下就开始向服务器端发请求

- 响应拦截器：

​	axios<font color=red>完成</font>与服务器端交互回到客户端后就执行此处逻辑，在这个地方可以做一些后续收尾事宜，例如判断axios请求是否成功，或相关数据过滤操作

`请求拦截器代码`：

```js
// 请求拦截器
axios.interceptors.request.use(function (config) {
  // 放置业务逻辑代码
  return config;
}, function (error) {
  // axios发生错误的处理
  return Promise.reject(error);
});
```

`响应拦截器代码`：

```js
// 响应拦截器
axios.interceptors.response.use(function (response) {
  // 放置业务逻辑代码
  // response是服务器端返回来的数据信息，与Promise获得数据一致
  return response;
}, function (error) {
  // axios请求服务器端发生错误的处理
  return Promise.reject(error);
});
```

`注意`：

1. 各个拦截器的第一个函数参数需要设置为 “**箭头函数**” ，使得内部this与外部保持一致，都是Vue实例
2. 各个拦截器需要设置在created中，因为需要**第1时间**就操控data成员showflag，再者可以使得各个拦截器被“自动”执行
3. 注意保持一个created



### 细节说明

1. config参数

   config是一个对象 与  axios.defaults 相当(不等于)

   config可以给axios配置例如baseURL的信息的

2. response参数

   服务器端给返回的具体数据信息，可以接收使用，axios应用的具体信息是该response的体现

3. Promise.reject()

   Promise.reject(data)  是 **语法糖**的用法，本质与下述一致，即返回一个Promise对象

   ```js
   Promise.reject(data)
   上下效果一致
   new Promise(function(resolve,reject){
     reject(data)
   })
   
   Promise.resolve(data)
   上下效果一致
   new Promise(function(resolve){
     resolve(data)
   })
   ```

   

## vue-组件(重要)

`什么是`：

​	组件是拥有一定功能许多html标签的集合体

`好处`：

答：模板中为了实现一个效果(例如分页)，需要绘制**20**个html标签，现在使用组件了，相同的功能就只绘制**一个**组件标签就达成了，明显提升开发速度

### 区分大小写

HTML中对大小写不敏感，默认都转为小写，如果配置对象时名称含有大写字母，在使用组件是名称要用短横线连接

### 私有组件语法

`声明私有组件语法`：

```js
new Vue({
  components:{
    '组件的名称': { 配置对象成员 }, 
    '组件的名称': { 配置对象成员 }...
  },
})
```

`注意`：

1. template是组件的成员之一，还有其它成员
2. template设置的各个html标签需要有<font color=red>唯一的根元素</font>节点，上例为ul

3. 组件名称建议是 xx-yy 的格式



```html
<组件名称></组件名称>
```

> 组件形式上 就是html标签



### 相关成员

可以认为**组件**是特殊的**Vue实例**，拥有着与Vue实例大致相同的**成员**

`注意`：

​	组件data成员 与 Vue实例的 不一样，需要通过 function/return 设置，通过return返回一个{}对象供使用

`案例应用`：

给分页组件设置 单击事件、data成员、created生命周期  方法并执行

```js
// 声明私有组件
components:{
  // 组件名称:{配置对象成员}
  'com-page':{
    // template: 设置组件拥有的html标签内容
    template:`
      <ul>
        <li><a href="#">{{ prev }}</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#">2</a></li>
        <li><a href="#">3</a></li>
        <li @click="xia()"><a href="#">{{ next }}</a></li>
      </ul>
    `,
    data(){
      return {
        prev:'上一页',
        next:'下一页'
      }
    },
    methods:{
      xia(){
        console.log('进入下一页')
      }
    },
    created(){
      console.log('created 已经执行了')
    }
  }
},
```



### function声明data

组件中声明的data成员，值需要是一个function，内部通过return返回{}对象供使用，这个特性必须遵守

`为什么组件的data必须是一个function`：

答：组件根据业务需要，可以被使用多次，function会使得每次组件使用的时候都**亲自执行**并给当前应用分配一个**独立的数据对象**，这样多个组件的data数据是独立的，互相没有关联、牵扯，互相不会覆盖

​      相反，如果直接通过{}对象 给data赋值，多次使用组件会造成大家的data都是共享的，就是一份数据，一个组件修改data后，其他组件都受到影响，这与业务逻辑是相违背的



### 全局组件语法

`全局组件语法`：

```
Vue.component(名称,{配置对象成员})
new Vue()
```

​	全局组件需要在new Vue之前设置



## yarn方式安装依赖包

`与npm区别`：

yarn安装更快，会同时安装多个，而npm按照队列一个一个顺序去安装，必须等到当前的package安装完毕后才能去安装下一个

`安装`：

```
npm install  -g  yarn
```

>    // 全局方式安装yarn依赖包，这样在系统任何目录都可以使用yarn指令

`配置镜像源`：

```bash
yarn config get registry				// 查看当前使用的源
yarn config set registry https://registry.npm.taobao.org		// 配置为taobao的镜像源
```

`使用`：

```bash
yarn  add  依赖包  	==================  npm install  依赖包
yarn remove 依赖包 	=================  npm uninstall  依赖包
yarn               	==================  npm  i       // 安装全部依赖包
yarn -y init       	==================  npm -y init  // 创建package.json文件
yarn add global 依赖包 ================  npm i -g 依赖包  // 全局方式装包
```



## VueCLI

`什么是`

答：是脚手架，其可以把许多项目**通用的依赖包**(vue、webpack、路由、vuex、less编译器等等) 和 **通用的配置**都给做好安装好，使得开发者全部的注意力都集中在业务层面，明显提升开发效率的，真实项目都要使用脚手架开发。

依赖包：axios、vue等等都是依赖包，一个依赖包中有许多 模块



`安装vuecli`：

```bash
npm i -g @vue/cli   // 使用该方式安装
```

> 上述依赖包通过全局方式安装，完毕后在系统任何目录都会执行名称为"vue"的一个指令

> 依赖包安装完毕，会形成 在 C:\Users\ssh\AppData\Roaming\npm\node_modules\@vue\cli 目录

> vue --version  查看脚手架版本，现在默认是4.0.5版本(如果是2.9.6就是错误的，需要卸载重新安装)



`vuecli创建项目`：

```bash
vue  create  项目名称(01-pro)
```



### 创建项目结构文件

```
vue create my-project
```

![1561622952268](Image/img(online)/1561622952268.png)

![1565964186423](Image/img(online)/1565964186423.png)

![1561623170607](Image/img(online)/1561623170607.png)

![1561623274446](Image/img(online)/1561623274446.png)

![1563505874818](Image/img(online)/1563505874818.png)

> 上图的两个项目都不要选取

![1561623412365](Image/img(online)/1561623412365.png)

![1561623482895](Image/img(online)/1561623482895.png)

![1561623586580](Image/img(online)/1561623586580.png)

![1566010958700](Image/img(online)/1566010958700.png)

![1561623689667](Image/img(online)/1561623689667.png)

(题外话：当再次创建项目时，就可以选取之前配置好的项目，**一次性**完成项目的创建，不用再详细选取配置)

![1561623755361](Image/img(online)/1561623755361.png)

上边的20190628具体配置在如下文件，可以直接删除，以便恢复：

![1561692040822](Image/img(online)/1561692040822.png)



`注意`：

​	c:/用户/ssh/.vuerc文件被删除作用

1. 创建项目选取配置的小项目被清除了
2. 项目创建过程中会提示要求选取 yarn  或  npm  方式下载包

​	创建项目过程中需要安装许多依赖包，建议通过yarn方式安装，如果不是，可以删除 “ c:\用户\用户名\.vuerc  ”  文件后再重新执行 "vue  create  xxx"命令，此时会提示选取



### 结构文件说明

```js
|-- node_modules								// 项目需要的依赖包
|-- public										 // 静态资源存储目录
|   |-- index.html							// 项目主容器文件
|   |-- favicon.ico							// 项目默认索引图片
|-- src
|   |-- assets									// 放置一些静态资源文件，例如图片、图标、字体 
|   |-- components							// 公共组件目录
|   |-- views									  // 业务组件目录
|   |-- App.vue									// 顶层根基路由组件
|   |-- main.js									// 项目主入口文件(包括Vue实例也在这)
|-- .editorconfig								// 代码规范配置文件
|-- .eslintrc.js								// eslint代码规范检查配置文件
|-- .gitignore									// git上传需要忽略的文件格式
|-- babel.config.js							// babel配置文件
|-- yarn.lock										// 依赖包版本锁定文件
|-- package.json								// 项目基本信息配置文件
|-- postcss.config.js						// css预处理器配置文件
|-- vue.config.js								// webpack 配置文件(与webpack.config.js作用一致)
```

`注意`：

1. public/index.html文件是div容器所在文件

2. src/main.js是Vue实例所在文件




### 项目运行

`步骤`：

1. 修改src/main.js文件为如下内容

   ```js
   // import Vue from 'vue' // Vue实例有render可以使用的
   import Vue from 'vue/dist/vue.common.js' // Vue实例 没有 render时候可以使用的
   // import App from './App.vue'
   
   Vue.config.productionTip = false
   
   new Vue({
     data:{
       msg:'项目已经运行了'
     }
     // render: h => h(App)
   }).$mount('#app')
   ```

   

3. 修改vue.config.js文件内容如下

   ```js
   module.exports = {
     lintOnSave: false,
     devServer:{
       open:true, // 项目运行自动开启浏览器
       port:16699 // 给项目运行创建web服务的端口号码(1~65535之间)
     }
   }
   ```

   > 当前项目运行的时候会创建一个http服务，上述16699就是服务器的端口号码，
   >
   > open:true  项目运行的时候，会**自动**打开浏览器并呈现效果

4. 在终端中执行命令

   ```
    npm  run  serve
   ```

   > 上述命令需要在项目根目录下运行(01-pro目录下)
   >
   > serve:指令标志是package.json文件配置好了

> 现在项目可以运行了，并且有实时加载的效果，业务文件随时改变，浏览器随时查看到对应效果



## ES6模块化

项目中一些**程序代码**经常被其他业务场景使用，为了避免重复开发，就把这些代码设置为**共享模式**，共享模式就是**模块化**。像jquery、axios、vue等等都是模块化的体现，需要的时候直接拿过来用即可 

`模块化技术有哪些`：

CommonJS(nodejs)、ES6模块化、AMD、CMD等

`CommonJS`：

CommonJS模块化 是2009年发布的，是民间出品的，相对不正规，可以在nodejs中应用

```js
// 导出
module.exports = 对象
// 导入
var obj = require(模块文件)
```



`ES6模块化`：

ES6模块化 是2015年官方正式出品的，已经被纳入到JavaScript标准里边，也是js未来的标准，由于各种原因 nodejs和浏览器中现在还不能直接使用ES6模块化，要相信未来可以



`AMD模块化`：

 Asynchronous Module Definition  异步模块定义 

2009年诞生，可以实现浏览器中应用模块化技术



`CMD模块化`：

Common Module Definition 通用模块定义

2011年诞生，阿里公司出品，可以实现浏览器中应用模块化技术



各个模块化应用的场合：

1. commonjs模块化可以应用在nodejs中，浏览器中不可以
2. es6模块化暂时还不能在nodejs 和 浏览器 中使用，但是要相信，未来可以
3. 浏览器中可以运行的模块化名称为 AMD 和 CMD



[AMD、CMD、Commonjs、ES6模块化介绍](https://segmentfault.com/a/1190000015302578)



### 默认导出和导入

在一个js文件中，通过一个**对象**把全部的数据导出出去，就是**默认导出**

对默认导出的成员进行接收就是默认导入

`模块`：

一个js文件就是一个模块，前提是该文件有做**导出**动作

`导出语法`

```js
// 导出：
export default  对象
```

`导入语法`：

```js
// 导入：
import 名称  from  模块文件名字
```

1. 一个模块中 默认导出 只能进行**一次**
2. es6模块化现在只可以在VueCli项目中使用



### 按需导出和导入

哪些成员可以做按需导出导入处理？

答： **常量**、**对象** 、**函数** 三种信息可以做模块化应用 (var、let等变量用于模块化没有意义)

`导出语法`：

```js
export const  a = 10		// 常量
export function ab(){}  // 函数
export const  b = 20
export const cat = {name:'kitty',age:5} // 对象
...
```

> 注意：一般按需只做常量、函数导出，var/let变量不导出，本身没有意义

`导入语法`：

```js
import {xx,yy,zz} from 模块文件
import {xx as kk,yy as mm,zz as qq} from 模块文件
```

`注意`：

1. xx,yy,zz代表被导入的成员名称，与导出的要求一致

2. 成员不用全部都导入，根据需要，导入 **1个或多个或全部** 都可以
3. 如果导入进来的成员名称 与 当前环境名称 有冲突，可以设置别名，使用关键字as



导出：

```js
// 按需导出
export const a = 10
const b = 20

export const cat = {name:'kitty',age:4}
export function say(){
  return 'hi'
}
```

导入：

```js
// 2) 按需导入
// import {name,name..} from '模块'
import {a,  say as shuo} from './modules/02-按需导出.js'
console.log(a,shuo)
```



### 默认和按需同时导出和导入

有时，在一个模块中 默认 和 按需 导出会同时存在

`导出语法`：

```js
export const  a = 10    // 按需导出
export function ab(){}  // 按需导出
export default  对象/{}  // 默认导出
export const  b = 20
export function abc(){}
```

`注意`：

1. 一个模块只能  默认导出**一次**，按需导入可以设置多次
2. 默认导出  的语句没有前后顺序要求

`导入语法`：

```js
// 1) 分别导入
import 名称  from  模块
import  {xx,yy}  from  模块
// 2) 一并导入
import 名称,{xx,yy} from 模块
```

`注意`：

​	一并导入必须是 默认在"前"，按需在"后"



导出：

```js
// 默认按需导出
export default {city:'北京',weather:'雨'}
export const a = 10
const b = 20

export const cat = {name:'kitty',age:4}
export function say(){
  return 'hi'
}
```

导入：

```js
// 3) 默认按需导入
// a. 分别导入
// import 名称 from ''  // 默认
// import {xx,yy,zz} from '' // 按需
// b. 一并导入
// import 名称,{xx,yy,zz} from ''
import obj2, {a as aa,cat,say} from './modules/03-默认按需导出.js'
console.log('%c%s','color:green',obj2.city)
console.log('%c%s','color:green',aa)
console.log('%c%s','color:green',cat.name)
console.log('%c%s','color:green',say)
```



### 没有导出应用

项目开发时有的文件没有做导出动作(例如 css、less)，这样文件可以称为为 非模块文件，那么可以通过如下方式做导入

```
import  文件路径名
```

导出：

```js
// 没有导出
for(var i=0; i<5; i++){
  console.log(i)
}
```

导入：

```js
// 4) 没有导出的导入
// import '模块'
import './modules/04-没有导出.js'
```



## 单文件组件 

`什么是`：

​	把一个组件的全部内容汇合到**一个文件**中，文件名字是以`.vue`结尾的就称作**vue单文件组件**

`普通组件的缺点`：

普通vue组件  其代码 和 其它JS代码逻辑掺杂在一块儿，不易维护，优势没有发挥到极致！



### 最简单使用

```js
import Vue from 'vue/dist/vue.common.js' // Vue实例没有render要使用该vue
// import Vue from 'vue' // Vue实例有render要使用该vue(vue.runtime.common.js)

// es6模块化导入单文件组件-默认方式
// import 组件模块 from './components/01-第一个单文件组件.vue'
import ComOne from './components/01-第一个单文件组件.vue'

Vue.config.productionTip = false

new Vue({
  // 把导入进来的组件给注册好
  // components:{组件名称:{配置对象成员}} // 普通组件
  // components:{组件名称:组件模块} // 单文件组件
  // 组件名称推荐是“xx-yy”格式
  components:{
    'com-one':ComOne
  },
  data:{
    msg:'开始学习Vue单文件组件'
  }
}).$mount('#app')
```

`注意`：

1. 单文件组件的模板内容必须通过template实现,内部要求有**唯一根元素**
2. 单文件组件文件本身比较特殊，必须借助vuecli脚手架项目才可以运行



### 组织结构

1. template标签，内部要求有**唯一根元素**(推荐div)，template是html5标签，只运行，浏览器源代码不显示
2. script标签：该标签内部可以执行普通js代码，但是最主要的是内部可以通过**export  default {}** 导出一个对象，该对象的成员完全可以参考 **Vue实例**，类似 data、methods、created、filters、components等等都可以应用，各个成员都是为template模板服务的
3. style标签:设置css样式，作用给template内部的html标签使用
4. script和style如果不需要，可以不设置，template必须要写



### 私有注册应用

`私有方式注册语法`：

```js
new Vue({
  components:{
		组件名称: 组件模块,
		组件名称: 组件模块,
		组件名称: 组件模块,
	}
})
```

小结：

1. 单文件组件，每个组件都有3个部分（template/script/style）
2. template 是固定标签，内部要求有**唯一根元素**
3. script  导出一个对象     对象成员可以参考Vue实例
4. style 设置样式
5. 组件需要被main.js文件 引入、注册，之后index.html应用



### 全局注册介绍

`注册`：

```js
import 组件模块  from  'xxx.vue'       // .vue后缀可以不设置，系统已经准备好了

// 全局方式声明组件
Vue.component(组件名称, 组件模块)
Vue.component(组件名称, 组件模块)

var vm = new Vue({……})
```

`注意`：

​	组件注册的代码需要在new Vue()上边

​	

### scoped属性

默认情况下，vue单文件组件的style样式是[全局的]()，

如果在一个应用中使用了**多个**单文件组件，它们使用<span style="background-color:yellow;">相同选择器</span>为相同的元素设置了style样式，那么只有一个会起作用 (后者会覆盖前者)

`scoped作用`：

​	使得style的样式针对自己组件生效

`原理`：

​	给每个style标签都设置一个`scoped`属性，这样组件的各个html标签解析出来后都会带有一个与其他单组件标签不同的 <font color=red>data-v-xxx</font> 的唯一属性名称，style样式设定也会自动与这个的data-v-xxx联系起来，这样就使得style样式只针对自己的组件起作用了

```html
<style  scoped>
  xxxxx
</style>
```

`注意`：

尽管有scoped，但是不同的组件间还是尽量**不要使用相同名称**的选择器



### 父子嵌套组件应用

`步骤`：

1. 创建两个组件 05-Fat.vue  和  05-Son.vue  内容简单填充

   05-Son.vue内容：

   ```html
   <template>
       <div id="son">
         <p>我是儿子郭小达</p>
       </div>
   </template>
   
   <style scoped>
     #son{
       width:300px;
       height:100px;
       border:2px solid purple;
     }
   </style>
   ```

   

05-Fat.vue内容，对子组件做引入、注册、使用：

```html
<template>
    <div id="fat">
      <p>我是老子郭达</p>
      <!--3. 使用-->
      <com-son></com-son>
    </div>
</template>

<script>
  // 对其他组件做 导入、注册、使用
  // 1.导入
  import ComSon from './05-Son.vue'
  export default {
    // 2.注册
    components:{
      'com-son':ComSon
    }
  }
</script>

<style scoped>
  #fat{
    width:400px;
    height:200px;
    border:2px solid orange;
  }
</style>
```

   

2. 在src/main.js中 引入、注册  05-Fat.vue

   ```js
   import Vue from 'vue/dist/vue.common.js' // Vue实例没有render要使用该vue
   // import Vue from 'vue' // Vue实例有render要使用该vue(vue.runtime.common.js)
   
   // es6模块化导入单文件组件-默认方式
   // import 组件模块 from './components/01-第一个单文件组件.vue'
   import ComOne from './components/01-第一个单文件组件.vue'
   import ComTable from './components/03-Table.vue'
   
   Vue.config.productionTip = false
   // Vue.component('com-one',ComOne)
   // Vue.component('com-table',ComTable)
   
   new Vue({
     components:{
       'com-one':ComOne,
       'com-table':ComTable,
     },
     
     data:{
       msg:'开始学习Vue单文件组件'
     }
   }).$mount('#app')
   ```
   
   
   
3. 在public/index.html 应用 041-Fat.vue

   ```html
       <div id="app">
         {{msg}}
         <com-one></com-one>
         <hr />
         <com-table></com-table>
         <hr />
         <com-first></com-first>
         <com-second></com-second>
         <hr />
         <com-fat></com-fat>
       </div>
   ```

`嵌套本质`：

​	一个单文件组件可以  **引入**、**注册**、**使用** 另外一个单文件组件



### vscode安装扩展

设置 ------> user snippets ----->  vue.json,设置如下内容

```js
{	
	"Create vue template": {
		"prefix": "vuec",
		"body": [
		 "<template>",
		 "  <div>$1</div>",
		 "</template>",
		 "",
		 "<script>",
		 "  export default {",
		 "}",
		 "</script>",
		 "",
		 "<style lang=\"less\" scoped>",
		 "</style>",
		 "",
		],
		"description": "Create vue template"
	}
}
```

> 之后，在vue文件中就可以通过 “vuec” 代码片段创建组件结构内容了



### 父给子传值

父组件可以  引入、使用 子组件，从业务上看，该父组件有可能对子组件有**个性化**需求，为了体现组件的**灵活多变**，可以通过**传值**实现

`语法`：

父组件要在子组件标签上通过**属性值**方式传值

```html
<子组件标签 name=value name=value name=value></子组件标签>
```

子组件接收并应用值，具体通过props接收

```html
<!--在模板中应用传递来的数据-->
<input :style="{color:xx}">

<script>
  export default {
    // 通过props接收父传递过来的数据,注意各个名称需要使用单引号圈选
    props:['xx','xx','xx']
  }
</script>
```



### 扩展

`this指向`：

1. **Vue实例内部**指向 new  Vue()
2. **组件内部**指向**组件实例(VueComponent)**，同时该VueComponent有**继承Vue**，因此组件内部使用this与Vue实例的用法完全一致，即组件内部this可以正常访问**自己**的data、methods、computed等成员



#### render方法扩展使用

具体如下：

```js
new Vue({
  render:h=>h('p','ok')  // 要生成 <p>ok</p> 并覆盖渲染 div容器
  render:h=>h(组件模块) // 要使用一个组件模块 对 div容器 进行覆盖渲染
})
```



`说明`：

​	真实项目中一般喜欢创建一个名称为App.vue的组件，并用它去渲染覆盖 div容器

​	所有业务逻辑实现都从App.vue开始，div容器 就是一个空壳摆设



通过render对App.vue组件覆盖渲染应用,所有业务通过App.vue展开：

1. 在main.js文件中，要使用默认的vue    **import  Vue  from 'vue'**
2. 所有业务组件都通过App.vue文件做应用( 组件的引入、注册、使用)



## SPA

`什么是`：

概念定义：SPA英文全称是Single Page Application, 中文翻译是 “单页面应用程序项目”

通俗的理解是：一个网站只有一个Web页面；网站的所有功能都在这个唯一的页面上进行展示与使用

`好处`：

1. 实现了前后端**分离模式**(目前最好的开发模式)开发，各司其职；提高了开发效率；
2. 用户体验好，页面部分内容发生变化只需要更新局部即可(非刷新整个页面)；

`缺点`：

1. 对SEO(搜索引擎)不是很友好，网站从开始到结束始终访问一个程序文件，造成搜索引擎不给检索， 但是有解决方案，再者后台系统应用本身对seo不做要求
2. 每次应用运行时，需要一次性把全部的html、js、css等内容加载进来，因此会造成页面一开始请求速度较慢的问题(首页较慢，后续页面正常)



`spa应用场合`：

后台管理系统 和 移动端项目，它们特点是供访问的页面总数量小于500个



3. 在 src/App.vue 中设置如下内容


```
1. 在App.vue中设置component标签，代表各个业务组件要在此显示，component可以理解为是“占位符”
    <component :is=" 组件名字  "></component>   // 设置显示各个子组件
```

    > is属性要接收一个具体组件名称，控制显示组件
    > is属性本身需要冒号属性绑定方式设置

2. window.onhashchange事件，可以感知#锚点发生变化
3. window.location.hash 获得浏览器当前变化后的锚点数据



`注意`：

1. 在main.js文件中直接引入使用vue   **import Vue from 'vue'**

2. App.vue中设置window.onhashchange=**箭头函数**，箭头函数使得内部this与外部保持一致，都是组件实例

3. 属性绑定说明

   ```html
   {{js表达式}}
   <div :id=" js的表达式  ">
   
   <div id=" 14 ">  // id接收14是字符串信息
   <div :id=" 14 ">  // id接收14是数值型信息
   <div :id=" '14' ">  // id接收14是字符串信息
   
   <script>
     var age = 14
     var score = '100'
     var xx = js表达式
   </script>
     
   <div id="apple">  apple是字符串
   <div :id="   apple   ">  apple代表的是实例内部data成员名称
   <div :id="  'apple'  ">  apple是普通字符串
   ```



## 路由

`什么是`：

答：路由是一个js功能模块，用于解决做个组件切换显示问题的，本身对**组件切换**的各个底层技术有做**封装**，是更成熟组件切换解决方案，使用起来更高级、方便。

路由封装元素有：\#锚点超链接、component占位符标签、window.onhashchange、window.location.hash等等

路由：通俗讲 就是#锚点 与 被显示组件 的对应关系，内部有若干执行环节



执行指令单独安装：

```bash
yarn  add vue-router
```

​	以上安装依赖包的指令需要在项目根目录(src目录并列的位置)执行



> 依赖包：通过npm i  或 yarn  add 装的东西就是依赖包，每个依赖包内部有**多个**功能模块
>
> 模块：一个js文件内部有做"模块化导出"动作，这个js文件就是一个(功能)模块
>



#### 设置切换按钮和占位符

> 路由中通过router-link设置  按钮和#锚点信息

占位符：

```html
<router-view></router-view>
```

> 路由中通过 router-view 设置组件显示占位符



#### 执行过程分析

路由执行过程：

- 用户点击 页面的 路由链接router-link，点击的一瞬间，就会修改 浏览器 地址栏 中的 #号 锚点地址信息，
- \#锚点变化了 会立即被  路由 监听到   (路由有封装onhashchange事件)
- 之后 路由 会获取变化后的#锚点信息  (路由有封装window.location.hash)
- 再之后 路由 根据#锚点信息找到对应 的组件 (在main.js中可知)
- 最后组件是通过路由占位符rouer-view显示的



#### 重定向

`什么是`：

用户第一次访问网站页面("/根目录"首页)时，地址栏里边没有“#锚点”的信息，
也就没有对应的组件用于显示，明显项目体验不好，现在可以通过<font color=red>redirect</font>实现一种效果，即当浏览器没有任何 #锚点信息时，我们默认也给显示一个组件

重定向：使得一个路由地址A与另一个路由地址B联系起来，执行A的时候会跳转执行B

`语法`：

```js
var router = new VueRouter({
  routes:[
    // {path:'/', redirect:'跳转到的路由锚点信息'}
    {path:'/', redirect:'/hm'},
    {path:'/hm', component:Home},
    ……
  ]
})
```

> 执行路由地址/根目录时，就跳转执行路由地址/hm，进而把对应的组件给显示出来了

1. 不仅 "/" 可以被重定向配置，其他的普通路由锚点信息也可以设置
2. 重定向会使得路由再次发生调用请求



#### 按钮高亮设置

> 通过观察，发现按钮被访问激活后，其对应的html标签就会存在  class="router-link-active" 的属性值

​	通过观察，被激活的按钮的class属性值里边还有一个值为  router-link-exact-active  的信息，不要使用，其表达的意思是，只有路由**严格匹配**的时候才会出现这个信息，**模糊匹配**时候该信息就没有了，造成高亮失效，在后边学习子路由会有体现



### 子路由

一般项目开发中，App.vue是根基组件(第1级别的)，内部可以有具体业务组件(Home.vue  Movie.vue  Music.vue，它们是第2级别的)，根据业务需要，业务组件内部还要做内容**分级**显示，这样就形成第3级别的业务组件，第3级别组件(香港音乐/台湾音乐/大陆音乐)的路由 是 第2级别组件路由 的**子路由**

第3级别组件做应用的时候需要设置路由，并且与第2级别组件路由有形成父子关系，故称为  子路由

> Music 和 children 内部都可以设置重定向，两种方式

`注意`：

1. 子路由设置**重定向**有两种方式：父路由中 或 子路由中
2. 父级路由的component不能去除



### 路由传参

商品列表页面中，每个商品项目都有 `详情`等按钮，单击`详情`按钮查看当前商品时，就需要在url请求地址中把当前商品的id带着(例如： http://www.xxx.com/detail.html?gid=670)，以便据此查询商品的详细信息，商品id本身就是一个参数，spa项目应用中根据业务需求也要传递参数，这可以利用**路由传参**实现

`接收路由参数`：

```html
<标签>{{$route.params.xxx}}</标签>

<script>
new Vue({
	this.$route.params.xxx
})
</script>
```

> 模板 和 Vue实例 内部都可以接收

1. 路由有参数，那么应用中要**传递**该参数
2. router-link标签默认被编译为超链接a标签，可以设置**tag属性**，使其变为其他标签



### 编程式导航

`导航`：

​	一个路由被执行的过程就是一次导航

`导航种类`：

1. 声明式导航：router-link可以编译生成超链接按钮，单击按钮就切换路由并显示对应的组件，这个过程称为“声明式导航”
2. 编程式导航：有时由于业务需要，一个路由被切换执行并不方便通过**声明式导航**实现，相反是要通过**程序代码**的方式给实现出来，就是“编程式导航”

`编程式导航的实现`：

```js
路由对象.push(锚点信息)   // 根据锚点执行指定的路由  最经常使用
路由对象.back()  				// 后退
路由对象.forward()  		// 前进
路由对象.go(数字整数)    // 根据“整型数字”参数做路由的 前进(大于0)、刷新(等于0)、后退(小于0) 操作
```



### 守卫

​	每个路由在执行的时候都会经历一些"**关卡**"，关卡可以做决定是否 继续前进 或 执行其他路由 或 停止当前路由执行 ，关卡就是守卫，守卫有着一夫当关万夫莫开的作用

`为什么使用`：

​	每个项目都要使用守卫，例如后台管理系统，很多组件页面要求只有处于登录状态的用户才可以访问，判断是否登录就是通过守卫做的。

#### 简单使用

`语法`：

```js
router.beforeEach((to, from, next) => { /* 导航守卫 处理逻辑 */ })
```

> router是 new VueRouter() 得到的 路由对象

- to:是一个对象，保存着将要访问的路由相关参数

- from:是一个对象，保存着离开的那个路由的相关参数

- next:是一个回调函数，对后续的执行起着 拦截 或 放行 的作用

  如果没有问题请<font color=red>一定执行next()</font>方法，以进行后续操作，

  next()方法也可以通过传递路由信息实现其他组件的显示

  例如：next('/login')   显示登录组件

  ​            next(false)  停止当前路由执行

在main.js的**new VueRouter()代码之后**设置如下代码，查看执行效果

`注意`：

 “**全局前置守卫**” ，特点是所有的路由在执行之前会经过该守卫



## WebStorage

`cookie缺陷`：

1. 大小受限，单个项目有**4k**限制
2. 用户可以操作（禁用）cookie，使功能受限
3. 每次请求时，cookie都会存放在请求头中，请求被拦截，cookie数据会存在安全隐患

`WebStorage特点`：

1. 存储空间更大，单个项目 Chrome，Firefox和Opera 数据大小可以达到 **5MB**， IE是10M 
2. 只能存储**字符串**类型
3. 不能被爬虫抓取到，更安全 



WebStorage的使用具体分为两种：localStorage 和 sessionStorage

- localStorage（持久存储），关闭浏览器之后localStorage中的数据也不会消失。除非主动删除数据，否则数据永远存在
- sessionStorage（会话存储），临时存储，数据只在当前会话下是有效的，只要这个 浏览器/标签窗口 没有关闭，即使刷新页面或者进入同源另一个页面，数据依然存在，关闭了 浏览器/标签窗口 后数据就被被销毁

`应用场景`：

localStorage：用于长期登录（+判断用户是否已登录），适合长期保存在本地的数据。

sessionStorage：敏感账号一次性登录



# ESLint

- 声明变量但是**未使用**会报错
- 简单语句结尾不能有**分号**
- 给变量赋值 **等号** 左右要求有空格
- 在行结尾处，**多余**的空格不允许
- 字符串必须使用**单引号**圈选，不能是双引号
- 对象 成员名称**冒号** 与 值 之间需要有一个空格
- 方法名称小括号 的**左右**需要保留一个空格
- 在每一个文件的结尾处，必须有一个空行
- 文件中如果出现空白行，要求只能有一行空白，不能连续出现两行或以上的空白行

2. eslint只是针对 **js文件** 和 **vue文件的js部分** 做规范检查



## 自定义规则配置

根据自己的想法给eslint配置规范，修改配置文件.eslintrc.js，给其中的rules段做配置即可

```js
// 匹配规则:[开启规则参数，要求/禁用参数]
'semi':['error','always'],  // 简单语句后边要求设置分号，不设置会报错
'semi':['error','never'],  // 简单语句后边不要设置分号，设置会报错
'semi':['off','always'],  // 关闭规则检测
'semi':['off','never'],  // 关闭规则检测
  
'space-before-function-paren': ['error', 'never'],  // 禁止在function小括号左边设置空格，否则报错
'space-before-function-paren': ['error', 'always'], // 要求在function小括号左边设置空格，否则报错
'space-before-function-paren': ['off', 'always'], // 关闭规则
'space-before-function-paren': ['off', 'never'], // 关闭规则
  
'no-multiple-empty-lines': ['error', { 'max': 3 }], // 文件中间允许出现3个或以内的空白行
'no-multiple-empty-lines': ['off', { 'max': 3 }], // 关闭规则
```

> 开启规则参数：
>
> ​	error：将规则视为一个错误
>
> ​	off：关闭规则
>
> 要求/禁用参数：
>
> ​	always：要求规则
>
> ​	never：禁止规则



## 代码自动规范

2. 全局方式安装eslint依赖包

   ```
   npm install -g eslint
   ```

   > 该依赖包安装完毕是对1步骤扩展做支撑的
   >
   > 注意：通过npm方式安装

3. 打开vscode配置文件 settings.json  (by File-> Preferences->Settings)

   在最末尾如下内容

   ```javascript
   "eslint.enable": true,
   "eslint.autoFixOnSave": true,
   "eslint.run": "onType",
   "eslint.options": {
       "extensions": [".js",".vue"]
   },
   "eslint.validate": [
       { "language": "html", "autoFix": true },
       { "language": "javascript", "autoFix": true },
       { "language": "vue", "autoFix": true }
   ]
   ```




# ElementUI

`ElementUI官网`：

 https://element.eleme.cn/#/zh-CN 

## 安装

```
yarn add element-ui
```

1. 在main.js文件中引入elementui模块和注册

   ```js
   // eslint要求import系列代码都要在普通代码上边设置
   // 引入elementui组件库
   import ElementUI from 'element-ui'
   // 引入css样式
   import 'element-ui/lib/theme-chalk/index.css'
   // 把组件库注册给Vue
   // 之前组件注册：Vue.component(名称,组件) 每次只能注册一个
   // 现在组件注册: Vue.use(组件模块) 一次性注册"全部"的组件，非常高效
   Vue.use(ElementUI)
   ```

   element组件库提供内容由两种：组件、事件方法


`注意`：

1. 我们要在src目录下编辑项目代码，这是项目的源代码，完毕后还要做**打包**上线处理
2. src目录下的代码不能部署，相反是打包后的代码文件可以部署（npm run build）



## 完整引入使用

`什么是完整引入`：

​	在项目入口文件main.js中一次性把ElementUI组件库全部的**组件**和**方法**做引入部署

```js
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI);
```



## 按需引入使用

`什么是`：

​	Element-UI本身有非常多的`组件`、`css样式`、`方法`，在一个项目中有可能不会用到全部，如果全部引入，不用的元素会造成额外资源开销，进而影响项目性能。采取的措施就是用多少就引多少，即按需引入

`步骤`：

1. 安装依赖包

   ```
   yarn add babel-plugin-component -D
   ```

2. 在babel.config.js文件中做如下配置

   ```js
   module.exports = {
     plugins: [
       [
         'component',
         {
           'libraryName': 'element-ui',
           'styleLibraryName': 'theme-chalk'
         }
       ]
     ]
   }
   ```

以上两个步骤完成后，**css样式** 已经可以实现**按需引入**了(main.js中关于elementui的css样式引入已经不起作用了，鉴于代码美观可以删除 或 屏蔽   // import 'element-ui/lib/theme-chalk/index.css')



3. 在main.js文件中给 **组件** 和 **事件方法** 做按需引入

   ```js
   // 2) 按需引入
   import { Row, Button, MessageBox, Message } from 'element-ui'
   // 按需注册组件
   Vue.use(Row)
   Vue.use(Button)
   // 按需注册事件方法(原型继承)
   Vue.prototype.$confirm = MessageBox.confirm
   Vue.prototype.$message = Message
   ```

   > 以上配置完毕，请重启服务 npm run serve



可以借鉴按需导入的全部组件和事件方法： https://element.eleme.cn/#/zh-CN/component/quickstart 



2. 按需引入根据内容可以分为：css样式、组件、事件方法 3种
3. 为了方便开发，前期只做**css样式**按需引入，待项目开发完毕后，再给**组件**和**事件方法** 做统计按需引入



# 插槽

要传递的数据非常多，例如**一大段html标签**内容，则不合适，这时可以通过   **插槽**  实现	

​	父子组件嵌套情形，子组件给自己**个性化区域**设置一个占位符，父组件给占位符填充内容，占位符就是 **插槽**



## 简单应用(匿名)

匿名插槽定义语法：

```html
<slot></slot>
```

> 在一个子组件中，允许出现多个匿名插槽，它们都会接收相同内容，但一般没有实际意义

给插槽传递数据：

```html
<子组件标签> 被填充到插槽的内容 </子组件标签>
```

`步骤`：

1. 在components目录里边创建组件Button.vue，内容如下，其中有slot插槽体现

   ```html
   <template>
       <div>
         <button>
           <!--设置插槽(占位符),父组件对该插槽进行内容填充，进而显示不同的按钮文字-->
           <slot></slot>
         </button>
       </div>
   </template>
   ```

2. 在App.vue实现如下代码，给子组件标签**内容区域**设置信息，其会被传递给插槽

   ```html
   <template>
       <div>
         <h2>App根组件</h2>
         <!--使用子组件-->
         <my-button><a href="#">确定</a></my-button>
         <my-button><i>取消</i></my-button>
         <my-button>重置</my-button>
       </div>
   </template>
   
   <script>
   // 引入Button.vue组件
   import Button from '@/components/Button.vue'
   export default {
     // 注册Button组件
     components: { 'my-button': Button }
   }
   </script>
   ```



`注意`：

1.  vue文件编译运行后**slot标签**会被父组件传递的信息覆盖掉，即使没有接受到信息本身也不在浏览器体现
2.  一个组件根据需要可以声明多个匿名slot，每个slot会分别**独立接收**到相同的内容，匿名插槽在一个组件中通常只会出现**一个**
3.  父组件给插槽传递的信息可以是     **html标签** 或 **字符串** 或 **组件** 等内容，并且数量没有限制
4.  子组件标签**内容区域信息**必须与slot联系，如果子组件内部没有slot，那么这个信息会丢失



## 命名插槽

子组件根据需要，内部可能有多个**个性化区域**，这样就需要定义多个slot，为了加以区分，可以给slot定义名字

`命名插槽`：

```html
<slot name="s1"></slot>
<slot name="s2"></slot>
<slot name="s3"></slot>
```

> 通过name属性给插槽定义名字

父组件根据名字给插槽填充内容

```html
<子组件>
  <div slot="s1">填充给name="s1"的插槽中</div>
  <div slot="s2">填充给name="s2"的插槽中</div>
  <p>填充给匿名插槽</p>
  <div slot="s3">填充给name="s3"的插槽中</div>
  <p>填充给匿名插槽</p>
<子组件>
```



## 命名插槽应用

`步骤`：

1. 创建Page.vue组件并声明slot命名插槽

   ```vue
   <template>
       <div>
         <ul>
           <li><slot name="one"></slot></li>
           <li>1</li>
           <li>2</li>
           <li><slot name="two"></slot></li>
         </ul>
       </div>
   </template>
   ```
   
2. App.vue  导入、注册、使用 Page.vue并传递信息

   ```vue
   <template>
       <div>
         <h2>App根组件</h2>
         <!--使用子组件-->
      		<my-button><a href="#">确定</a></my-button>
         <my-button><i>取消</i></my-button>
         <my-button>重置</my-button>
         <page>
           <a href="#" slot="one">上一页</a>
           <a href="#" slot="two">下一页</a>
         </page>
       </div>
   </template>
   
   <script>
   // 引入Button.vue组件
   import Button from '@/views/Button.vue'
   import Page from '@/views/Page.vue'
   export default {
     // 注册Button组件
     components: { 
       'my-button': Button,
       Page
     }
   }
   </script>
   ```



`注意`：

1. 命名插槽  和 匿名插槽 可以**同时**存在，它们会分别接受自己的信息
2. 给 命名插槽 填充信息必须要通过  "**html标签**" 圈选，以便设置slot=xx的属性
3. 针对同一个命名插槽，可以接收**多个**不同的内容



## 作用域插槽(难点)

​	插槽应用中，父组件给插槽填充的内容通常有两部分：**html标签**、**数据**部分

​	实际情况是：父组件只传递html标签，数据信息要通过slot自己传递，

​	父组件关注外在表现，子组件插槽关注核心数据

​	子组件给插槽定义要使用的数据，这个数据只是自己应用区域可见 故称为   **作用域插槽**

`语法`：

1. 插槽给自己声明数据：

   ```html
   <slot xx=xx yy=yy zz=zz></slot>
   ```

   > 通过"属性值"方式定义数据

   

2. 父组件应用插槽数据

   ```html
   <子组件>
     <html标签 slot-scope="名称">
       {{ 名称.xx }}
       {{ 名称.yy }}
       {{ 名称.zz }}
     </html标签>
   </子组件>
   ```

   

`插槽数据声明注意`：

1. 通过  **属性值**  方式声明数据，数量不限制，名称不能是name(其为命名插槽固定属性)
2. 匿名、命名插槽 都可以声明数据，实现 作用域插槽 效果
3. 插槽数据来源可以是 **直接声明** 的，也可以进行 **属性绑定** 获取本身组件实例的信息
4. 声明数据的类型不限制(例如String、Number、Boolean、Object、Array 都可以)



`插槽数据使用注意`：

1. 在html标签中声明属性值  **slot-scope=名称**   接收插槽声明的数据，**名称**是一个对象，成员就是插槽的属性名
2. 接收的信息如果是数组，可以通过v-for遍历
3. slot-scope  与 v-for  不能出现在同一个html标签中，确有需要，可以让它们出现在父子标签里边



## 作用域插槽案例

`步骤`：

1. 创建名称为Page2.vue的组件，给两个slot声明要使用的数据

   ```html
   <template>
       <div>
         <!--分页组件-->
         <ul>
           <!--两个命名插槽-->
           <!--作用域插槽：声明自己要使用的数据-->
           <!--  通过"属性值"方式设置即可 -->
           <slot name="shang" prev="上页"></slot>
           <li>1</li>
           <li>2</li>
           <slot name="xia" next="下页"></slot>
         </ul>
       </div>
   </template>
   ```
   

   
2. App.vue 导入、注册、使用  PageOne.vue 组件，接收、使用插槽的数据

   ```html
   <template>
       <div>
         <h2>App根组件(作用域插槽)</h2>
         <com-page>
           <!--获得插槽定义的数据信息-->
           <!--标签需要使用一个名称为"slot-scope"的属性接收信息-->
           <!--例如slot-scope="stData"-->
           <!--stData:是一个对象(自定义名称)，具体可以访问到插槽的属性名称，例如prev-->
   
           <li slot="shang" slot-scope="stData">{{ stData.prev }} </li>
           <li slot="xia" slot-scope="stData">{{stData.next}}</li>
   
         </com-page>
       </div>
   </template>
   
   <script>
   // 针对其他组件做：导入、注册、使用
   import ComPage from './components/Page'
   export default {
     components: {
       ComPage
     }
   }
   </script>
   ```



`注意`：

1. 自己slot插槽定义的数据，只能是自己的slot-scope接收使用



# 起步

2. import有两种使用方法
   1. import xx from ''   模块化导入
   2. import()  函数调用 ，引入一个文件进来



## 项目-git初始化

1. 在本地项目中给远程仓库连接地址设置“别名”

   ```
   git remote add top87 https://gitee.com/sunshuhua/topline87.git
   ```

3. 把当前初始化好的项目文件的master分支做push，推送给远程仓库

   ```
   git push top86 master
   ```

4. 现在给git创建login分支并切换过来

   ```
   git checkout -b login  // git branch  login   &  git checkout login
   ```



# 登录

## 初始化login组件文件

`步骤`：

1. 创建views/login/index.vue 组件文件，内容简单设置

2. 给login创建路由，src/router/index.js

   ```js
   // 当前项目内部已经对 index.vue和 index.js文件做了默认的索引寻找配置，
   // 如果一个目录名字没有明确设置要找到的文件，那么优先寻找index.vue或index.js
   // 故login目录下边的index.vue 处于代码优雅考虑 可以 不设置
   
     // @别名：代表src目录的绝对路径名地址(vuecli准备好的)
     // E:\Vue86-87\87\87everyday\02daypro\topline87\src\
     // index.vue文件是默认索引文件，不用设置，自动寻找
   { path: '/login', name: 'login', component: () => import('@/views/login') }
   ```

   

3. 启动服务 npm run serve

4. 浏览器输入  http://127.0.0.1:12306/#/login  已经可以访问登录组件效果了

`注意`：

   @ 是系统给封装好的别名，代表src目录的"绝对路径名"信息

   @：E:\Vue86-87\86\86everyday\02daypro\topline\src\

## 给login组件绘制登录盒子

`步骤`：

1. 创建src/assets/css/global.css文件

   ```css
   html,body,#app{
     height:100%;
     margin:0;
     padding:0;
   }
   ```

2. 在main.js中引入global.css文件

   ```js
   // 导入全局样式文件
   import '@/assets/css/global.css'
   ```

   

3. 在login/index.vue文件中通过html标签 和 css样式实现登录盒子效果

   

`注意`：

1. VueCli框架已经给src文件夹的**绝对路径名**信息定义为<font color=red>@符号</font>的别名了，可以直接使用

2. 定义 **全局样式文件(src/assets/css/global.css)** 给父级 App.vue 和 index.html 文件**统一**做样式控制



## 安装配置ElementUI组件库

`步骤`：

1. 安装组件库依赖包  yarn  add  element-ui

2. 安装按需引入依赖包  yarn  add   babel-plugin-component -D

3. 在babel.config.js中做css样式按需引入配置，设置plugins段

   ```js
   module.exports = {
     plugins: [
       [
         'component',
         {
           'libraryName': 'element-ui',
           'styleLibraryName': 'theme-chalk'
         }
       ]
     ]
   }
   ```

399. 在main.js中引入、注册组件库模块

     ```js
     // 引入组件库模块
     import ElementUI from 'element-ui'
     // 注册
     Vue.use(ElementUI)
     ```


`注意`：

​	eslint要求，一个文件中的所有导入**import语句**必须在其他语句**之前**配置(自动代码规范 会配置)



## form表单组件介绍

```html
<el-form ref="form" :model="form" label-width="80px">
ref: 使得可以获取当前的组件对象  this.$refs.form，后期表单校验会使用
:model="form"  属性绑定model，与v-model没有关系，作用是要收集表单的全部数据，后期表单校验会使用
label-width：设置表单域项目名字区域宽度

  <el-form-item label="活动名称">
    每个表单域项目的单元组成
    label设置当前表单项目的名字
    
    <el-input v-model="form.name"></el-input>
    具体输入框表单域项目
    v-model:双向数据绑定，具体帮到到form对象的name成员里边
```

> \<div/组件 ref="xx" id="yy"\>
>
> 获得div的dom对象： document.getElementById('yy')
> vue方式获取dom对象： this.$refs.xx
>
> 以上两者获得div对象完全一样(都是dom对象)
>
> 如果div是一个组件，那么this.$refs.xx 就会把该组件对象VueComponent给获得到
>
> div元素对象获取：两种方式，如上提示
>
> 组件对象获取：一种方式，如上提示



`注意`：

1. 以上各个属性  ref、model、v-model是必须的  label-width 和 label是非必须的

2. ref：属性是方便后期通过vue的方式获得当前的组件，必须属性

3. model：属性是要收集全部的表单信息以便后期校验等使用，必须属性

4. label-width：给表单域名字区域设置宽度

   > 以后每个el-form使用的时候都要设置ref 和 model属性



## el-form表单组件绘制登录表单域

`说明`：

1. 表单域项目具体有   **手机号码** 、 **校验码**、**协议**、**登录按钮** 
2. el-form的label-width属性要去除，el-form-item的label属性去除
3. elementui每个组件   都需要被编译为具体的html标签代码，html标签会同时生成class属性，**属性值就会包含当前组件标签的名字**，因此可以通过组件名称以class的方式进行css样式控制

```
<el-form>      -----编译---->  <form class="el-form">
```

`注意`：

​	elementui组件库初次使用没有css样式效果，请重启服务npm run serve




## 进入后台首页

`步骤`：

1. 创建后台首页组件文件  views/home/index.vue

2. 给home设置路由( src/router/index.js )

   ```js
   { path: '/home', name: 'home', component: () => import('@/views/home') }
   ```
   

   
3. 给“登录”按钮设置单击事件@click="login()"，使得路由跳转

   ```html
   <el-button style="width:100%;" type="primary" @click="login()">登录</el-button>
   ```
   
4. 在methods中实现login方法

   ```js
     methods: {
       login () {
         // this.$router.push('/home')
         this.$router.push({name:'home'})
       }
     }
   ```

## 表单校验(自然方式)

`步骤`:

1. 给el-form设置rules属性

   ```html
   <el-form :rules="loginFormRules">
   ```

2. 给各个被校验项目的el-form-item组件设置prop属性，属性值就是表单对象的成员名称(不要定义为其他)

   ```html
   <el-form-item prop="mobile">
   <el-form-item prop="code">
   ```

   > prop会使得校验规则 与 当前项目联系

3. 在data中定义具体校验规则

   ```js
   // 给form表单域制作校验规则
     data () {
       return {
         loginFormRules: {
           mobile: [
             { required: true, message: '手机号码必填' },
             { pattern: /^1[35789]\d{9}$/, message: '手机号码格式不对' }
           ],
           code: [
             { required: true, message: '验证码必填' }
           ]
         }
       }
     }
   ```


`注意`：

1. 每个表单域项目根据需要可以配置**多个**校验项目
2. elementui内部有引入第三方功能包实现校验，名称为[async-validator](https://github.com/yiminghe/async-validator)  可以参考使用
3. required只校验 null   undefined 和空字符串 ,但是不校验false/true



| 规则         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| type(可不填) | 指定要检验的字段的类型                                       |
| required     | 必填项,如果不填 就无法通过校验/如果为true,就表示该字段必填   |
| validator    | **`自定义校验函数`**                                         |
| message      | 当不满足设置的规则时的提示信息                               |
| pattern      | 正则表达式                                                   |
| range        | 使用min和max属性定义范围。对于字符串和数组类型，将根据长度进行比较，对于数字类型，数字不得小于min，也不得大于max。 |
| len          | 要验证字段的确切长度，请指定len属性。对于字符串和数组类型，对length属性执行比较，对于数字类型，此属性指示数字的完全匹配，即，它可能仅严格等于len。如果len属性与最小和最大范围属性组合，则len优先。 |
| enum         | 要从可能值列表中验证值，请使用带枚举属性的枚举类型，列出该字段的有效值，例如： var descriptor = {   role: {type: "enum", enum: ['admin', 'user', 'guest']} |



## 表单校验(登录方式)

给methods的login方法增加校验逻辑

```js
  methods: {
    // 登录系统
    login () {
      // 全部表单域项目校验
      // 获得form表单组件的语句: this.$refs.loginFormRef
      // form组件.validate(回调函数)
      // 参数valid：会体现布尔值，表示校验是否成功
      this.$refs.loginFormRef.validate((valid) => {
        if (valid) {
          this.$router.push({ name: 'home' })
        }
      })

      // this.$router.push('/home')
      // this.$router.push({ name: 'home' })
    }
  }
```

`说明`：

1. el-form组件内部有属性值 ref="loginFormRef"，Vue允许通过 this.$refs.loginFormRef的方式获得该组件对象
2. el-form组件本身可以调用validate方法，实现对**全部**表单域项目做校验
3. validate内部有**回调函数**参数，该函数内部还有valid参数，valid会返回布尔值，进而知道校验是否成功
4. validate内部的回调函数要设置为  “箭头函数”，使得内部this与外部保持一致指引，都是组件实例
5. form表单全部做校验还与el-form 的**model属性**有关系，其会获取全部的表单信息，提供校验使用



## 表单校验(自定义-协议)

`步骤`：

1. 设置prop属性

   给xieyi  的项目设置prop属性

   ```html
   <el-form-item prop="xieyi">
   ```

   

2. 声明校验的function方法

   在data中为xieyi校验声明方法

   ```js
     data () {
       // 自定义校验函数，验证协议
       var xieyiTest = function (rule, value, callback) {
         // rule:校验规则，一般不用
         // value:当前被校验的信息
         // callback：回调函数，校验成功或失败都需要执行
         // if (value) {
         //   callback()
         // } else {
         //   return callback(new Error('请无条件遵守规矩'))
         // }
         value ? callback() : callback(new Error('请无条件遵守规矩'))
       }
     }
   ```
   
> 注意：校验方法需要在return语句的“前边”设置

3. 通过validator使用该自定义校验方法

   ```js
   loginFormRules: {
     ……
     xieyi: [
       { validator: xieyiTest }
     ]
   }
   ```



`说明`：

1. 协议  项目没有提供校验机制(required不能校验true/false的信息)，故要自定义
2. 校验协议信息的 xieyiTest 方法需要定义到data方法中，注意不是**return内部**
3. 校验规则要使用 validator 关联 xieyiTest函数



## 安装配置axios

`步骤`：

1. 安装axios：  yarn  add  axios

2. 在main.js主入口文件中引入配置axios

   ```js
   import axios  from  'axios'
   // 配置后端服务器接口公共根地址
   axios.defaults.baseURL = 'http://ttapi.research.itcast.cn/mp/v1_0/'  
   Vue.prototype.$http = axios  
   ```

`说明`：

根据ElementUI事件方法注册机制，给axios做如下配置

`Vue.prototype.$http = axios`   axios通过继承方式配置为Vue的成员，这样所有通过Vue实例出来的对象就都可以访问，形式为this.\$http

单文件组件VueComponent也有继承Vue，因此组件实例都可以通过 this.\$http 的方式访问axios对象



## 注册账号

地址为http://ttmp.research.itcast.cn/的参考项目如果需要一个的账号，

要通过postman向http://ttapi.research.itcast.cn/app/v1_0/authorizations 发送post请求并传递数据实现

`步骤`：

1. 请求方式为post

2. 请求体为Body，二级选项为raw 和 JSON(application/json)

   请求体：

   ```json
   {
     "mobile": "你的手机号",
     "code": "246810"
   }
   ```

   > code固定为246810不要更改

3. 请求数据为下图json格式

![1563865009333](Image/img(online)/1563865009333.png)



## 校验账号

用户登录系统，表单域校验成功后，要通过axios校验账号的真实性，成功再进入后台系统

```js
methods: {
  login () {
    this.$refs.loginFormRef.validate(valid => {
      // 表单域校验成功
      if (valid) {
        // 账号真实性校验
        var pro = this.$http.post('/authorizations', this.loginForm)
        pro
          .then(result => {
            if (result.data.message === 'OK') {
              // 进入后台系统
              this.$router.push('/home')
            }
          })
          .catch(err => {
            return this.$message.error('用户名或密码错误' + err)
          })
      }
    })
  }
}
```

`说明`：

```js
// elementui组件库事件方法$message使用有两种格式
1. this.$message({type:'error', message:'用户名或密码错误'})
2. this.$message.error('用户名或密码错误')
设置停留时间：
this.$message({type:'error', message:'用户名或密码错误',duration:1000})
```

## 客户端记录账号信息

管理员登录系统成功，通过sessionStorage对各个信息(id/name/photo/token)做记录，用以表示当前用户处于登录状态

```js
  methods: {
    login () {
      this.$refs.loginFormRef.validate(valid => {
        if (!valid) {
          return false
        }
        var pro = this.$http.post('/authorizations', this.loginForm)
        pro
          .then(result => {
            if (result.data.message === 'OK') {
              // 客户端记录用户的信息
              window.sessionStorage.setItem('userinfo', JSON.stringify(result.data.data))
              this.$router.push('/home')
            }
          })
          .catch(err => {
            return this.$message.error('用户名或密码错误' + err)
          })
      })
    }
  }
```

`说明`：

1. 服务器端返回的账号数据信息是一个**对象**，内部有 id/name/photo/token等，webstorage不能存储对象，故要通过  **JSON.stringify()**  进行转换变为字符串，相反信息做应用时还要通过  **JSON.parse()**  再转回为对象
2. 一般客户端只存储用户token信息即可(表明是否处于的登录状态)，存储其他信息是为了其他用途
3. 如果有其他考虑，使用localStorage存储用户信息也可以



## 非登录用户限制访问

在src/router/index.js中做守卫设置，代码如下：

```js
// 设置 全局前置守卫
router.beforeEach((to, from, next) => {
  // 用户如果是"非登录"状态，并且其还要访问 非登录 页面，那么就强制登录去
  var userinfo = window.sessionStorage.getItem('userinfo')
  if (!userinfo && to.path !== '/login') {
    // 路由导航到登录页面
    return next('/login') // ok
  }
  next()
})
```

`注意`：

1. 如果用户已经退出系统，或由于其他原因导致客户端数据丢失，则userinfo的信息为**null**
2. 如果其他应用要用**userinfo**用户信息，其是字符串类型，需要通过**JSON.parse()**转换后才可以使用



## 极验

### 人机交互验证介绍

极验是一款人机交互页面效果系统，用户的**行为**没有满足要求，不给与下一步执行的机会

之前传统网站，用户输入 **用户名**、**密码**、**验证码**  就可以登录系统了

这样的网站不安全，有网络**爬虫**技术，可以通过“后端程序代码” **模拟账号**登录，进而获得我们网站的信息

现在比较先进的网站，都使用“**人机交互验证**”功能，对登录者提出高要求，不让模拟登录得逞，相反只允许“实在的人”来登录系统并应用

极验官网：<https://www.geetest.com/>



### 流程分析

开发人机验证步骤：

1. axios向本身后端服务器发起请求，后端服务器会返回极验请求的秘钥信息
2. **极验秘钥信息** + **用户行为** 一并提交给 极验服务器 做判断，查验行为是否正确



### 获取极验秘钥信息

`步骤`：

1. 把 账号真实校验 和 登录系统 逻辑代码封装为独立的loginAct方法，方便开发
2. axios根据接口发送请求，获得极验请求秘钥信息



login/index.vue相关代码结构：

```js
  methods: {
    login () {
      this.$refs.loginFormRef.validate(valid => {
        // 表单域校验成功
        if (valid) {
          // A. axios获得极验请求秘钥信息
          let pro = this.$http.get(`/captchas/${this.loginForm.mobile}`)
          pro
            .then(result => {
              // 服务器端返回极验的请求秘钥信息
              console.log(result) // config 【data】 request  headers status statusText
            })
            .catch(err => {
              return this.$message.error('获得极验初始校验信息错误：' + err)
            })

          // B. 账号真实校验，登录后台
          // this.loginAct()
        }
      })
    },
    // 校验账号真实性，登录后台
    loginAct () {
      // 账号真实性校验
      var pro = this.$http.post('/authorizations', this.loginForm)
      pro
        .then(result => {
          if (result.data.message === 'OK') {
            // 客户端记录用户的信息
            window.sessionStorage.setItem('userinfo', JSON.stringify(result.data.data))
            // 进入后台系统
            this.$router.push('/home')
          }
        })
        .catch(err => {
          return this.$message.error('用户名或密码错误' + err)
        })
    }
  }
```



### 创建校验窗口并应用

`步骤`：

1. 在login/index.vue中向引入gt.js文件
2. 对返回的极验请求秘钥信息做接收处理(对象解构赋值)
3. 调用initGeetest() 函数，生成极验窗口
   1. 添加product:'bind'
   2. verify()等方法调用

具体代码(login/index.vue)：

```js
// 对gt.js文件进行导入
// gt.js文件本身没有做导出动作，所以就直接导入即可，此时系统增加一个全局变量，名称为 initGeeTest
import '@/assets/js/gt.js'
……
login () {
  this.$refs.loginFormRef.validate(valid => {
    // 表单域校验成功
    if (valid) {
      // A. axios获得极验初始校验信息
      let pro = this.$http.get(`/captchas/${this.loginForm.mobile}`)
      pro
        .then(result => {
          // 接收处理返回的极验请求秘钥信息
          let { data } = result.data
          // 显示极验应用窗口
          // 请检测data的数据结构， 保证data.gt, data.challenge, data.success有值
          window.initGeetest({
            // 以下配置参数来自服务端 SDK
            gt: data.gt,
            challenge: data.challenge,
            offline: !data.success,
            new_captcha: true,
            product: 'bind' // 没有按钮，通过登录按钮激活验证
          }, captchaObj => {
            // 这里可以调用验证实例 captchaObj 的实例方法
            captchaObj.onReady(() => {
              // 验证码ready之后才能调用verify方法显示验证码
              captchaObj.verify() // 显示验证码窗口
            }).onSuccess(() => {
              // your code
              // B. 校验账号真实性，登录
              this.loginAct()
            }).onError(() => {
              // your code
            })
          })
        })
        .catch(err => {
          return this.$message.error('获得极验初始校验信息错误：' + err)
        })
    }
  })
}
```

`注意`：

​	在login方法内部为了使得this仍然指引VueComponent组件实例对象，要把相关的function都变为箭头函数



### 按钮等待和禁用

极验窗口的显示需要消耗一定时间，为了增强用户体验，给“登录”按钮设置“等待”效果，同时考虑到严谨性，要同时设置disabled，使得按钮等待的同时也不让单击

```html
<el-button :loading="ture/false" :disabled="true/false">登录</el-button>
```

> loading: 设置按钮等待效果
>
> disabled:使得按钮禁止单击

`步骤`：

1. data成员设置  isActive:false

   ```js
   isActive: false, // 按钮是否等待、禁用
   ```

2. 给el-button登录按钮应用 loading  和  disabled属性，它们的值通过 btnLoading控制

   ```html
   <el-button 
              style="width:100%;" 
              :loading="isActive" 
              :disabled="isActive" 
              type="primary" 
              @click="login()">登录</el-button>
   ```

   

3. 单击登录按钮后马上禁用 按钮  this.isActive= true

   ```js
   login () {
     this.$refs.loginFormRef.validate(valid => {
       // 表单域校验成功
       if (valid) {
         this.isActive = true // 登录按钮处于等待、禁用状态
   ```

   

4. 极验交互窗口显示完毕 就恢复按钮 this.isActive= false

   ```js
   captchaObj.onReady(() => {
     ……
     this.isActive = false // 恢复按钮
   ```



### 处理重复创建dom问题

每次单击“登录”按钮，那么就给显示“人机交互”页面，本质是许多div  html标签的集合体，如果反复点击“登录”按钮，之前的"窗口"，就隐藏掉(display:none)，再重新生成许多div出来，这个过程不好的地方是，用户都需要等很长时间，并且页面会残留许多无用、过时的dom内容



我们做优化处理：

第一次生成人机窗口后，就给保存起来，后续再发生相同的动作直接使用即可

好处：用户等待时间缩短，页面上也不用生成许多div了

`步骤`：

1. 创建data成员 ctaObj

   ```js
   ctaObj: null, // 极验对象
   ```

2. 第一次生成的人机窗口对象 赋予给 this.ctaObj= captchaObj

   ```js
   captchaObj.onReady(() => {
   	……
     this.ctaObj = captchaObj // 已经极验对象赋予给ctaObj
   ```

   

3. 用户重复单击登录窗口使用缓存好的极验对象

   ```js
   login () {
     this.$refs.loginFormRef.validate(valid => {
       // 表单域校验成功
       if (valid) {
         // 极验对象存在就直接调用
         if (this.ctaObj !== null) {
           return this.ctaObj.verify()
         }
         // 注意：按钮等待 要在 之后设置
         this.isActive = true // 登录按钮处于等待、禁用状态
   ```

`注意`：

登录按钮等待的代码要在之后设置，这样的原因是使用之前的缓存极验对象，由于速度很快，按钮就不要做禁用状态了



## iconfont图标

通过“命名插槽”的方式给 手机和验证码 的输入框前边设置对应的图标

iconfont图标官网： https://www.iconfont.cn/ 

elementui组件库有提供有限的图标供使用，我们可以通过  **阿里巴巴** 网站获取其他的一些图标做应用

`步骤`：

1. 在阿里巴巴网站获得需要的图标

2. 把图标文件目录复制到 src/assets/iconfont目录里边

    

   3. 在login的vue文件中引入css样式

      ```js
      // 引入iconfont的css文件
      import '@/assets/font/iconfont.css'
      ```

      

   4. 给输入框做图标应用

      ```vue
      <el-form-item prop="mobile">
        <!--el-input:普通输入框组件-->
        <!--v-model:必须属性，双向数据绑定-->
        <el-input v-model="loginForm.mobile" placeholder="请输入手机号码">
          <i slot="prefix" class="iconfont icon-shoujihao"></i>
        </el-input>
      </el-form-item>
      <el-form-item prop="code">
        <el-input v-model="loginForm.code" placeholder="请输入校验码">
          <i slot="prefix" class="iconfont icon-yanzhengma"></i>
        </el-input>
      </el-form-item>
      ```



## 左侧导航

el-menu组件标签

```html
<el-menu
  background-color="#353B4E"   // 菜单背景颜色
  text-color="#fff"    // 菜单文字颜色
  active-text-color="#3C9DFF"  // 子菜单选中后的颜色
>
```

> 各个属性都是配置颜色的

```html
<el-submenu index="1">  // 表示当前的菜单拥有子级菜单
<el-menu-item index="2"> // 表示叶子菜单，没有子级
```

> index在父级菜单上边可以设置一个唯一属性用以区分彼此
>
> ​           在子菜单上后期可以设置请求#锚点信息，单击后也执行具体的导航

`注意`：

​	给各个顶级菜单设置**图标**



### 折叠展开效果制作

`步骤`：

1. 给el-menu设置相关属性

   ```js
   :collapse="isCollapse"   // 控制折叠展开
   :collapse-transition="false"  // 禁用折叠动画
   ```

2. 创建data成员 isCollapse=false，控制折叠展开

   ```js
   isCollapse: false  // false:展开   true:折叠
   ```

3. 给"图标"设置单击事件，折叠展开要显示不同的图标(unfold  和 fold 区分)

   ```html
   <i
     slot="prefix"
     :class="isCollapse?'el-icon-s-unfold':'el-icon-s-fold'"
     style="cursor:pointer;"
     @click="isCollapse=!isCollapse"
   ></i>
   ```

   > 菜单折叠展开，小图标也要做变换显示操作

4. 菜单宽度自适应

   

## 退出系统

`具体实现`：

给退出按钮设置单击事件：

```html
<el-dropdown-item @click.native="logout()">退出</el-dropdown-item>
```

在methods中实现退出方法：

```js
    // 退出系统
    logout () {
      this.$confirm('确定要提出系统?', '退出', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        window.sessionStorage.clear()
        this.$router.push('/login')
      }).catch(() => { })
    }
  }
```

`说明`：

给按钮设置点击事件

```html
<button @click="logout()">退出</button>     // 退出事件ok
<el-dropdown-item @click="logout()">退出</el-dropdown-item>   // 事件操作失败
```

@click是vue事件绑定操作，具体是给普通的html标签使用的

el-dropdown-item本身是一个“组件”，组件是组多html标签的集合体，这个集合体绑定事件，不知道具体给到那个标签使用，因此事件绑定失败

解决：

事件绑定设置一个名称为native的修饰符(**事件修饰符**)，使得该事件作用到内部的html标签身上

```html
<el-dropdown-item @click.native="logout()">退出</el-dropdown-item>   // 事件操作失败
```

 

# 文章列表

`说明`：

el-menu组件可以使得本身的菜单项目具备**声明式导航**功能(类似router-link功能)

步骤：

1. 给el-menu设置**router**属性，使得路由导航功能被激活
2. 在el-menu-item的**index**属性中配置锚点信息



`注意`：

Vue中属性绑定布尔值true，可以通过如下两种方式

```html
<标签 :属性="true"><标签>   // 1.普通属性绑定
<标签 属性><标签>           // 2.直接声明空的属性名称
```



### 频道表单域

`步骤`：

1. 在article/index.vue频道列表表单域绘制如下代码：

```html
<el-form-item label="频道列表：">
  <el-select v-model="searchForm.channel_id" placeholder="请选择"  clearable>
    <el-option
      v-for="item in channelList"
      :key="item.id"
      :label="item.name"
      :value="item.id"
    ></el-option>
  </el-select>
</el-form-item>
```

> `说明`：
>
> 1. v-model: 双向绑定，获取选中的项目  或 设置哪个项目选中
> 2. clearable：可以清除选中的项目
>
> 3. label  设置每个项目对外提示的名称
>
> 4. value 设置每个项目真实起作用的value值

2. data支持：

频道demo数据 和 搜索表单数据channel_id频道

```
      // 频道demo数据
      channelList: [
        { id: 201, name: 'ios' },
        { id: 202, name: 'andriod' },
        { id: 203, name: '塞班' }
      ],
      searchForm: {
        status: '1', // 状态
        channel_id: '' // 频道
      }
```



### 时间表单域

`步骤`：

1. 在article/index.vue时间选择表单域绘制如下代码：

```html
<el-form-item label="时间选择：">
  <el-date-picker
    v-model="timetotime"
    type="daterange"
    range-separator="至"
    start-placeholder="开始日期"
    end-placeholder="结束日期"
    value-format="yyyy-MM-dd"
  ></el-date-picker>
</el-form-item>
```

> `说明`
>
> 1. v-model ：双向绑定，获取设置好的时间信息，或设置哪个时间显示
> 2. type="daterange" : 类型设置，daterange表示是日期范围选取的，还有其他可选 year/month/date/dates/ week/datetime/datetimerange/ daterange/monthrange 
> 3. value-format  设置时间格式，例如 yyyy-MM-dd

2. 声明data成员

```js
timetotime: [], // 临时接收时间范围信息
```



`注意`：

el-date-picker组件的v-model="timetotime"接收到的是一个**数组**信息，里边的第1、2个单元分别代表开始日期和结束日期，要想办法把其分配给searchForm的两个成员(begin_pubdate和 end_pubdate)里边去



### watch监听器

监听器就是一致机制，可以监测vue中data数据的变化，并做相关处理

`语法`：

```js
data(){
  return {
    name:'',
    addr:'',
    cat:{
      leg:'',
      tail:'',
      son:{
        name:'小黄',
        weight:50
      }
    }
  }  
}
watch:{
  data成员名称:函数(新值，旧值){}
  name:function(newv,oldv){},
  addr:function(newv,oldv){},
  'cat.leg':function(newv,oldv){},  // 对象成员监听
  'cat.tail':function(newv,oldv){},
  cat: { // 深度监听，内部任意成员变化都会感知到
    handler: function (newv, oldv) { /* ... */ },
    deep: true
  },
}
```

`说明`：

1. 监听器既可以监听**普通成员**、也可以监听**对象成员**，还可以**深度**监听

2. 一般this可以调用的成员属性都可以监听，例如computed计算属性，但是data作为主要使用对象
3. 深度监听，使用**handler**+**deep**关键字达成

`步骤`：

1. 给data  searchForm增加两个成员begin_pubdate和end_pubdate（搜索文章发布的开始和结束时间）

   ```js
   searchForm: {
     begin_pubdate: '', // 文章发布开始时间
     end_pubdate: '' // 文章发布结束时间
   }
   ```

   

2. 给timetotime设置**监听器watch**，值发生变化后做相关处理

   ```js
   watch: {
     // 对timetotime成员进行监听
     timetotime (newval) {
       // 把newval的值拆分分别给到 begin_pubdate和end_pubdate 里边
       if (newval) {
         // 赋予时间信息
         this.searchForm.begin_pubdate = newval[0]
         this.searchForm.end_pubdate = newval[1]
       } else {
         // 清空
         this.searchForm.begin_pubdate = ''
         this.searchForm.end_pubdate = ''
       }
     }
   },
   ```


`注意`：

​	日期选择器有清空功能，因此监听器也要有清空设置	



### 获得真实频道数据展示

`步骤`：

1. data创建成员channelList

   ```js
   channelList: [],
   ```

   

2. 在methods中创建getChannelList方法，其中axios获得数据并赋予给1的channelList里边

   ```js
       // 获取频道列表数据
   		getChannelList () {
         var pro = this.$http.get('/channels')
         pro
           .then(result => {
             if (result.data.message === 'OK') {
               this.channelList = result.data.data.channels
             }
           })
           .catch(err => {
             return this.$message.error('获得文章频道错误：' + err)
           })
       }
   ```

   

3. 在created中调用2的getChannelList方法

   ```js
     created () {
       // 获得频道信息
       this.getChannelList()
     },
   ```

   4. 确认在模板中正确显示

```
             <el-form-item label="频道列表：">
               <el-select v-model="searchForm.channel_id" placeholder="请选择" clearable>
                 <el-option
                   v-for="item in channelList"
                   :key="item.id"
                   :label="item.name"
                   :value="item.id"
                 ></el-option>
                 <!--
                   label:下拉列表小单元对外提示内容
                   value:value值选项
                 -->
               </el-select>
             </el-form-item>
```



### 配置token

在main.js的axios的**请求拦截器**中给配置token

```js
// 配置请求拦截器
axios.interceptors.request.use(function (config) {
  // userinfo并不是始终存在的，要做判断使用
  let userinfo = window.sessionStorage.getItem('userinfo')

  if (userinfo) {
    let token = JSON.parse(userinfo).token
    // 给axios请求头配置token
    config.headers.Authorization = 'Bearer ' + token
  }

  return config
}, function (error) {
  return Promise.reject(error)
})
```

`注意`：

1. 浏览器中并不是始终存在userinfo的用户信息的，也并不是每次请求都要传递token秘钥信息，故要把包含着token的userinfo获得出来，判断存在再赋予给axios，不做判断贸然使用会有错误
2. 根据API接口提示，token信息前边需要  “Bearer ”标志，Bearer后边有<font color=red>空格</font>



### axios闹独立

main.js文件是项目的主入口文件，非常重要，里边的内容如果比较多，会造成后期升级、维护困难度增加

现在要把axios繁琐的代码提取到一个独立文件中，之后再引入使用



`步骤`：

1. 创建src/utils/ax.js文件，从main.js中把axios相关代码剪切过来：

   ```js
   import Vue from 'vue'
   // 引入axios
   import axios from 'axios'
   
   // 公共根地址
   axios.defaults.baseURL = 'http://ttapi.research.itcast.cn/mp/v1_0/'
   // 请求拦截器
   axios.interceptors.request.use(function (config) {
     let userinfo = window.sessionStorage.getItem('userinfo')
     if (userinfo) {
       config.headers.Authorization = 'Bearer ' + JSON.parse(userinfo).token
     }
   
     return config
   }, function (error) {
     return Promise.reject(error)
   })
   
   // 把axios通过原型继承的方式配置给Vue，使得组件内部可以直接访问
   // 后期在组件内部就可以通过 this.$http 的方式获得axios对象
   // $http:就是自定义名称，可以为其他
   Vue.prototype.$http = axios
   ```

   > 需要另行独立引入Vue

2. main.js引入已经独立的axios代码文件

   ```js
   // 引入axios相关
   import '@/utils/ax.js'
   ```



### 获取文章列表信息

`步骤`：

```js
articleList: [], // 文章列表
searchForm:{
  ……
  // 增加分页相关成员
  page: 1, // 默认获取第1页数据
  per_page: 10 // 每页返回10条记录
}
```



2. 在methods里边创建  getArticleList()方法，axios去获得文章列表信息

   ```js
    // 获得文章列表信息
       getArticleList () {
         let pro = this.$http.get('/articles')
         pro
           .then(result => {
             if (result.data.message === 'OK') {
               // 把文章赋予给articleList成员
               this.articleList = result.data.data.results
             }
           })
           .catch(err => {
             return this.$message.error('获得文章列表错误:' + err)
           })
       },
   ```

   

3. 在created中调用 getArticleList() 执行

   ```js
   this.getArticleList()
   ```

  

### table表格-文章列表展示

#### el-table介绍

el-table表格组件语法：

```html
<el-table :data="数据来源(数组对象集)" style="width:100%;">
  <el-table-column label="表格头信息" prop="被显示数据字段名称" width="列宽度(100)"></el-table-column>
  <el-table-column label="……" prop="……" width="……"></el-table-column>
  <el-table-column label="……" prop="……" width="……"></el-table-column>
  <el-table-column label="……" prop="……" width="……"></el-table-column>
</el-table>
```

`说明`：

1. data: 数据来源(数据在组件实例的data中有声明)
2. prop: 定义当前列数据来源的字段名称，来自data数据对象的成员属性名字

3. label: 定义表格列的表头信息

4. width：列的宽度，如果不设置，就自适应占据宽度



`注意`：

​	el-table组件内部已经把 “遍历” 机制给集成好了，我们不用额外设置，多条数据会自动形成多行显示



#### 普通列的展示

`步骤`：

1. 在article/index.vue中设计代码如下：

```html
<el-card class="box-card">
  <div slot="header" class="clearfix">
    <span>共找到{{tot}}条符合条件的内容</span>
  </div>
  <div class="text item">
    <el-table :data="articleList" style="width:100%;">
      <el-table-column label="标题" prop="title" width="300"></el-table-column>
      <el-table-column label="状态" prop="status" width="100"></el-table-column>
      <el-table-column label="发布时间" prop="pubdate" ></el-table-column>
    </el-table>
  </div>
</el-card>
```

2. data中额外声明tot成员接收总记录条数

```js
data(){
  return {
    tot:0 // 全部记录条数
  }
}
```

3. getArticleList()方法中把获得好的总记录条数赋予给tot成员

```js
if (result.data.message === 'OK') {
  this.articleList = result.data.data.results
  this.tot = result.data.data.total_count // 总记录条数
}
```

4. 给卡片域设置外边距

```html
<style lang="less" scoped>
  /*给卡片区设置向下的外边距*/
  .box-card{margin-bottom:15px;}
</style>
```

`说明`：

需要通过**el-card卡片区组件**表现文章列表信息



#### 操作列展示

`实现`：

在操作列里边绘制代码如下

```html
<el-table-column label="操作">
  <el-button type="primary" size="mini">修改</el-button>
  <el-button type="danger" size="mini">删除</el-button>
</el-table-column>
```

> size=“mini”设置按钮大小的，相关选项值有  medium / small / mini 

`说明`：

有的列不适合通过具体的数据信息直接呈现，例如操作列，里边具体要显示 **修改**、**删除** 两个按钮

那么，该column列中不要设置**prop**，而修改、删除 按钮等内容通过“**内容区域**”呈现即可



#### 图标列展示

`实现`：

在图标列里边绘制代码如下

```html
<el-table-column label="图标">
	<img :src="stData.row.cover.images[0]" slot-scope="stData" alt="没有图标" 
       width="150" height="100">
</el-table-column>

```

`说明`：

图标列   与  操作列   有相似的地方，所要呈现的内容都不能直接通过prop获取到

现在需要在column列的“内容区域”中手工绘制   **img标签**

img标签 绘制完毕，其中的src属性 比较特殊，其需要通过后端数据提供，具体是“**作用域插槽**”

stData调用<font color=red>row</font>：代表当前被遍历出来的每个文章记录信息(对象){cover、id、pubdate、status、title等字段}

stData.row.cover.images[0]：代表当前被遍历出来的每条记录的图标信息

原理：

```
模拟el-table-column组件内容
<template>
	<div>
		<slot row="每个文章的记录信息，是一个对象，里边有各个成员"></slot>
	</div>
</template>
```

`注意`：

在每个el-table-column组件内部都可以通过**作用域插槽**获得当前被遍历出来的各个文章信息，插槽属性名称都是通过**row**	

子组件：

```
<slot a="10" b="20" row="每条文章记录信息，是一个对象，里边有各个成员"></slot>
```

父组件：

```
<子组件>
	<标签 slot-scope="stData">{{stData.a}}---{{stData.b}}---{{stData.row.xxx}}</标签>
</子组件>
```



#### 状态列展示

`实现`：

状态列   与  操作列   有相似的地方，所要呈现的内容都不能通过prop获取，相反要在内容区域中设置

在状态列里边绘制代码如下

```html
<el-table-column label="状态">
  <!--如果当前内容区域中多个标签都使用了 作用域插槽，
			可以优化为：提供一个父级的template标签统一使用作用域插槽-->
  <template slot-scope="stData">
    <el-tag v-if="stData.row.status===0">草稿</el-tag>
    <el-tag v-else-if="stData.row.status===1" type="success">待审核</el-tag>
    <el-tag v-else-if="stData.row.status===2" type="info">审核通过</el-tag>
    <el-tag v-else-if="stData.row.status===3" type="warning">审核失败</el-tag>
    <el-tag v-else type="danger">已删除</el-tag>
  </template>
</el-table-column>
```

`说明`：

1. el-tag是一个通过type属性体现不同样式效果的组件标签
2. 多个el-tag组件标签都要使用数据部分，作用域插槽不用体现多份，为了减少重复代码编写量，可以使用一个公共的父级**template标签统一**接收使用



### 获得文章数据补充条件

给获得文章的方法getArticleList()增加文章检索条件参数，并对空的条件做过滤

```js
    // 获得文章列表信息
    getArticleList () {
      // 把searchForm内部为空的成员都过滤掉
      let searchData = {}
      for (var i in this.searchForm) {
        // i:代表对象的成员属性名称, status、channel_id、begin_pudate等等
        if (this.searchForm[i]) {
          // 成员值非空
          searchData[i] = this.searchForm[i]
        }
      }

      let pro = this.$http.get('/articles', { params: searchData })
      pro
        .then(result => {
          console.log(result)
          if (result.data.message === 'OK') {
            // 把文章赋予给articleList成员
            this.articleList = result.data.data.results
            // 把total_count中条数信息赋予给tot成员
            this.tot = result.data.data.total_count
          }
        })
        .catch(err => {
          return this.$message.error('获得文章列表错误:' + err)
        })
    },
```



el-pagination分页组件属性解读：

```html
<el-pagination
               @size-change="handleSizeChange"
               @current-change="handleCurrentChange"
               :current-page="currentPage4"
               :page-sizes="[100, 200, 300, 400]"
               :page-size="100"
               layout="total, sizes, prev, pager, next, jumper"
               :total="400"
               >
</el-pagination>
```

> ​          @size-change="handleSizeChange"  // 每页显示条数变化的处理事件，需要methods方法配合
>
> ​          @current-change="handleCurrentChange" // 当前页码变化的回调处理事件，需要methods方法配合
>
> ​          :current-page="currentPage4" // 默认当前页码 1
>
> ​          :page-sizes="[100, 200, 300, 400]" // 下拉列表，设计每页显示条数的
>
> ​          :page-size="100" // 默认每页显示条数
>
> ​          layout="total, sizes, prev, pager, next, jumper" // 分页元素构成设计
>
> ​          :total="400" // 记录总条数



### 应用

步骤：

1. 应用el-pagination组件，并设置相关属性

   ```html
   <el-pagination
     @size-change="handleSizeChange"
     @current-change="handleCurrentChange"
     :current-page="searchForm.page"
     :page-sizes="[10, 15, 20, 40]"
     :page-size="searchForm.per_page"
     layout="total, sizes, prev, pager, next, jumper"
     :total="tot"
   ></el-pagination>
   ```

   > 以上 current-page、page-size、total 的值来自**data**声明的
   >
   > @size-change和@current-change 需要在**methods**中声明空方法




2. 页码 和 每页条数  变化处理更新

   在methods中声明相关方法

   ```js
   // 当前页码变化的回调处理
   handleCurrentChange (val) {
     // val: 变化后页码的值
     // console.log(val)
     // 把val赋予给searchForm.page成员
     this.searchForm.page = val
     // 根据变化后的条件，重新获得记录信息
     this.getArticleList()
   },
     // 每页数据记录条数变化的回调处理
     handleSizeChange (val) {
       // val: 变化后的页码条数
       // console.log(val)
       // 把val赋予给searchForm.per_page
       this.searchForm.per_page = val
       // 根据变化后的per_page重新获取数据
       this.getArticleList()
     },
   ```

   

3. 相关data数据支持

   ```js
   data () {
     return {
       searchForm: {
         page: 1,
         per_page: 10
       },
       tot: 0 // 总记录条数
     }
   },
   ```

   

4. 设置css样式，使得分页有向上的外边距

   ```css
   .el-pagination{
     margin-top:15px;
   }
   ```



## 筛选过滤

`实现`：

​	给el-radio单选按钮升级处理，通过el-radio-group组别圈选设置

​	以便给el-radio-group组别设置change内容改变事件

​	再者多个radio的v-model 可以通过group设置一次即可

```html
<el-form-item label="文章状态：">
  <el-radio-group v-model="searchForm.status" @change="getArticleList()">
  	<el-radio label>全部</el-radio>
  	<el-radio label="0">草稿</el-radio>
  	<el-radio label="1">待审核</el-radio>
  	<el-radio label="2">审核通过</el-radio>
  	<el-radio label="3">审核失败</el-radio>
  	<el-radio label="4">已删除</el-radio>
  </el-radio-group>
</el-form-item>
```



为什么要使用group做分组

答：该group可以统一给多个radio单选按钮设置change事件，当一个项目被选中后，可以被感知，之后可以调用getArticleList()方法，根据变化后的文章状态获取对应的文章列表数据



87期同学通过watch监听器实现的状态筛选文章：

```html
<el-form-item label="文章状态：">
  <el-radio-group v-model="searchForm.status" @change="getArticleList()">
  	<el-radio label>全部</el-radio>
  	<el-radio label="0">草稿</el-radio>
  	<el-radio label="1">待审核</el-radio>
  	<el-radio label="2">审核通过</el-radio>
  	<el-radio label="3">审核失败</el-radio>
  	<el-radio label="4">已删除</el-radio>
  </el-radio-group>
</el-form-item>
```



```js
  watch: {
    // status变化的回调处理
    'searchForm.status': function (newv, oldv) {
      // 更新相关文章即可
      this.getArticleList()
    },
  }
```



### 频道下拉列表筛选

`实现`：

给频道的下拉列表组件设置change事件，使得项目变化被感知，并根据变化后频道获得文章

```html
<el-select 
           v-model="searchForm.channel_id" 
           placeholder="请选择" 
           clearable 
           @change="getArticleList()" >
```



### 时间范围筛选

`实现`：

在timetotime的watch监听器的最后设置getArticleList()方法调用，获取最新的文章

```js
  watch: {
    // 对timetotime成员进行监听
    timetotime (newval) {
      // 把newval的值拆分分别给到 begin_pubdate和end_pubdate 里边
      if (newval) {
        this.searchForm.begin_pubdate = newval[0]
        this.searchForm.end_pubdate = newval[1]
      } else {
        this.searchForm.begin_pubdate = ''
        this.searchForm.end_pubdate = ''
      }
      // 根据最新的时间范围，获得对应文章信息
      this.getArticleList()
    }
  },
```



汇总：

```js
  // 对searchForm的各个成员多深度监听，统一筛选获得文章，其他地方的getArticleList都可以省略了
	watch:{
    searchForm: {
      handler: function (newv, oldv) {
        this.getArticleList()
      },
      deep: true
    }
  }
```



## 401状态码的处理

axios向服务器端发送请求时有两种情况会出现401状态码(unauthorized未授权)：

1. 服务端要求传递token信息，而实际没有传递
2. 我们有传递token到达服务器端，但由于时间比较久，这个token在服务器中已经过期了(服务器存储token有效期时间为2个小时)

总之，服务器端有些api接口要求传递token，我们的token失效或没有传递，就会报401错误

第1种情况，已经在**axios请求拦截器**中做token传递操作了

第2种情况，可以这样设置，在**axios响应拦截器**中判断请求状态如果是401，就强制用户重新登录系统



`第2中情况处理实现`：

在axios的响应拦截器中，判断错误码等于401就强制登录

```js
// 引入路由
import router from '@/router'
…………
// axios配置响应拦截器
axios.interceptors.response.use(function (response) {
  // response：服务器端返回的数据信息，与 then(result=>{}) 的result一致
  return response
}, function (error) {
  // 判断响应状态码如果登录401，就强制登录
  // error对象
  // error.response.status======401
  // console.dir(error)
  if (error.response.status === 401) {
    // 强制登录
    router.push({ name: 'login' })
  }
  return Promise.reject(error)
})
```

`注意`：

路由对象.push(xxx) 可以实现编程式导航

路由对象：在组件中是  this.$router ，在main.js中就是router，要在ax.js中对路由模块做导入才可以使用



# 发布文章

创建src/views/articleadd/articleadd.vue 组件文件

```vue
<template>
    <div>发表文章展示</div>
</template>

<script>
export default {
  name: 'ArticleAdd'
}
</script>

<style lang="less" scoped>
</style>
```

1. 在src/router/index.js中创建路由(home子路由)

   ```js
   { 
     path: '/articleadd', 
     name: 'articleadd', 
     component: () => import('@/views/articleadd/articleadd.vue') 
   }
   ```

   

2. 在src/views/home/index.vue中为发表文章创建导航路由菜单

   ```html
   <el-menu-item index="/articleadd">发布文章</el-menu-item>
   ```


## 绘制表单

`实现`：

绘制 **标题**(普通输入框)、**内容**(普通输入框)、**封面**(单选按钮)、**频道**(下拉列表) 4个表单域，

其中频道的创建 与 文章列表页面完全一致

1. ​	创建data成员channelList
2. ​	methods方法getChannelList()
3. ​	created调用getChannelList()
4. el-select组件应用

具体代码如下：

```html
<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>发表文章</span>
      </div>
      <div class="text item">
        <el-form ref="addForm" :model="addForm" label-width="120px">
          <el-form-item label="标题：">
            <el-input v-model="addForm.title"></el-input>
          </el-form-item>
          <el-form-item label="内容：">
            <el-input v-model="addForm.content"></el-input>
          </el-form-item>
          <el-form-item label="封面：">
            <el-radio-group v-model="addForm.cover.type">
              <el-radio :label="1">单图</el-radio>
              <el-radio :label="3">三图</el-radio>
              <el-radio :label="0">无图</el-radio>
              <el-radio :label="-1">自动</el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="频道：">
             <el-select
              v-model="addForm.channel_id"
              placeholder="请选择"
              clearable
            >
              <el-option
                v-for="item in channelList"
                :key="item.id"
                :label="item.name"
                :value="item.id"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>
```

```html
<script>
export default {
  name: 'ArticleAdd',
  data () {
    return {
      channelList: [], // 接收频道列表数据
      addForm: {
        title: '', // 文章标题
        content: '', // 文章内容
        cover: {
          type: 0, // 封面类型 -1:自动，0-无图，1-1张，3-3张
          images: []
        },
        channel_id:'' // 频道
      }
    }
  },
  created () {
    this.getChannelList()
  },
  methods: {
    // 获取频道列表数据
    getChannelList () {
      var pro = this.$http.get('/channels')
      pro
        .then(result => {
          if (result.data.message === 'OK') {
            this.channelList = result.data.data.channels
          }
        })
        .catch(err => {
          return this.$message.error('获得文章频道错误：' + err)
        })
    }
  }
}
</script>
```



## 使用富文本编辑器

github中有一个名称awesome(厉害、强大的) 的资源汇总页面，把与计算机项目开发有关系的技术、文章、话题等给罗列出来了

想要什么资源都可以到其中去获取

github里边awesome的直接请求地址：https://github.com/sindresorhus/awesome

vue的话题汇总：vuejs/awesome-vue（github） https://github.com/vuejs/awesome-vue#readme 

我们要使用富文本编辑器名称为：vue-quill-editor  https://github.com/surmon-china/vue-quill-editor 



富文本编辑器应用步骤：

1. 安装 yarn add vue-quill-editor

2. 在应用组件中引入3个css文件

   ```js
   import 'quill/dist/quill.core.css'
   import 'quill/dist/quill.snow.css'
   import 'quill/dist/quill.bubble.css'
   ```

   

3. 在应用组件中引入quillEditor模块

   ```js
   // 通过es6按需导入方式 导入需要的组件模块
   import { quillEditor } from 'vue-quill-editor'
   ```

   

4. 在应用组件中注册 quillEditor模块 为具体的组件

   ```js
     components: {
       // 简易成员赋值 quillEditor: quillEditor
       // 组件使用两种方式：<quillEditor></quillEditor> 或 <quill-editor></quill-editor>
       quillEditor
     },
   ```

   

5. 应用编辑器组件即可

   ```html
   有两种方式引用编辑器组件：
   <quillEditor v-model="addForm.content"></quillEditor>
   <quill-editor v-model="addForm.content"></quill-editor>
   ```

   > <quillEditor>  或  <quill_editor>

6. 给编辑器区域设置高度(500)

   ```html
   <style lang="less" scoped>
   /*给富文本编辑器设置内容区域高度*/
   /* .ql-editor{   .ql-editor[data-v-xxx]不对了*/
   /*deep：深度作用选择器，使得编译后的效果为：.el-form[data-v-xx] .ql-editor{}*/
   .el-form /deep/ .ql-editor{
    height:200px;
   }
   </style>
   ```

   > deep是深度作用选择器的体现(还可以使用 >>>)
   >
   > 注意：在articleadd/index.vue的结尾处重新创建一个**没有scoped属性**的style设置编辑器高度样式

## 深度作用选择器

当前组件A 引入一个其他组件B做应用

A组件由于scoped作用，本身的全部html标签都会包含一个 data-v-xxx 的属性名称，使得css样式达到私有效果

被使用的组件B由于某些原因，编译解析后各个html标签**不会**形成 data-v-xxx 的属性，这样在组件A中给组件B设置样式会导致无效

解决：

通过深度作用选择器/deep/ 给B组件的某些标签设置样式

```
.a /deep/ .b { /* ... */ }
```

a是组件A的选择器，b是组件B的选择器，它们会形成如下效果

```css
.a[data-v-f3f3eg9] .b { /* ... */ }
```

这样.b的css样式就生效了



深度作用选择器： https://vue-loader.vuejs.org/zh/guide/scoped-css.html#

`注意`：

1. 某些情况下>>>符号有可能无法正确解析，可以替换为别名  /deep/ 或 ::v-deep
2. 深度作用选择器的**左边**必须是当前组件的css选择器，**右边**是子组件标签选择器



## 表单校验

`步骤`：

1. 给el-form设置 :rules="addFormRules" 属性

   ```html
   <el-form ref="addFormRef" :model="addForm" label-width="120px" 
            :rules="addFormRules">
   ```

   > 注意：  :rules 带“冒号”属性绑定设置

2. 给各个表单域项目配置prop   el-form-item prop="xxx"

   ```html
   <el-form-item label="标题：" prop="title">
   <el-form-item label="内容：" prop="content">
   <el-form-item label="频道：" prop="channel_id">
   ```

   

3. 在data中配置具体校验规则

   ```js
   // 表单校验规则
   addFormRules: {
     title: [
       { required: true, message: '标题必填' },
       // 后端要求title长度介于5-30个字符
       {
         min: 5,
         max: 30,
         message: '标题长度介于5-30个字符'
       }
     ],
     content: [{ required: true, message: '内容必填'}],
     channel_id: [{ required: true, message: '频道必选'}]
   },
   ```

## 存储数据

`步骤`：

1. 创建发布按钮

   ```html
   <el-form-item>
     <el-button type="primary" @click="addarticle(false)">发布</el-button>
     <el-button @click="addarticle(true)">存入草稿</el-button>
   </el-form-item>
   ```

   > 按钮click事件要去传入 true/false参数，表示 存入草稿 或 正式发布

2. 制作发布文章的methods方法

   ```js
   // 添加文章-收集数据存储
   // flag:true  发布一个草稿文章
   // flag:false 发布一个正式文章
   addarticle (flag) {
     // 表单校验
     this.$refs.addFormRef.validate(valid => {
       if (valid) {
         // 把被添加的文章信息通过axios传递给服务器端存储
         // axios发起post请求的时候，不仅可以传递post数据还可以传递get请求字符串信息
         // this.$http.post(地址,post数据,get请求字符串信息)
         var pro = this.$http.post('/articles', this.addForm, {
           params: { draft: flag }
         })
         pro
           .then(result => {
             this.$message.success('文章发布成功')
             this.$router.push({ name: 'article' })
           })
           .catch(err => {
             return this.$message.error('发布文章失败' + err)
           })
       }
     })
   },
   ```

   > axios进行post请求的同时，本身通过第3个参数还可以传递get请求字符串信息



注意：

在addForm表单里边要求设置addForm.cover.type的类型为整型的，并且要设置**为0**，表示无图,切记切记！

```js
cover: {
  type: 0,  // 整型的0
  images: []
},
```



# 文章删除

后端服务器给我们返回的文章id已经大大超过了js可以表达的整型范畴，因而使用的时候会发生**变型**

例如：

​	本质id为：1194555075163324416

​	变型后为：1194555075163324400

​	通过console.log(1194555075163324416 )输出即可看出

答：文章的id是整型的信息，并且已经超过了javascript语言可以表达的最大整型范畴

```js
// javascript中可以表达的最大整型可以通过如下代码获得
console.log( Number.MAX_SAFE_INTEGER )
// 输出：9007199254740991
```

首次文章删除失败原因：

文章的id由于太大了，变型为一个其他信息了，导致后端无法删除该记录了

## 大数字处理依赖包介绍

项目中如果使用一些超出javascript语言限制的大整型数字信息，该数字会变形为其他信息，为了避免产生问题，可以通过json-bigint做转换，使得大整型数字可以正常使用，这就是json-bigint的作用

`原理`：

​	json-bigint会把大整型的数字信息拆分个小段信息存储到数组的各个元素中，待使用的时候再拼接到一起变为字符串

github网站相关介绍： https://github.com/sidorares/json-bigint 



json-bigint使用示例：

```js
var JSONBig = require('json-bigint');  // 需要先安装 yarn add json-bigint
var str = '{ "value" : 9223372036854775807, "v2": 123 }';

var obj = JSONBig.parse(str) // 字符串--->对象
console.log(obj.value) // 9223372036854775807(正确)

var obj2 = JSON.parse(str) // 字符串--->对象
console.log(obj2.value) // 9223372036854776000(错误)
```

结论：

​	json-bigint需要对一个包含大整型信息的“**字符串**”做转换处理变为对象，这个对象可以获得正确的大数字信息



## 大数字具体处理

服务器给客户端返回数据的第一手处理者是 “转换器( transformResponse )”，转换器处理完毕再交给响应拦截器使用，故要对大数字信息做处理，下手点是"转换器"(响应拦截器获得数据已经是变形后的内容了)

> 本质上：服务器返回信息的类型是“字符串”，要经过转换器做JSON.parse()转化处理，所以响应拦截器接收到的是对象



`步骤`：

1. 给项目安装工具依赖包   

   ```bash
   yarn add json-bigint
   ```

   

2. 在src/utils/ax.js中引入json-bigint模块，对服务器返回的信息做处理，具体通过axios的 “数据转换”  机制实现

   ```js
   // 引入json-bigint
   import JSONbig from 'json-bigint'
   ……
   // 对服务器端返回来的数据信息做处理(尤其是大数字的处理)
   // axios配置"数据转换器"
   axios.defaults.transformResponse = [function (data) {
     // 服务器端返回给客户端的data数据主要就两种类型
     // 1) 字符串对象  '{xx:xx...}'
     // 2) 空字符串   ''
     // 在此处要利用JSONbig对返回的信息加以处理，如果不处理，系统默认是通过JSON.parse()给处理的
     // 这样大数字就错误了
     if (data) {
       return JSONbig.parse(data)
     } else {
       return data
     }
   }]
   ```

   > 注意：
   >
   > 上述数据转换一定要设置else，以便对空字符串的做处理，因为服务器有时候会返回空字符串信息

3. 给文章列表的删除按钮设置del()删除事件，同时传递被删除文件的id

   ```html
   <el-button type="danger" size="mini" @click="del(stData.row.id)">删除</el-button>
   
   ```

4. 在methods里边定义del()方法实现删除逻辑

   


`注意`：

​	json-bigint处理的是**字符串类型**的信息，大数字给处理，普通信息不给与处



# 修改文章

1. 创建articleedit/articleedit.vue组件，  内容可以全盘复制**添加文章**组件的

   注意替换字眼

   > 发布/添加-->修改
   >
   > addForm-->editForm
   >
   > ArticleAdd-->ArticleEdit
   >
   > addarticle-->editarticle

   
   
2. 创建路由，要求传递被修改文章aid参数 

   ```js
   { 
     path: '/articleedit/:aid', 
     name: 'articleedit', 
     component: () => import('@/views/articleedit') 
   }
   ```

3. 给文章列表页面的 修改 按钮设置单击事件，其会进行路由跳转，注意传递id参数

   ```html
   <template slot-scope="stData">
     <el-button type="primary" size="mini" 
                @click="$router.push(`/articleedit/${stData.row.id}`)">修改</el-button>
     <el-button type="danger" size="mini" @click="del(stData.row.id)">删除</el-button>
   </template>
   ```




## 展示修改文章内容

`步骤`：

1. 为了获得aid路由参数比较方便，可以通过computed计算属性做封装

   ```js
     computed: {
       // 被修改文章id
       aid () {
         return this.$route.params.aid
       }
     },
   ```

   > 之前获得文章id参数： this.$route.params.aid
   >
   > 计算属性封装后： this.aid

2. articleedit/index.vue中声明 getArticleByAid()的methods方法，根据aid获得被修改文章并赋予给editForm成员

   ```js
   // 根据id获得文章信息
   getArticleByAid () {
     let pro = this.$http.get(`/articles/${this.aid}`)
     pro
       .then(result => {
       if (result.data.message === 'OK') {
         // 把文章赋予给editForm里边
         this.editForm = result.data.data
       }
   
     })
       .catch(err => {
       return this.$message.error('获得文章失败！：' + err)
     })
   },
   ```

   

3. 在created中调用 getArticleByAid()方法

   ```js
   created () {
     this.getChannelList() // 获得频道
     this.getArticleByAid() // 获得指定文章
   },
   ```

现在 点击 修改按钮，修改页面已经可以把被修改文章显示出来了(表单中各个表单域的v-model都是事先准备好的)





## 修改文章，存储入库

`实现`：

在editarticle()方法中 [对应添加文章的addarticle方法] ，把之前的post请求改为**put**修改的请求，同时在请求地址中把**aid**设置好

```js
  // 修改文章
  // flag=true  是存入草稿
  // flag=false  正式发布
  editarticle (flag) {
    // 表单校验
    this.$refs.editFormRef.validate(valid => {
      if (valid) {
        // 表单校验成功
        // get:获取操作
          // post:添加操作
          // put：修改操作
          // delete：删除操作
        let pro = this.$http.put(`/articles/${this.aid}`, this.editForm, { params: { draft: flag } })
        pro
          .then(result => {
            if (result.data.message === 'OK') {
              this.$message.success('修改文章成功！')
              // 跳转到列表页面
              this.$router.push('/article')
            }
          })
          .catch(err => {
            return this.$message.error('修改文章失败！：' + err)
          })
      }
    })
  },
```



## 创建独立组件

`步骤`：

1. 创建组件文件src/components/channel.vue，内容如下

   通过**添加文章组件**把频道相关的4部分(el-select/channelList/created/getChannelList())内容复制过来

   具体内容有：**el-select组件**、data成员(**chid**、**channelList**)、**getChannelList()方法**、**created**、

   ​					**props**[cid]、**watch**监听器[cid、chid]

   ```vue
   <template>
     <el-select v-model="chid" placeholder="请选择" clearable>
       <el-option v-for="item in channelList" :key="item.id" :label="item.name" :value="item.id"></el-option>
     </el-select>
   </template>
   
   <script>
   // 当前子组件拥有名称为slt的事件(是父组件给声明的)
   // 对chid做监听(watch/change)，有变化，就调用slt事件，并把chid传递给父组件
   export default {
     name: 'ChannelCom',
     // 接收父组件传递过来的数据信息
     // props:[xx,xx,xx]
     // props:{
     //   xx:{
     //     type:Number/Object/Array/Boolean, 类型限制
     //     default:0 // 给设置默认值
     //   }
     //   xx:{}
     // }
     props: {
       // 接收父给子传递的频道信息
       cid: {
         default: 0 // 设置默认值
       }
     },
     watch: {
       // 对cid做监听，使得cid的信息被赋予给chid使用
       cid: function (newV, oldV) {
         this.chid = newV
       },
       // 对chid做监听
       chid: function (newV, oldV) {
         // 调用自己的slt方法
         this.$emit('slt', this.chid)
       }
     },
     data () {
       return {
         chid: '', // 记录当前选中的频道信息
         channelList: [] // 频道列表
       }
     },
     created () {
       // 获得频道列表
       this.getChannelList()
     },
     methods: {
       // 获得频道
       getChannelList () {
         let pro = this.$http.get('/channels')
         pro
           .then(result => {
             // console.log(result) // config 【data】 request headers  status statusText
             if (result.data.message === 'OK') {
               // 把获得好的频道给与channelList成员
               this.channelList = result.data.data.channels
             }
           })
           .catch(err => {
             return this.$message.error('获得频道错误:' + err)
           })
       }
     }
   }
   </script>
   
   <style lang="less" scoped>
   </style>
   ```

`注意`：

1. 给独立组件的el-select设置自己的**v-model="chid" ** 的属性值 和 data chid:'' 成员

    

## 添加文章应用

`步骤`：	

1. **添加文章**的组件views/articleadd/articleadd.vue中

   **去除**之前的频道相关内容(el-select、channelList成员、getChannelList()、created调用等)

   A.应用频道独立组件：

   ```html
   <el-form-item label="频道" prop="channel_id">
     <channel-com @slt="selectHandler"></channel-com>
   </el-form-item>
   ```
   
> @slt是给channel-com组件声明的事件，名称为slt，selectHandler是事件响应方法，需要在当前组件(父组件)methods中声明好

B.引入注册频道

```js
   // 引入频道公共组件
   import ChannelCom from '@/components/channel.vue'
   …………
     components: {
   		// 注册频道独立组件
       ChannelCom
     },
```

   C. 设置频道methods事件方法

   ```js
// 频道组件方法，获得子组件传递过来的频道id并赋予给channel_id成员
   // val:子组件给传递过来的频道信息
   selectHandler (val) {
     this.addForm.channel_id = val
   },
   ```

`注意`：

​	@slt="selectHandler",不要设置()括号




## 文章列表应用

1. **文章列表**的组件views/article/index.vue中

   去除之前的频道相关内容(el-select、channelList成员、getChannelList()、created相关等)

   A.应用频道独立组件：

   ```html
   <el-form-item label="频道列表：">
     <channel-com @slt="selectHandler"></channel-com>
   </el-form-item>
   ```
   

B.引入注册频道

```js
   // 引入频道公共组件
   import ChannelCom from '@/components/channel.vue'
   …………
   
     components: {
   		// 注册频道独立组件
       ChannelCom
     },
```

   C. 设置频道methods事件方法

   ```js
// 频道组件方法，获得子组件传递过来的频道id并赋予给channel_id成员
       selectHandler (val) {
         this.searchForm.channel_id = val
       },
   ```

   > 注意：上边是给searchForm的channel_id填充信息

## 修改文章应用

1. **修改文章**的组件views/articleedit/articleedit.vue中

   去除之前的频道相关内容(el-select、channelList成员、getChannelList()方法、created相关等)

   A.应用频道独立组件：

   ```html
   <el-form-item label="频道" prop="channel_id">
     <channel-com @slt="selectHandler" :cid="editForm.channel_id"
                  ></channel-com>
   </el-form-item>
   ```
   
> :cid 是给子组件传递的信息，是当前被修改文章拥有的频道id，这样子组件就会把默认的频道选中显示了

B. 另外需要在channel.vue组件中给cid设置**watch监听器**  和 **props**接收cid属性

```js
     props: {
       // cid的值有类型 和 默认值 修饰
       cid: {
         // type: Number, // Object Array
         default: 0 // 设置默认值
       }
     },
   	watch: {
       // 监听父组件是否有传递cid信息过来，有的话，就接收赋予给chid，使得频道有默认显示项目
       cid: function (newV, oldV) {
         this.chid = newV
       }
     },
```

   

   C.引入注册频道

   ```js
// 引入频道公共组件
   import ChannelCom from '@/components/channel.vue'
   …………
   
     components: {
   		// 注册频道独立组件
       ChannelCom
     },
   ```

   D. 设置频道methods事件方法

```js
   selectHandler (val) {
  this.editForm.channel_id = val
   },
```

   > 注意：表单名称为editForm

`应用到的技术`：

1. 父组件给子组件传值
2. 子组件给父组件传值
3. watch监听器



props使用说明： https://vue.docschina.org/v2/api/#props 

两种方式：数组和对象

```js
// 简单语法
Vue.component('props-demo-simple', {
  props: ['size', 'myMessage']
})

// 对象语法，提供校验
Vue.component('props-demo-advanced', {
  props: {
    // 检测类型
    height: Number,
    // 检测类型 + 其他验证
    age: {
      type: Number,
      default: 0,
      required: true,
      validator: function (value) {
        return value >= 0
      }
    }
  }
})
```



`注意`：

​	文章 添加、修改、列表 各个页面中都需要定义 channel-com组件的事件响应方法**selectHandler**，但是它们调用的表单名称不一样，分别是：**addForm**、**editForm**、**searchForm**



## 文章列表检索优化(已经完成)

`步骤`：

1. 给searchForm做watch深度监听，条件变化就重新获得文章列表

   ```js
     watch: {
       // 给searchForm做深度监听
       searchForm: {
         handler: function (newV, oldV) {
           // 内部成员有变化，就根据变化的条件重新检视数据
           this.getArticleList()
         },
         deep: true
       },
     }
   ```
   
2. 把之前关于检索的各个getArticleList()方法调用都删除掉(包括分页)

由于之前已经给searchForm做了深度监听更新数据机制，现在频道即使独立出去使用，也不影响文章筛选功能



# 组件传值

父组件可以  引入、使用 子组件，从业务上看，该父组件有可能对子组件有**个性化**需求，为了体现组件的**灵活多变**，可以通过**传值**实现

`语法`：

父组件要在子组件标签上通过**属性值**方式传值

```html
<子组件标签 name=value name=value name=value></子组件标签>
```

子组件接收并应用值，具体通过props接收

```html
<!--在模板中应用传递来的数据-->
<input :style="{color:xx}">

<script>
  export default {
    // 通过props接收父传递过来的数据,注意各个名称需要使用单引号圈选
    // 具体有两种方式：
    props:['xx','xx','xx'],
    props:{
      xx:{
        type:类型限制
        default:默认值
      }
    }
  }
</script>
```



## 子给父传递

`步骤`：

1. 父组件 向子组件 传递一个事件，本身声明事件的methods方法

2. 子组件 调用 父组件 传递过来的事件，并传递相关的数据

3. 父组件 通过事件方法参数获得子组件传递过来的数据并使用



**`父组件操作语法`**：

父组件通过**@符号**向子组件传递一个<font color=red>事件方法</font>

```
<子组件 @func1="show"></子组件>
...
methods:{
	show(arg1,arg2){xxxx}
}
```

其中

​	func1为事件的名称，给子组件触发使用

​	show为该事件的执行函数，在父组件内部的methods中定义好

​	在事件中可以通过形参(arg1、arg2)接收子组件出来过来的数据 并做近一步处理



**`子组件操作`**：

子组件中，使用<font color=red>this.$emit()</font>调用 父组件中的方法

```js
$emit:使得子组件调用 自己的事件方法(父组件给声明的)
this.$emit('func1', 数据, 数据)
this:当前子组件对象(组件实例)
func1:是父组件给子组件声明的事件方法，通过第2、3位置设置给父组件传递的数据
```

从第二个位置开始传递实参数据，其可以被父组件methods方法的形参所接受

$emit(名称，数据，数据……) 是组件调用自己方法的固定方式，第一个参数是被调用方法的名称，后续参数都是给方法传递的实参信息



# 账户管理

模板部分：

```html
<template>
  <!--卡片区-->
  <el-card class="box-card">
    <!--命名插槽，头部内容设置-->
    <div slot="header" class="clearfix">
      <span>账户信息</span>
    </div>
    <!--匿名插槽，卡片主体内容-->
    <div class="text item cardbody">
      <div id="lt">
        <el-form ref="accountFormRef" :model="accountForm" label-width="100px">
          <el-form-item label="用户名：">
            <el-input v-model="accountForm.name"></el-input>
          </el-form-item>
          <el-form-item label="手机号码：">
            <el-input v-model="accountForm.mobile" disabled></el-input>
          </el-form-item>
          <el-form-item label="邮箱：">
            <el-input v-model="accountForm.email"></el-input>
          </el-form-item>
          <el-form-item label="简介：">
            <el-input type="textarea" v-model="accountForm.intro"></el-input>
          </el-form-item>
          <el-form-item label="简介：">
            <el-button type="primary" @click="upAccount()">更新账户</el-button>
          </el-form-item>
        </el-form>
      </div>
      <div id="rt">头像展示区域</div>
    </div>
  </el-card>
</template>

```

> 注意：给手机号码设置disabled，禁用设置

组件实例部分：

```html
<script>
export default {
  name: 'Account',
  data () {
    return {
      accountForm: {
        // 各个成员来自api参考【2.4 编辑用户资料】
        id: '', // id
        name: '', // 名称
        mobile: '', // 手机号码
        email: '', // 邮箱
        intro: '' // 简介
      }
    }
  }
}
</script>
```



## 获得当前账户信息并显示

`步骤`：

1. 创建methods方法 getAccountInfo()，通过axios获得账户信息 并赋予给  editForm成员

   ```js
       // 获得账户基本信息
       getAccountInfo () {
         let pro = this.$http.get('/user/profile')
         pro
           .then(result => {
             if (result.data.message === 'OK') {
               // 把获得账户的信息赋予给accountForm
               this.accountForm = result.data.data
             }
           })
           .catch(err => {
             return this.$message.error('获得账户失败：' + err)
           })
       }
     }
   ```
   

   
2. 在created中调用 getAccountInfo() 方法

   ```js
     created () {
       // 获取账户信息
       this.getAccountInfo()
     },
   ```
   



## 表单校验

`步骤`：

1. 给el-form设置 :rules="accountFormRules" 属性

   ```html
   <el-form ref="accountFormRef" :model="accountForm" label-width="100px"
            :rules="accountFormRules">
   ```
   

   
2. 给各个表单域项目配置prop 

   ```html
   <el-form-item label="用户名：" prop="name">
   
   <el-form-item label="邮箱：" prop="email">
   ```
   

   
3. 在data中配置具体校验规则

   ```js
   // 表单校验
   accountFormRules: {
     name: [
       { required: true, message: '名字必填' },
       // 后端要求title长度介于1-7个字符
       {
         min: 1,
         max: 7,
         message: '名字长度介于1-7个字符之间'
       }
     ],
     email: [
       { required: true, message: '邮箱必填' },
       { type: 'email', message: '邮箱格式不正确' }
     ],
       /*
     mobile: [
       { required: true, message: '手机号码必填' },
       { pattern: /^1[35789]\d{9}$/, message: '手机号码格式不对' }
     ]
     */
   }
   ```

`注意`：

​	**服务器端**有如下验证规则：

​	账户名字：名字长度：1-7个字符之间

​	邮箱：@符号前边要求是1-12个字符之间



## 修改账户存储入库

`步骤`：

1. 创建 “修改账户” 按钮 并设置 单击事件 editAccount

   ```html
   <el-button type="primary" @click="editAccount()">更新账户</el-button>
   ```
   

   
2. 在methods中声明成员  editAccount()方法，axios传递表单数据给服务器端存储

   ```js
       // 更新账户，收集并存储数据到服务器端
       editAccount () {
         // 表单校验
         this.$refs.accountFormRef.validate(valid => {
           if (valid) {
             // axios行动了
             // get/post/put/delete
             // put: 修改，修改全部表单
             // patch：修改，修改部分项目
             let pro = this.$http.patch('/user/profile', this.accountForm)
             pro
               .then(result => {
                 if (result.data.message === 'OK') {
                // 提示成功
                   this.$message.success('修改账号信息成功')
              	}
               })
               .catch(err => {
                 return this.$message.error('修改失败：' + err)
               })
           }
         })
       },
   ```
   



## 上传头像

回顾：

```
附件上传
<form id="fm">
<input type="file" name="mypic">
<button onclick="send()">提交</button>

<script>
FormData表单数据对象 h5

var ff = document.getElementById('fm')
var fd = new FormData(ff) // 根据指定的表单制作表单数据对象(数据中有上传的附件信息)
// fd既有普通表单域信息，还有上传的文件信息
axios.post(url, fd)
```



### el-upload组件介绍

el-upload上传组件说明：

```html
<el-upload
  action="https://jsonplaceholder.typicode.com/posts/"  // 接收附件的服务器端地址
  :show-file-list="false" // 上传好的图片不要通过列表形式呈现
  :on-success="handleAvatarSuccess"  // 图片上传成功后的回调处理
  :http-request="httpRequest" // 自定义上传行为，有了此属性，那么 action 和 on-success 都成摆设了
>
  <img v-if="imageUrl" :src="imageUrl" class="avatar">
  <i v-else class="el-icon-plus avatar-uploader-icon"></i>
</el-upload>
```

> 上述el-upload上传图片组件内部给集成了ajax，请求方式为**post**，会自动带着被上传的附件到达服务器端存储，由于我们的api接口要求是 **patch**方式请求，故组件的默认请求不能使用，要通过 **http-request**自定义上传行为，其会覆盖默认行为，这样形式上 action和 on-success可以不定义，但是action属性是必须的，应用上留空即可



### 应用

`步骤`：

1. 应用el-upload组件标签

   ```html
   <div id="rt">
          <!--
             class="avatar-uploader" // 自定义组件样式
             action="https://jsonplaceholder.typicode.com/posts/" // 上传附件服务器端地址
             :show-file-list="false" // 图片是否是列表展示
             :on-success="handleAvatarSuccess" // 图片上传成功后的回调处理
             :before-upload="beforeAvatarUpload" // 图片上传前的回调处理
             :http-request="httpRequest" // 自定义上传行为，此时action和on-success无效了，action是必须项目，留空即可
           -->
           <el-upload
             action=""
             :show-file-list="false"
             :http-request="httpRequest"
           >
           <!--判断是否有图像并展示，否则展示+号-->
             <img v-if="accountForm.photo" :src="accountForm.photo" class="avatar" width="200" height="200">
             <i v-else class="el-icon-plus avatar-uploader-icon"></i>
           </el-upload>
   </div>
   ```
   
> 给el-upload声明http-request属性 并设置methods的httpRequest方法，表示自定义上传行为

2. 在methods中创建httpRequest()方法，实现上传

   ```js
   // 自定义上传头像行为
   // resource参数：是一个对象，里边有当前正在上传的图片信息(resource.file)
   httpRequest (resource) {
     // 1. FormData表单数据对象收集表单信息，即上传附件信息
     let fd = new FormData()
     // 把图片的信息添加给fd对象
     // fd.append(名称，值)
     fd.append('photo', resource.file) // 文件已经被fd保存好了
   
     // 2. axios带着附件到达服务器端存储
     let pro = this.$http.patch('/user/photo', fd)
     pro
       .then(result => {
         if (result.data.message === 'OK') {
           // 把服务器端返回的新的头像获得到，并更新给accountForm.photo成员里边
           // result.data.data.photo:头像完整请求地址信息
           this.accountForm.photo = result.data.data.photo
           this.$message.success('头像更新成功！')
         }
       })
       .catch(err => {
         return this.$message.error('头像更新失败：' + err)
       })
   },
   ```



### FormData回顾

FormData表单数据对象介绍

1.  FormData 是 Html5 新加进来的一个类,可以模拟表单数据 
2.  可以使用 JQuery 的 $.Ajax 结合 FormData 异步上传二进制文件 
3.  可以先通过 new 关键字创建一个空的 FormData 对象，然后使用 append() 方法向该对象里添加字段 
4.  也可以 new 的同时直接传入表单对象，从而创建有值的FormData对象 

FormData在普通表单域中的应用：

```html
<form id="upload" method="post" action="">
  <input type="text" name="username" value=""/>
  <input type="password" name="paw" value=""/>
  <input type="button" onclick="send()" value="提交"/>
</form>
```

```js
function send(){
  //获取一个form表单对象
  let fm = document.getElementById("upload");
  //用这个表单对象来初始化FormData对象
  let fd = new FormData(fm);
	// 现在fd里边已经拥有form表单里边全部的数据了，调用axios即可完成传递给服务器端功能
  axios.post(url, fd)
}
```

FormData传递上传文件

```js
  //创建一个空的FormData对象
  let fd = new FormData();
	// fd可以通过调用append()方法给自己添加成员信息
  // 语法：fd.append(name,value)
  // append():既可以添加普通表单域信息，也可以添加文件表单域信息
	fd.append(myfile,文件对象信息)
	// 通过axios把上传文件传递给服务器端
  axios.post(url, fd)
```

 

## 兄弟之间传值

给组件实例声明事件：

```html
<组件 @事件名称="事件驱动方法"></组件>
methods:
	事件驱动方法(形参，形参){}
```

还有一种方法就是通过**$on**进行声明：

```js
// 语法：
组件实例.$on(事件名称，事件驱动方法(形参，形参){})
// 例如：
// 声明事件
vm.$on('hello',function(traffic,city){console.log(`我坐着{$traffic}到达${city}城市`)})
// 触发事件执行
vm.$emit('hello','汽车','广州')  // 我坐着汽车到达广州城市
```

> 注意：组件实例  和 vue实例  都可以调用$on

$on铺垫，实现给组件实例声明事件方法,简单应用

```vue
<template>
    <div id="app">
      <h2>App根基组件(兄弟之间传值)</h2>
      <!--单击按钮，触发请求on设置的事件-->
      <button @click="$emit('hello','北京')">触发请求事件</button>
    </div>
</template>

<script>
export default {
  name: 'App',
  // 声明周期方法，及时把事件给声明好
  created () {
    // 给当前组件实例声明事件
    this.$on('hello', function (city) {
      console.log(`我已经到达${city}城市了`)
    })
  },
}
</script>

<style lang="less" scoped>
#app{
  width: 400px;
  height: 400px;
  border:2px solid blue;
}
</style>
```



实现步骤：

1. 定义模块 src/bus.js，内容就是**导入**Vue模块并**导出**一个Vue实例对象

   ```js
   import Vue from 'vue'
   export default new Vue() 
   ```

   

2. 在各个兄弟组件中，导入 bus.js 模块

   ```js
   import bus from '@/bus.js'
   ```

   > 虽然bus.js被各个组件都导入，但是系统中bus只有一份

3. 在**接收**数据的兄弟组件的 created 生命周期方法里(使得事件及时响应)，"大哥"的组件中声明

   使用 bus.$on('事件名称', (接收的数据) => {}) 定义事件成员方法

   ```js
   created(){
     // 定义事件,注意箭头函数应用
     bus.$on('xxx', data=>{
       console.log(data)
     })
   }
   ```

   > xxx是事件方法的名称
   >
   > data是形参，待接收数据，并且可以定义多个
   >
   > 注意：如果$on内部要使用this，请通过"**箭头函数**"声明方法

4. 在**发送**数据的兄弟组件中，使用 bus.$emit('事件名称', 要发送的数据) 来向外发送数据

   ```js
   <button @click="sendMsg">给兄弟说话</button>
   export default {
   
     methods: {
       sendMsg(){
         // 触发 绑定的 事件，并向外传递参数
         bus.$emit('xxx', '1000元保护费')
       }
     }
   }
   ```

   > xxx 是接收数据组件给bus声明的方法

> 第二个参数是传递的实参数据

`说明`：

1. Vue实例可以调用$on()方法进行事件方法创建

   ```js
   实例.$on(名称,(形参，形参，形参……){})
   ```

   > 参数根据需要，可以是一个或多个

2. Vue实例可以调用$emit()方法进行事件方法调用

   ```js
   实例.$emit(名称,实参，实参，实参……)
   ```
   
> 参数 与 $on的形参是一一对应的



src/bus.js代码：

```js
// 快递员，负责兄弟组件之间传递数据
import Vue from 'vue'
// 导出一个Vue对象
// 注意：这是一个新的对象，与main.js里边的没有关系
export default new Vue()
```

First.vue代码(created、$on设置事件方法，准备接受数据)：

```vue
<template>
    <div id="one">
      <h3>大哥组件</h3>
      <span>接收小弟的礼物：{{money}}</span>
    </div>
</template>

<script>
// 引入bus.js进来
import bus from '@/bus.js'

export default {
  name: 'One',
  // 在created中给bus绑定事件，时机最靠前，随时可以响应使用
  data () {
    return {
      // 接收小弟来到数据
      money: ''
    }
  },
  created () {
    // this:组件实例对象
    // 注意：设置为箭头函数
    bus.$on('receive', val => {
      // val：是其他应用处给传递的数据
      // 把获得的数据赋予money
      this.money = val
    })
  }
}
</script>

<style lang="less" scoped>
#one{
  width: 300px;
  height: 100px;
  border:1px solid red;
  margin-bottom:20px;
}
</style>
```

Second.vue代码(bus调用$emit()调动事件进行数据传递)：

```vue
<template>
    <div id="two">
      <h3>小弟组件</h3>
      <p>
        <button @click="say">给大哥说话</button>
      </p>
    </div>
</template>

<script>
// 引入bus.js进来
import bus from '@/bus.js'

export default {
  name: 'Two',
  methods: {
    // 实现给大哥传递数据的
    say () {
      // 让bus调用自己的事件
      bus.$emit('receive', '1000元保护费')
    }
  }
}
</script>

<style lang="less" scoped>
#two{
  width: 300px;
  height: 100px;
  border:1px solid greenyellow;
}
</style>
```

App.vue代码(引入、注册、使用各个兄弟组件)：

```vue
<template>
    <div id="app">
      <h2>App根基组件(兄弟之间传值)</h2>
      <!--使用两个兄弟组件-->
      <first-com></first-com>
      <second-com></second-com>
    </div>
</template>

<script>
// 对大哥、小弟两个组件做 引入、注册、使用
import FirstCom from '@/components/First.vue'
import SecondCom from '@/components/Second.vue'
export default {
  name: 'App',
  components: {
    FirstCom,
    SecondCom
  }
}
</script>

<style lang="less" scoped>
#app{
  width: 400px;
  height: 400px;
  border:2px solid blue;
}
</style>
```



## 子给父传递(回顾)

`步骤`：

1. 父组件 向子组件 传递一个事件

2. 子组件 调用 父组件 传递过来的事件，并传递相关的数据

3. 父组件 通过事件函数参数获得子组件传递过来的数据并使用



其中

​	func1为事件的名称，给子组件触发使用

​	show为该事件的执行函数，在父组件内部的methods中定义好

​	在事件中可以通过形参(arg1、arg2)接收子组件出来过来的数据 并做近一步处理



**`子组件操作`**：

子组件中，使用<font color=red>this.$emit()</font>调用 父组件中的方法

```js
this.$emit('func1', 数据, 数据)
this:当前子组件对象
$emit:通过这个关键字可以使得子组件可以调用 父组件 的事件
```

从第二个位置开始传递实参数据，其可以被父组件methods方法的形参所接受

$emit(名称，数据，数据……) 是组件调用自己方法的固定方式，第一个参数是被调用方法的名称，后续参数都是给方法传递的实参信息



案例应用：

子组件Son.vue   给  父组件App.vue 传递 ”**啤酒**“数据

Son.vue具体代码(通过$emit()调用父给声明的btn方法)：

```vue
<template>
    <div id="son">
      <h3>我是son子组件</h3>
      <p>
        <button @click="$emit('btn','啤酒')">给父传递数据</button>
      </p>
    </div>
</template>

<script>
export default {
  name: 'Son'
}
</script>

<style lang="less" scoped>
#son{
  width: 200px;
  height: 100px;
  border:1px solid orange;
}
</style>
```



App.vue代码(@声明事件，methods定义事件方法，drink接收数据)：

```vue
<template>
    <div id="app">
      <h2>App根组件(父组件)</h2>
      <span>子给老子传递的信息：{{drink}}</span>
      <!--使用子组件-->
      <!--@ 是子组件创建(自定义)事件-->
      <son-com @btn="buttonHandler"></son-com>
    </div>
</template>

<script>
// 对Son.vue做引入、注册、使用
import SonCom from '@/components/Son.vue'
export default {
  name: 'App',
  components: {
    SonCom
  },
  data () {
    return {
      // 接收子传递的数据
      drink: ''
    }
  },
  methods: {
    // 子组件事件方法声明
    // val:子给父传递的数据
    buttonHandler (val) {
      // 把信息赋予给drink
      this.drink = val
    }
  }
}
</script>

<style lang="less" scoped>
#app{
  width: 400px;
  height: 200px;
  border:2px solid blue;
}
</style>
```



# 同步更新账户信息

`步骤`：

1. 创建名称为  src/utils/bus.js  的组件文件

   ```js
   import Vue from 'vue'
   export default new Vue()
   ```
   
2. 在 账户account 和 首页home 的组件文件中对bus都做导入

   ```js
   // 导入公共bus的vue对象
   import bus from '@/utils/bus.js'
   ```
   
3. 在 首页home 组件中，为 用户名、头像 声明临时**data成员**，用于接收更新的账户信息

   ```js
   tmpname: '', // 临时账户名称
   tmpphoto: '', // 临时账户头像
   ```
   
4. 在 首页 home  组件中，给name和 photo的计算属性判断临时成员存在就直接用，否则在用sessionStorage的账户信息

   ```js
     computed: {
       name () {
         return this.tmpname || JSON.parse(window.sessionStorage.getItem('userinfo')).name
       },
       photo () {
         return this.tmpphoto || JSON.parse(window.sessionStorage.getItem('userinfo')).photo
       }
     },
   ```
   
> sessionStorage没有响应式，这样做可以模拟响应式
   
5. 在  首页home  的created生命周期中，bus对象 通过**$on**声明事件方法**upAccountName**和**upAccountPhoto**，以便让account的bus来调用进行数据更新

   ```js
     created () {
       // 1. 对  名称  进行更新
       bus.$on('upAccountName', nm => {
         // 更新sessionStorage中name的信息
         let userinfo = JSON.parse(window.sessionStorage.getItem('userinfo'))
         userinfo.name = nm
         window.sessionStorage.setItem('userinfo', JSON.stringify(userinfo))
         // 更新临时成员tmpname
         this.tmpname = nm
       })
       // 2. 对  名称  进行更新
       bus.$on('upAccountPhoto', ph => {
         // 更新sessionStorage中photo的信息
         let userinfo = JSON.parse(window.sessionStorage.getItem('userinfo'))
         userinfo.photo = ph
         window.sessionStorage.setItem('userinfo', JSON.stringify(userinfo))
         // 更新临时成员tmpphoto
         this.tmpphoto = ph
       })
     },
   ```
   
6. 在  账户account  组件中，当账户名称更新后，bus要通过**$emit**调用对应的方法(home组件给bus声明的)，实现  home 页面更新

   ```js
       // 账户名字更新
   		editAccount () {
         let pro = this.$http.patch('/user/profile', this.accountForm)
         pro
           .then(result => {
             // bus通过$emit调用自己的相关方法更新   首页home  的账户信息
             bus.$emit('upAccountName', result.data.data.name)
   ```
   
```js
    // 自定义上传用户头像逻辑
       httpRequest (res) {
         var fd = new FormData()
         fd.append('photo', res.file)
         let pro = this.$http.patch('/user/photo', fd)
         pro
           .then(result => {
             this.$message.success('上传头像成功')
           	// bus通过$emit调用自己的相关方法更新   首页home  的头像信息
             bus.$emit('upAccountPhoto', result.data.data.photo)
   ```



# 素材管理

`步骤`：

1. 创建组件：material/material.vue

   ```vue
   <template>
       <div>素材管理</div>
   </template>
   
   <script>
   export default {
     name: 'Material'
   }
   </script>
   
   <style lang="less" scoped>
   </style>
   ```
   
2. 创建路由：/materail

   ```js
   { path: '/material', 
     name: 'material', 
     component: () => import('@/views/material/material.vue') },
   ```
   

   
3. home里边创建导航：素材管理---->/material

   ```html
   <el-menu-item index="/material">素材管理</el-menu-item>
   ```
   



## 绘制素材列表结构

`步骤`：

1. 设置el-card卡片区 并 绘制静态的html图片列表展示素材图片示例结构(参考)

   ```html
   <template>
     <!--卡片区-->
     <el-card class="box-card">
       <!--命名插槽，头部内容设置-->
       <div slot="header" class="clearfix">
         <span>素材管理</span>
       </div>
       <!--匿名插槽，卡片主体内容-->
       <div class="text item">
         <ul>
           <li class="image-box" v-for="item in 20" :key="item">
             <img src="../../assets/logo.png" alt>
             <div class="image-bot">
               <el-button type="success" icon="el-icon-star-off" circle></el-button>
               <el-button type="danger" icon="el-icon-delete" circle></el-button>
             </div>
           </li>
         </ul>
       </div>
     </el-card>
   </template>
   ```
   

   
2. 给结构代码设置css样式(参考)

对应的css样式：

```css
// 素材图片列表样式
.image-box {
  list-style: none;
  width: 200px;
  height: 200px;
  background-color: #fff;
  margin: 10px;
  float: left;
  border: 1px solid #eee;
  img {
    width: 200px;
    height: 140px;
  }
  .image-bot {
    width: 200px;
    height: 60px;
    line-height: 60px;
    text-align: center;
  }
}
```



## 获取展示真实素材图片

步骤：

1. 创建data成员imageList，接收获取的图片列表信息

2. 创建data成员querycdt，设置获取图片列表的条件(collect:false/page:1/per_page:20)

   ```js
     data () {
       return {
         imageList: [], // 已有素材列表信息
         // 获得素材图片的条件信息
         querycdt: {
           collect: false,
           page: 1,
           per_page: 20
         }
       }
     }
   ```
   

   
3. 在methods中创建getImageList()方法，获取图片列表信息，并赋予给imageList

   ```js
      // 获取素材图片列表
       getImageList () {
         let pro = this.$http.get('/user/images', { params: this.querycdt })
         pro
           .then(result => {
             if (result.data.message === 'OK') {
               this.imageList = result.data.data.results
             }
           })
           .catch(err => {
             return this.$message.error('获得素材图片列表错误:' + err)
           })
       }
   ```
   

   
4. 在created钩子中对 getImageList()进行调用

   ```js
     created () {
       this.getImageList() // 获得文章列表
     },
   ```
   

   
5. 页面上要对imageList图片资源列表做遍历数据

   ```html
           <li class="image-box" v-for="item in imageList" :key="item.id">
             <img :src="item.url" alt>
   ```
   
> id 是图片的唯一标志
   >
   > url  是图片完整请求地址



## 上传素材图片实现

对el-upload组件的相关属性进行配置

对el-upload组件做第二次使用，并且要通过<font color=red>默认行为</font>上传素材图片

```html
<el-upload
           action="http://ttapi.research.itcast.cn/mp/v1_0/user/images"
           style="float: right; padding: 3px 0"
           :headers="setToken"
           name="image"
           :show-file-list="false"
           >
  <el-button size="small" type="primary">上传图片</el-button>
</el-upload>
```

> 注意：
>
> 1. 默认上传行为要执行自己的ajax，而服务器端处于认证考虑，要求我们传递token，这样还要给el-upload额外设置属性，具体为headers
>
> 2. 服务器端要求上传好的图片要通过“image”名称进行传递，默认是"file"名称，具体要通过name属性配置



`步骤`：

1. 应用上传图片组件

```html
  <!--卡片区-->
  <el-card class="box-card">
    <!--命名插槽，头部内容设置-->
    <div slot="header" class="clearfix">
      <span>素材管理</span>
      <!--
        默认上传动作
        1. action设置地址
        2. 需要传递token信息，通过headers属性设置
        3. 通过name属性设置被上传图片的传递名字,服务器端要求是image
        4. :show-file-list="false" 禁止形成列表效果
        5. on-success 文件上传成功后回调处理
      -->
      <el-upload
        style="float: right; padding: 3px 0"
        action="http://ttapi.research.itcast.cn/mp/v1_0/user/images"
        :headers="setToken"
        name="image"
        :show-file-list="false"
        :on-success="onSuccess"
      >
        <el-button size="small" type="primary">上传图片</el-button>
      </el-upload>
    </div>
```

2. 在computed计算属性中给上传ajax设置token

```js
  computed: {
    setToken () {
      let token = JSON.parse(window.sessionStorage.getItem('userinfo')).token
      return { Authorization: 'Bearer ' + token }
    }
  },
```

3. 在methods中制作onSuccess()方法，待图片上传做**提示**并刷新**显示**

   ```js
       // 素材上传完毕的回调处理
       onSuccess () {
         this.$message.success('图片上传成功！')
         this.getImageList() // 刷新图片
       },
   ```
   


# 发布文章封面处理

`步骤`：

1. 在添加文章 封面处绘制html标签代码

   在封面单选按钮组(el-radio-group)标签后边设置如下代码

   ```html
   <ul>
     <li class="uploadbox" v-for="item in 3" :key="item">
       <span>点击图标选择图片</span>
       <img v-if="addForm.cover.images[item-1]" :src="addForm.cover.images[item-1]" alt="" />
       <div v-else class="el-icon-picture-outline"></div>
     </li>
   </ul>
   ```
   
> addForm.cover.images[item-1]  是显示对应的封面图片效果，如果不做选择，默认是没有的
   

   
2. 绘制选择框对应的css样式(参考 项目笔记)

   ```css
   // 文章封面选择框样式
   .uploadbox {
     list-style: none;
     width: 200px;
     height: 200px;
     margin: 10px;
     float: left;
     cursor: pointer;
     border: 1px solid #eee;
     span {
       width: 200px;
       height: 50px;
       line-height: 50px;
       display: block;
       text-align: center;
     }
     div {
       width: 200px;
       height: 150px;
       font-size: 100px;
       display: flex;
       justify-content: center;
       align-items: center;
       background-color: #fff;
     }
     img{
       width: 200px;
       height: 150px;
     }
   }
   ```
   




## 选取框与单选按钮联系

`步骤`：

1. 通过computed设计covernum成员，

   该成员在type大于0情况下与type保持一致，其他情况都为0

```js
  computed: {
    // 设计当前图片"选择框"个数
    covernum () {
      if (this.addForm.cover.type > 0) {
        return this.addForm.cover.type
      }
      return 0
    }
  }
```

2. 模板中直接根据covernum做  选择框 显示

   ```html
   <li class="uploadbox" v-for="item in covernum" :key="item">
     <span>点击图标选择图片</span>
     <img v-if="addForm.cover.images[item-1]" :src="addForm.cover.images[item-1]" alt>
     <div v-else class="el-icon-picture-outline"></div>
   </li>
   ```
   


## 展示素材图片对话框

对话框组件el-dialog解读：

```html
<el-dialog
  title="提示"
  :visible.sync="dialogVisible"
  width="60%"
  >
  <!--匿名插槽体现-->
  <span>这是一段信息</span>
  <!--命名插槽体现-->
  <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>
</el-dialog>
```

> :visible.sync="true/false"  限制当前对话框 显示true或隐藏false
>
> width:设置对话框宽度



`展示对话框步骤`：

1. 添加文章组件中，与card卡片主体内容并列的后边绘制el-dialog组件内容

   ```html
   <el-dialog
              title="素材图片"
              :visible.sync="dialogVisible"
              width="60%"
              >
     <span>这是展示图片素材框框</span>
     <span slot="footer" class="dialog-footer">
       <el-button @click="dialogVisible = false">取 消</el-button>
       <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
     </span>
   </el-dialog>
   ```
   

   
2. data创建dialogVisible成员，默认值为false，控制是否开启对话框

   ```js
   dialogVisible: false, // 素材对话框是否启用
   ```
   

   
3. 给“选择框”的li标签设置事件 @click="showDialog()"

   ```html
   <li class="uploadbox" v-for="item in covernum" :key="item" 
       @click="showDialog()">
   ```
   

   
4. 在methods里边创建showDialog()方法，展示对话框

   ```js
       // 展示对话框逻辑
       showDialog () {
         this.dialogVisible = true // 打开dialog对话框
       },
   ```
   



## 展示素材图片列表

`步骤`：

1. 创建data成员 imageList,用于接收图片列表信息

2. 创建data成员 querycdt(collect:false/page:1/per_page:12) 设定获取图片列表的条件

   ```js
   	imageList: [], // 素材图片列表
     // 获取素材图片的条件参数
     querycdt: {
       collect: false, // 非收藏图片
       page: 1,
       per_page: 12
     },
   ```
   

   
3. 给methods创建 getImageList()方法，获取真实图片信息，完毕赋予给 imageList

   ```js
   // 获取素材图片列表
   getImageList () {
     let pro = this.$http.get('/user/images', { params: this.querycdt })
     pro
       .then(result => {
         if (result.data.message === 'OK') {
           this.imageList = result.data.data.results
         }
       })
       .catch(err => {
         return this.$message.error('获得素材图片列表错误:' + err)
       })
   },
   ```
   
4. 在created中调用 getImageList()方法 获取真实图片展示

   ```js
     created () {
       this.getImageList() // 获得供选取的素材图片
     },
   ```
   

   
5. 在dialog对话框中  绘制图片列表展示的相关html代码

   ```html
   <el-dialog title="素材图片" :visible.sync="dialogVisible" width="60%" @close="clearImage">
     <!--后添加的用于展示素材图片的标签-->
     <ul>
       <li class="image-box" v-for="item in imageList" :key="item.id">
         <img :src="item.url" alt="没有图片">
       </li>
     </ul>
     <span slot="footer" class="dialog-footer">
       <el-button @click="dialogVisible = false">取 消</el-button>
       <el-button type="primary" @click="imageOK">确 定</el-button>
     </span>
   </el-dialog>
   ```
   
> 通过 ul/li/img 标签对imageList素材图片做遍历展示
   

   
6. 绘制图片列表展示的相关html代码对应的css样式

   ```css
   // 对话框素材图片列表相关css样式
   .image-box {
     list-style: none;
     width: 200px;
     height: 140px;
     background-color: #fff;
     margin: 10px;
     float: left;
     border: 1px solid #eee;
     cursor:pointer;
     box-sizing:border-box;
     img {
       width: 100%;
       height: 100%;
     }
   }
   ```
   



## 选中素材图片高亮设置

`步骤`：

1. 给素材图片img标签设置@click="clkImage"事件

   ```html
         <ul>
           <li class="image-box" v-for="item in imageList" :key="item.id">
             <img :src="item.url" alt="没有图片" @click="clkImage" >
           </li>
         </ul>
   ```
   
> 注意 clkImage后边没有括号
   
2. 在methods中 定义  clkImage事件方法设置选中项目的语法高亮标志

   ```js
       // 素材图片被选中，设置高亮标志
       clkImage (evt) {
         // 其他项目要做清除border操作
         let lis = document.querySelectorAll('.image-box')
         for (var i = 0; i < lis.length; i++) {
           lis[i].style.border = ''
         }
         // console.log(evt) // MouseEvent 鼠标事件对象
         // evt.target // 被点击图片(img)的dom对象
         // evt.target.parentNode // 找到img的父级，即li标签
         // 给li设置border边框，高亮效果
         evt.target.parentNode.style.border = '4px solid red'
       },
   ```

   

2. 给选择框单击事件传递序号信息  @click="showDialog(item)"

   ```html
   <li class="uploadbox" v-for="item in covernum" :key="item" 
       @click="showDialog(item)">
   ```
   
> 把遍历的item当做序号传递给事件方法，值是从1开始的，接收后要做-1减一操作
   
3. methods方法 showDialog()中要接收序号并赋予给xu成员，注意要减一操作

   ```js
       // 展示对话框逻辑
       // n：代表第n个选择框被单击到了(值为1/2/3)
       showDialog (n) {
         // 更新xu成员
         this.xu = n - 1
         this.dialogVisible = true // 开启对话框
       },
   ```

## 记录选中的图片

`步骤`：

1. 给data声明 materialUrl成员

```js
   materialUrl: '', // 选中的素材图片的路径名地址信息
```

2. 在clkImage方法中，把当前被单击选中的img标签的src属性值赋予给materialUrl成员

   ```js
       // 素材图片选取操作
       clkImage (evt) {
         let lis = document.querySelectorAll('.image-box')
         for (var i = 0; i < lis.length; i++) {
           lis[i].style.border = ''
         }
         evt.target.parentNode.style.border = '3px solid red'
         // 把当前选中图片的src地址信息赋予给meterialUrl成员
         this.materialUrl = evt.target.src
       },
   ```
   


## 确定选取素材图片

`步骤`：

1. 给对话框**确定按钮**设置事件  @click="imageOK"

   ```html
   <el-button type="primary" @click="imageOK">确 定</el-button>
   ```
   

   
2. 在methods方法中声明imageOK,并把选择好的图片地址materialUrl赋予给添加文章表单的成员 

   ```js
   // 素材图片选取好，点击“对话框”确定按钮后，记录素材图片
   imageOK () {
     if (this.materialUrl) {
    // 给添加文章的表单域成员cover.image增加素材图片请求地址信息
       this.addForm.cover.images[this.xu] = this.materialUrl
       this.dialogVisible = false // 关闭对话框
     } else {
       this.$message.error('咋地，不挑一个再走啊')
     }
   },
   ```

`注意`：

​	如果用户没有选择图片，那么单击确定按钮式没有动作的，相反要提示“咋地，不挑一个再走啊”



## 后续优化

在对话框中选中一个图片，但是没有单击”确定“按钮就把对话框关闭了，此时再次打开对话框，发现之前选中的图片还是选中状态，并且materialUrl也是保存上一次选中图片的路径名信息，这样做不合适，设计一个清除操作，每次打开对话框都是一个初始化状态。

步骤：

1. 制作一个methods方法，清除之前选择素材图片的痕迹

   ```js
       // 清除之前选择素材图片的痕迹(边框高亮、图片路径名)
       clearImage () {
         let lis = document.querySelectorAll('.image-box')
         for (var i = 0; i < lis.length; i++) {
           lis[i].style.border = ''
         }
         this.materialUrl = '' // 清除图片路径名
       },
   ```
   

   
2. 素材选中 后要调用**clearImage**方法，使得之前选取的标记被清除

   ```js
       // 素材图片选取操作
       clkImage (evt) {
         // 清除之前选择图片的状态信息
         this.clearImage()
         evt.target.parentNode.style.border = '3px solid red'
         // 把当前选中图片的src地址信息赋予给meterialUrl成员
         this.materialUrl = evt.target.src
       },
   ```
   

   
3. 给el-dialog设置@close="clearImage" 事件, 使得任何 方式关闭对话框，都会对已经选取素材的状态进行清除

   ```html
   <el-dialog title="素材图片" :visible.sync="dialogVisible" width="60%" 
              @close="clearImage">
   ```
   


## [vue-resource 实现 get, post, jsonp请求](https://github.com/pagekit/vue-resource)

除了 vue-resource 之外，还可以使用 `axios` 的第三方包实现实现数据的请求

1. 之前的学习中，如何发起数据请求？
2. 常见的数据请求类型？  get  post jsonp
3. 测试的URL请求资源地址：

 + get请求地址： http://vue.studyit.io/api/getlunbo
 + post请求地址：http://vue.studyit.io/api/post
 + jsonp请求地址：http://vue.studyit.io/api/jsonp

4. JSONP的实现原理

 + 由于浏览器的安全性限制，不允许AJAX访问 协议不同、域名不同、端口号不同的 数据接口，浏览器认为这种访问不安全；
 + 可以通过动态创建script标签的形式，把script标签的src属性，指向数据接口的地址，因为script标签不存在跨域限制，这种数据获取方式，称作JSONP（注意：根据JSONP的实现原理，知晓，JSONP只支持Get请求）；
 + 具体实现过程：

  - 先在客户端定义一个回调方法，预定义对数据的操作；
  - 再把这个回调方法的名称，通过URL传参的形式，提交到服务器的数据接口；
  - 服务器数据接口组织好要发送给客户端的数据，再拿着客户端传递过来的回调方法名称，拼接出一个调用这个方法的字符串，发送给客户端去解析执行；
  - 客户端拿到服务器返回的字符串之后，当作Script脚本去解析执行，这样就能够拿到JSONP的数据了；

 + 带大家通过 Node.js ，来手动实现一个JSONP的请求例子；

 ```
    const http = require('http');
    // 导入解析 URL 地址的核心模块
    const urlModule = require('url');

    const server = http.createServer();
    // 监听 服务器的 request 请求事件，处理每个请求
    server.on('request', (req, res) => {
      const url = req.url;

      // 解析客户端请求的URL地址
      var info = urlModule.parse(url, true);

      // 如果请求的 URL 地址是 /getjsonp ，则表示要获取JSONP类型的数据
      if (info.pathname === '/getjsonp') {
        // 获取客户端指定的回调函数的名称
        var cbName = info.query.callback;
        // 手动拼接要返回给客户端的数据对象
        var data = {
          name: 'zs',
          age: 22,
          gender: '男',
          hobby: ['吃饭', '睡觉', '运动']
        }
        // 拼接出一个方法的调用，在调用这个方法的时候，把要发送给客户端的数据，序列化为字符串，作为参数传递给这个调用的方法：
        var result = `${cbName}(${JSON.stringify(data)})`;
        // 将拼接好的方法的调用，返回给客户端去解析执行
        res.end(result);
      } else {
        res.end('404');
      }
    });

    server.listen(3000, () => {
      console.log('server running at http://127.0.0.1:3000');
    });
 ```

5. vue-resource 的配置步骤：

 + 直接在页面中，通过`script`标签，引入 `vue-resource` 的脚本文件；
 + 注意：引用的先后顺序是：先引用 `Vue` 的脚本文件，再引用 `vue-resource` 的脚本文件；

6. 发送get请求：

```
getInfo() { // get 方式获取数据
  this.$http.get('http://127.0.0.1:8899/api/getlunbo').then(res => {
    console.log(res.body);
  })
}
```

7. 发送post请求：

```
postInfo() {
  var url = 'http://127.0.0.1:8899/api/post';
  // post 方法接收三个参数：
  // 参数1： 要请求的URL地址
  // 参数2： 要发送的数据对象
  // 参数3： 指定post提交的编码类型为 application/x-www-form-urlencoded
  this.$http.post(url, { name: 'zs' }, { emulateJSON: true }).then(res => {
    console.log(res.body);
  });
}
```

8. 发送JSONP请求获取数据：

```
jsonpInfo() { // JSONP形式从服务器获取数据
  var url = 'http://127.0.0.1:8899/api/jsonp';
  this.$http.jsonp(url).then(res => {
    console.log(res.body);
  });
}
```

## 配置本地数据库和数据接口API

1. 先解压安装 `PHPStudy`;
2. 解压安装 `Navicat` 这个数据库可视化工具，并激活；
3. 打开 `Navicat` 工具，新建空白数据库，名为 `dtcmsdb4`;
4. 双击新建的数据库，连接上这个空白数据库，在新建的数据库上`右键` -> `运行SQL文件`，选择并执行 `dtcmsdb4.sql` 这个数据库脚本文件；如果执行不报错，则数据库导入完成；
5. 进入文件夹 `vuecms3_nodejsapi` 内部，执行 `npm i` 安装所有的依赖项；
6. 先确保本机安装了 `nodemon`, 没有安装，则运行 `npm i nodemon -g` 进行全局安装，安装完毕后，进入到 `vuecms3_nodejsapi`目录 -> `src`目录 -> 双击运行 `start.bat`
7. 如果API启动失败，请检查 PHPStudy 是否正常开启，同时，检查 `app.js` 中第 `14行` 中数据库连接配置字符串是否正确；PHPStudy 中默认的 用户名是root，默认的密码也是root



## [Vue中的动画](https://cn.vuejs.org/v2/guide/transitions.html)

为什么要有动画：动画能够提高用户的体验，帮助用户更好的理解页面中的功能；

### 使用过渡类名

1. HTML结构：

```
<div id="app">
    <input type="button" value="动起来" @click="myAnimate">
    <!-- 使用 transition 将需要过渡的元素包裹起来 -->
    <transition name="fade">
      <div v-show="isshow">动画哦</div>
    </transition>
  </div>
```

2. VM 实例：

```
// 创建 Vue 实例，得到 ViewModel
var vm = new Vue({
  el: '#app',
  data: {
    isshow: false
  },
  methods: {
    myAnimate() {
      this.isshow = !this.isshow;
    }
  }
});
```

3. 定义两组类样式：

```
/* 定义进入和离开时候的过渡状态 */
    .fade-enter-active,
    .fade-leave-active {
      transition: all 0.2s ease;
      position: absolute;
    }

    /* 定义进入过渡的开始状态 和 离开过渡的结束状态 */
    .fade-enter,
    .fade-leave-to {
      opacity: 0;
      transform: translateX(100px);
    }
```

### [使用第三方 CSS 动画库](https://cn.vuejs.org/v2/guide/transitions.html#自定义过渡类名)

1. 导入动画类库：

```
<link rel="stylesheet" type="text/css" href="./lib/animate.css">
```

2. 定义 transition 及属性：

```
<transition
	enter-active-class="fadeInRight"
    leave-active-class="fadeOutRight"
    :duration="{ enter: 500, leave: 800 }">
  	<div class="animated" v-show="isshow">动画哦</div>
</transition>
```

### 使用动画钩子函数

1. 定义 transition 组件以及三个钩子函数：

```
<div id="app">
    <input type="button" value="切换动画" @click="isshow = !isshow">
    <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter">
      <div v-if="isshow" class="show">OK</div>
    </transition>
  </div>
```

2. 定义三个 methods 钩子方法：

```
methods: {
        beforeEnter(el) { // 动画进入之前的回调
          el.style.transform = 'translateX(500px)';
        },
        enter(el, done) { // 动画进入完成时候的回调
          el.offsetWidth;
          el.style.transform = 'translateX(0px)';
          done();
        },
        afterEnter(el) { // 动画进入完成之后的回调
          this.isshow = !this.isshow;
        }
      }
```

3. 定义动画过渡时长和样式：

```
.show{
      transition: all 0.4s ease;
    }
```


### [v-for 的列表过渡](https://cn.vuejs.org/v2/guide/transitions.html#列表的进入和离开过渡)

1. 定义过渡样式：

```
<style>
    .list-enter,
    .list-leave-to {
      opacity: 0;
      transform: translateY(10px);
    }
    .list-enter-active,
    .list-leave-active {
      transition: all 0.3s ease;
    }
</style>
```

2. 定义DOM结构，其中，需要使用 transition-group 组件把v-for循环的列表包裹起来：

```
  <div id="app">
    <input type="text" v-model="txt" @keyup.enter="add">

    <transition-group tag="ul" name="list">
      <li v-for="(item, i) in list" :key="i">{{item}}</li>
    </transition-group>
  </div>
```

3. 定义 VM中的结构：

```
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        txt: '',
        list: [1, 2, 3, 4]
      },
      methods: {
        add() {
          this.list.push(this.txt);
          this.txt = '';
        }
      }
    });
```


### 列表的排序过渡

`<transition-group>` 组件还有一个特殊之处。不仅可以进入和离开动画，**还可以改变定位**。要使用这个新功能只需了解新增的 `v-move` 特性，**它会在元素的改变定位的过程中应用**。

+ `v-move` 和 `v-leave-active` 结合使用，能够让列表的过渡更加平缓柔和：

```
.v-move{
  transition: all 0.8s ease;
}
.v-leave-active{
  position: absolute;
}
```

### webpack配置

[官网参考](https://cli.vuejs.org/zh/config/#lintonsave)

在项目根目录新建`vue.config.js`文件，内容设置结构为如下：

> vue-cli脚手架创建项目主结构文件，webpack配置文件名字就是vue.config.js，与默认的名字(webpack.config.js)不一样

```javascript
module.exports = {
  具体配置信息
}
```

> 在根目录通过终端执行如下指令，可以看到webpack的大概配置信息，可以根据需要灵活配置
>
> vue inspect > output.js				// 查看全部webpack配置信息

webpack和webpack-dev-server在脚手架创建的项目里边已经被**封装**了，具体可以通过如下路径名找到

[node_modules\@vue\cli-service\lib\commands\serve.js]()



# Plugin插件

应用中会看到这样的语句：  Vue.use(xxx) ，专业称谓是“Plugin插件”

意思是：

​	Vue引入一个功能模块 (例如ElementUI 或 Vuex)，这个模块打比方有10个组件，现在全部都要注册给Vue，传统方式要执行10次  Vue.component()  这样的语句，工作繁琐、效率低下，现在执行一次  Vue.use() 就可以搞定



定义插件语法：

```js
export default = {
  install(vm,options){
    // 1. 添加全局方法或属性
    vm.xxx = function () {}
    vm.xxx = yyy

    // 2. 添加指令
    vm.directive('my-directive', {
      inserted (el) {}
    })

    // 3. 过滤器
    vm.filter(xxx,function(){})

    // 4. 添加实例方法
    vm.prototype.$myMethod = yyy

    // 5. 添加组件
    vm.component(xxx,yyy)
  }
}
```

> 插件需要对外提供install方法
>
> vm：固定参数(不需要传递)，代表 “Vue实例” 对象，名称可以自定义
>
> options：给插件传递的参数，根据需要使用，例如 Vue.use(插件名称，参数)
>
> plugin插件  可以注册的内容很多，具体有：
>
> methods方法、data成员、directive指令、过滤器、组件、实例方法Vue.prototype等等



目标1:

通过插件一次性完成两个组件的注册

```js
// src/utils/many.js
import one from '@/components/one'
import two from '@/components/one'

export default {
  install(vm){
    vm.component('com-one',one)
    vm.component('com-two',two)
  }
}
```

引入注册：

```js
// src/main.js
import many from '@/utils/many'
Vue.use(many)
```

使用

```html
<!--src/App.vue-->
<com-one></com-one>
<com-two></com-two>
```



目标2:

通过插件  把axios注册成为Vue实例的成员

```js
// src/utils/axios.js
import axios from 'axios'

export default {
  install(Vue){
    Vue.prototype.$http = axios
  }
}

```

引入注册：

```js
// src/main.js
import axios from '@/utils/axios'
Vue.use(axios)
```

使用

```js
this.$http.get(xxx)
```



# watch监听器

vue的data数据部分可以被监听，数据一旦发生变化马上可以感知到，并做相关处理

watch 监听的特点：监听到某个数据的变化后，侧重于**做某件事情**；

只要被监听的数据发生了变化，会自动触发 watch 中指定的处理函数；

语法：

```js
data(){
  return {
    name:'',
    addr:'',
    cat:{
      leg:'',
      tail:''
    }
  }  
}
```

 

```js
watch:{
	data成员名称: 函数(变化后的值，变化前的值){}
  name:function(newval,oldval){},
  addr:function(newval,oldval){},
  'cat.leg':function(newval,oldval){},
  'cat.tail':function(){}
}
```

> 简单字符串成员可以监听，例如name、addr，复杂的对象，但是需要通过**点**连接被监听的成员(例如cat.leg和cat.tail)，并且要通过**引号**圈选



案例：

添加用户的  密码 的长度检测

密码长度小于8个字符为<span style="color:green">绿色</span>；大于等于8个字符字体为<span style="color:red;">红色</span>；

1. 给密码输入框组件设置ref属性

   这样通过**this.$refs.xxx**的方式可以找到

2. 设置监听器

   ![1562141203682](Image\img(online)/1562141203682.png)

   > getInput() 作用：使得组件找到内部的input对应的dom节点，进而控制css样式



## 相关文章

2. [npm](https://www.npmjs.com/)
3. [饿了么组件库](http://element-cn.eleme.io/#/zh-CN)
4. [webpack打包](https://webpack.docschina.org/)
5. [babel下一代javascript编译器](https://babel.docschina.org/)
6. [bootcdn免费提供静态内容支持](https://www.bootcdn.cn/)
7. [鸟哥帮助官网](http://www.runoob.com)
8. [JavaScript 指南](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide)
9. [印记中文(深入挖掘国外前端新领域，为中国 Web 前端开发人员提供优质文档！)](https://docschina.org/)
10. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)
11. [Vue开源项目汇总](https://github.com/opendigg/awesome-github-vue)
12. [Vuejs中文社区](https://www.vue-js.com)
13. [JavaScript Standard Style代码规范](https://standardjs.com/)

1. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
2. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)
3. [pagekit/vue-resource](https://github.com/pagekit/vue-resource)
4. [navicat如何导入sql文件和导出sql文件](https://jingyan.baidu.com/article/a65957f4976aad24e67f9b9b.html)
5. [贝塞尔在线生成器](http://cubic-bezier.com/#.4,-0.3,1,.33)
6. [Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN) 