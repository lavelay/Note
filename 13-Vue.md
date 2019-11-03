vue-介绍

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

vue“单击”事件参数的3种类型：

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



### vue指令-v-if&v-else

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



### 品牌管理-搭建服务器端项目

项目运行中：

- 客户端负责数据的**展示**
- 服务器端负责数据的**提供**
- axios是<font color=red>搬运工</font>，负责在 客户端 和 服务器端 传输数据



为了使得学习效果更好，现在统一设置`后端项目`

`步骤`：

1. 把后端的全部代码文件解压到桌面指定目录

   ![1561016785365](Image/img(online)/1561016785365.png)

2. 启动mysql

   ![1554629441784](Image/img(online)/2-1554629441784.png)

3. 创建数据库相关

   新建数据库：

   ![1561016897179](Image/img(online)/1561016897179.png)

   给数据库导入数据：

   ![1561016973984](Image/img(online)/1561016973984.png)

   ![1561016949657](Image/img(online)/1561016949657.png)

   数据导入成功：

   ![1561017013901](Image/img(online)/1561017013901.png)

4. 给项目配置数据库信息

   在src/app.js文件中根据实际情况配置 数据库用户名、密码、数据库名称

   ![1561017218181](Image/img(online)/1561017218181.png)

5. 给项目安装全部依赖包

   在**server**目录下运行 npm install

   ```
   npm install
   ```

   ![1561017337257](Image/img(online)/1561017337257.png)

   

6. 运行项目

   在**server/src**目录下运行 node app.js

   ```
   node app.js
   ```

   ![1561017520017](Image/img(online)/1561017520017.png)



## Promise

它是一个对象，是用来处理**异步**操作的，可以让我们写异步调用的时候写起来更加优雅，更加美观便于阅读。

`Promise的三种状态`：

1. pending（进行中

2. resolved（完成）

3. rejected（失败） 

异步：在同一个时间中，可以发送**多个**进行执行

同步：在同一个时间点，只有**一个**进程在执行

`作用`：

1. 解决了异步调用彼此嵌套的**回调地狱**问题
2. 解决了多个异步过程**顺序执行**问题



## xios-拦截器-interceptors

axios在客户端与服务端之间传递数据时候是有**时间消耗**的

网络好、服务器比较空闲，axios的执行速度快

网络不好、服务器比较繁忙，axios的执行速度慢(这时用户需要多等待)

axios无论执行速度快还是慢，用户都需要等待，如果在axios执行时页面给予一定的**提示**，那么用户体验就比较好，这时候[拦截器]()就可以应用上



![](Image/img(online)/2-4-444.png)

`什么是`：

​	拦截器是axios向服务器端发送**请求**和**响应**回来所经历的两道关口



axios本身有两种拦截器：[请求拦截]()、[响应拦截]()

- 请求拦截器：

​	axios每次<font color=red>开始</font>请求的时候先执行此处逻辑，在这个地方可以给axios做出发前的配置，也可以做出发前的检查工作，检查ok的情况下就开始向服务器端发请求

- 响应拦截器：

​	axios<font color=red>完成</font>与服务器端交互回到客户端后就执行此处逻辑，在这个地方可以做一些后续收尾事宜，例如判断axios请求是否成功，或相关数据过滤操作



拦截器关键字：interceptors



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

> 把以上拦截器代码设置好，那么axios"所有"的请求就都会执行了



### 加载等待案例效果

`步骤`：

1. 通过img标签显示加载图片，同时设置v-show="showflag" 控制是否显示
2. 在data中声明showflag:false 信息，控制图片显示
3. 在created生命周期函数中配置  请求、响应 拦截器



`代码`：

```html
<div class="showhead">
    <h2>品牌案例管理</h2>
    <img src="./loading.gif" alt="" v-show="showflag" >  
</div>
```

Vue实例相关代码：

```js
data:{
  showflag:false, // 控制等待图片是否显示
  ……
},
// 生命周期
created() {
  // 请求拦截器
  axios.interceptors.request.use(
    config => {
      // Do something before request is sent
      // 加载图片显示
      this.showflag = true;
      return config;
    },
    error => {
      // Do something with request error
      return Promise.reject(error);
    }
  );

  // 响应拦截器
  axios.interceptors.response.use(
    response=> {
      // Do something with response data
      // 加载图片隐藏
      this.showflag = false;
      return response;
    },
    error=> {
      // Do something with response error
      return Promise.reject(error);
    }
  );
	// 要在拦截器之后请求如下方法
  this.getBrandsList(); // 获得品牌列表数据
},
```



`注意`：

1. 各个拦截器的第一个函数参数需要设置为 “**箭头函数**” ，使得内部this与外部保持一致，都是Vue实例
2. 各个拦截器需要设置在created中，因为需要**第1时间**就操控data成员showflag，再者可以使得各个拦截器被“自动”执行
3. 注意保持一个created



### 细节说明

`目标`：

​	知道config参数 和 Promise.reject(error) 分别代表的意思

```js
// 请求拦截器
axios.interceptors.request.use(function (config) {
  // 放置业务逻辑代码
  return config;
}, function (error) {
  // axios发生错误的处理
  return Promise.reject(error);
});

// 响应拦截器

axios.interceptors.response.use(function (response) {
    // Do something with response data
    return response;
  }, function (error) {
    // Do something with response error
    return Promise.reject(error);
  });
```

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



### 私有组件语法

`目标`：

​	知道私有组件的语法规则



`声明私有组件语法`：

```js
new Vue({
  components:{
    '组件的名称': { 配置对象成员 }, 
    '组件的名称': { 配置对象成员 }...
  },
})
```

例如：

```js
components:{
  'my-page',{
    template:`
      <ul>
        <li>上一页</li>
        <li>[1]</li>
        <li>2</li>
        <li>[3]</li>
        <li>下一页</li>
      </ul>
      `,
  }
}
```

`注意`：

1. template是组件的成员之一，还有其它成员
2. template设置的各个html标签需要有<font color=red>唯一的根元素</font>节点，上例为ul

3. 组件名称建议是 xx-yy 的格式



`使用组件语法`：

```html
<组件名称></组件名称>
```

> 组件形式上 就是html标签



`案例应用代码`：

制作一个分页组件并使用

```html
<div id="app">
  <!--使用组件-->
  <com-page></com-page>
</div>

<script src="./vue.js"></script>

<script>
  var vm = new Vue({
    // 声明私有组件
    components:{
      // 组件名称:{配置对象成员}
      'com-page':{
        // template: 设置组件拥有的html标签内容
        template:`
          <ul>
            <li><a href="#">1</a></li>
            <li><a href="#">2</a></li>
            <li><a href="#">3</a></li>
          </ul>
        `
      }
    },
    el:'#app',
    data:{
    },
    methods:{
    }
   });
</script>
```



### 相关成员

可以认为**组件**是特殊的**Vue实例**，拥有着与Vue实例大致相同的**成员**

例如  **data**、**methods**、**filters**、**directives**、**created**等等成员在组件内部都可以设置



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



`组件与Vue实例异同`：

1. 组件中的 data 必须是一个 **function** 并 return 一个 字面量对象
   (Vue 实例的 data 可以是 字面量对象，也可以是 function/return形式，前者推荐使用)
2. 组件中直接通过 template 属性来指定组件的UI结构
   Vue 实例中，一般通过 el 属性来指定渲染的容器，当然也可以使用template
3. 组件和Vue实例拥有类似的成员，都有自己的生命周期函数，过滤器，methods、data等成员





### 全局组件语法

`目标`：

​	了解全局组件创建的语法



`全局组件语法`：

```
Vue.component(名称,{配置对象成员})

new Vue()
```



`注意`：

​	全局组件需要在new Vue之前设置



### 小结

1. 组件是拥有一定功能多个html标签的**集合体**
2. 组件根据定义类型分为 **全局**/**私有** 组件
3. 组件是特殊的Vue实例，与Vue实例拥有着基本相同的成员(methods/created/data/template等)
4. template都必须有一个**根元素节点**
5. data的值需要是function/return形式



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

yarn较比npm装包更快，界面体验更好(安装进度条提示)



`注意`：

1. yarn安装完毕后要配置镜像源为taobao，否则优势发挥不出来
2. yarn全局方式装包要设置  global  关键字，而npm是 -g



## VueCLI

`什么是`

答：是脚手架，其可以把许多项目**通用的依赖包**(vue、webpack、路由、vuex、less编译器等等) 和 **通用的配置**都给做好安装好，使得开发者全部的注意力都集中在业务层面，明显提升开发效率的，真实项目都要使用脚手架开发。

依赖包：axios、vue等等都是依赖包，一个依赖包中有许多 模块



### 安装

`目标`：

​	能够安装和使用vuecli



`安装vuecli`：

```bash
######## yarn global add @vue/cli  // 弃用
npm i -g @vue/cli   // 使用该方式安装
```

> 上述依赖包通过全局方式安装，完毕后在系统任何目录都会执行名称为"vue"的一个指令

> 依赖包安装完毕，会形成 在 C:\Users\ssh\AppData\Roaming\npm\node_modules\@vue\cli 目录

> vue --version  查看脚手架版本，现在默认是4.0.5版本(如果是2.9.6就是错误的，需要卸载重新安装)



`vuecli创建项目`：

```bash
vue  create  项目名称(01-pro)
```



`注意`：

1. npm全局方式安装依赖包关键字是-g，而yarn全局装包关键字为global

2. vuecli创建新项目时，项目名称需要是一个**新目录**，完毕后会自动生产之，并在其中生成项目需要的文件

3. 项目(01-pro)上级各个目录名字最好为**英文** 或 **数字** 或 **中横线** 不要设置 中文的

   > 例如 E:\Vue86-87\87\87everyday\04day\01-pro  就是项目ok的各个目录体现



### 创建项目结构文件

`目标`：

​	利用vuecli创建自己的第一个项目



`步骤`：

​	运行以下命令来创建一个新项目，位置随意，但是各个上级目录最好都是英文的，my-project是项目名称，也是项目目录，不要提前创建

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



创建好的项目效果

![1561623844071](Image/img(online)/1561623844071.png)



`注意`：

​	c:/用户/ssh/.vuerc文件被删除作用

1. 创建项目选取配置的小项目被清除了
2. 项目创建过程中会提示要求选取 yarn  或  npm  方式下载包

​	创建项目过程中需要安装许多依赖包，建议通过yarn方式安装，如果不是，可以删除 “ c:\用户\用户名\.vuerc  ”  文件后再重新执行 "vue  create  xxx"命令，此时会提示选取



### 结构文件说明

`目标`：

​	了解项目的各个文件作用

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

   

2. 修改public/index.html文件，使用Vue实例的data数据

   ```html
       <div id="app">
         {{ msg }}
       </div>
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

`什么是`：

项目中一些**程序代码**经常被其他业务场景使用，为了避免重复开发，就把这些代码设置为**共享模式**，共享模式就是**模块化**。像jquery、axios、vue等等都是模块化的体现，需要的时候直接拿过来用即可 

![1566000527767](Image/img(online)/1566000527767.png)





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



`注意`：

​	重点掌握两种  ES6 和 CommonJS



### 默认导出和导入

`什么是默认导出和导入`：

数据提供者称为 导出

数据使用者称为 导入

在一个js文件中，通过一个**对象**把全部的数据导出出去，就是**默认导出**

对默认导出的成员进行接收就是默认导入



`模块`：

一个js文件就是一个模块，前提是该文件有做**导出**动作



`导出语法`：

```js
// 导出：
export default  对象
```

`导入语法`：

```js
// 导入：
import 名称  from  模块文件名字
```



`注意`：

1. 一个模块中 默认导出 只能进行**一次**
2. es6模块化现在只可以在VueCli项目中使用



`示意案例`：

01-默认导出.js

```js
// 默认导出
const a = 10
const b = 20

var cat = {name:'kitty',age:4}

export default cat  // 与 module.exports = cat 相当
```



main.js导入

```js
// 1) 默认导入
// import  对象  from  '模块'
import obj from './modules/01-默认导出.js'
console.log(obj)
```



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



`案例`：

对按需导出、导入进行简单使用

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

`目标`：

​	掌握 默认和按需 同时导出、导入技术



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



`案例`：

对默认和按需同时导出和导入做简单应用

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



使用示例：

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



### 小结

小结：

1. 导出，就是共享内容**提供方**
2. 导入，就是共享内容**使用者**
3. **默认导出**就是通过一个对象把全部的内容都提供出来 export default 对象
4. **按需导出**就是需要哪个信息就导哪个出来，不需要的不操作(常量和函数适合按需导出)  export const a = 10
5. 按需导出导入的相关元素：常量、函数、对象
6. 一个模块只能做**一次默认**导出，但是可以做**多次按需**导出



作业：

1. 给品牌管理案例实现**拦截器**加载图片效果

2. 练习，vuecli脚手架安装、创建项目出来、配置项目运行

3. 制作一个table表格组件，要求可以实现如下表格(4行3列)，其中数据部分来自data定义

   | 序号 | 名称     | 价格   |
   | ---- | -------- | ------ |
   | 1    | 华为手机 | 3449元 |
   | 2    | oppo手机 | 2999元 |
   | 3    | 苹果手机 | 4229元 |

   



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



## 相关文章

1. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
2. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)
3. [pagekit/vue-resource](https://github.com/pagekit/vue-resource)
4. [navicat如何导入sql文件和导出sql文件](https://jingyan.baidu.com/article/a65957f4976aad24e67f9b9b.html)
5. [贝塞尔在线生成器](http://cubic-bezier.com/#.4,-0.3,1,.33)
6. [Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)