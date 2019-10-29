## vue-介绍

### 三大前端框架

#### Vue

Vue.js (view)是一套构建用户界面的前端<font color=red>框架</font>技术

内部集成了许多基础技术，例如html、css、javascript、ajax、node等，当然还有vue本身高级技术体现，例如组件、过滤器、指令、路由、webpack等等

2012年出现，是中国人 <font color=green>尤雨溪</font> 开发的，2016年3月 加入阿里巴巴公司(该事件助推了vue的发展)



Vue只关注**视图**（页面）层的开发，文档非常丰富、易于上手，流行度高，拥抱经典的web技术、早起灵感来源于angular

vue.js兼具angular.js和react.js的优点，并剔除了它们的缺点



与Vue有关联的话题 组件、路由、webpack、loader、vue-cli、VirtualDOM(虚拟DOM)、NPM、SPA、ES6、单文件组件、双向数据绑定等

 

使用vue的公司

小米、阿里、百度、饿了么、**掘金**、苏宁易购、美团、天猫、Laravel、htmlBurger、哔哩哔哩直播、哔哩哔哩商城



**TypeScript**(javascript超集)

新旧版本没有平滑升级

使用特点：强侵入，凡事都必须遵循angular的规则

#### React

2010年出现，**facebook**公司出品

React.js   是目前最流行的一个框架；是用的人最多的一个框架；但是，学习起来也比较难，因为在 React中，所有的功能，都要用 JavaScript 来实现；

**JSX**(JavaScript XML/Xhtml) & ES2015(es6)   一切都是javascript、包括html、css

(JSX的引入导致代码清晰度很差)

太笨拙，难以掌握，有些地方的代码看起来完全没有逻辑性，学习过程痛苦



## 获得vue

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

3) 使用 `npm`下载（默认安装最新稳定版）

```javascript
npm install vue
```

Vue.js 不支持 IE8 及其以下版本



## vue-简单使用

`目标`：

​	通过vue输出城市和天气信息

`步骤`：

1. 引入vue.js文件

   ```html
   <script src="./vue.js"></script>
   ```

2. 创建div容器

   ```html
   <div id="app"> {{ city }}----{{weather}} </div>
   ```

3. 实例化Vue对象

   ```js
   var vm = new Vue({
     el:xxx
     data:{xxx}
   })
   ```




## Vue-MVVM设计模式

`目标`：

​	了解MVVM各部分含义 和 对应代码

mvvm设计模式可以解读为如下：

m: model  数据部分  data

v：view  视图部分  div容器

vm： view & model 视图和数据 的 结合体  

![1565680427600](Image/img(online)/1565680427600.png)



## vue指令

### 插值表达式

vue中如果需要在html标签的“**内容区域**”中表现数据，就可以使用**{{}}双花括号**，这个技术称为插值表达式

语法：

```html
<标签> {{ 表达式 }} </标签>
```

> 表达式：变量、常量、算术运算符、比较运算符、逻辑运算符、三元运算符

使用示例：

```html
<div id="app">
  <p>{{ msg }}</p>										<!--变量-->
  <p>{{ score }}</p>  								<!--变量-->
  <p>{{ 500 }}</p>  									<!--常量-->
  <p>{{ score+10 }}</p> 							<!--算术运算-->
  <p>{{ score>10 }}</p> 							<!--比较运算-->
  <p>{{ score>80 && age>18 }}</p>  			<!--逻辑运算-->
  <p>{{ age>18 ? '成年' :'少年' }}</p>  	<!--三元运算-->
</div>
```



如果{{}}使用中有冲突，想更换为其他标记，可以这样：

```js
delimiters:['${'，'}$']  // 标记符号变为${}$了 
```



`使用要点`：

1. 在插值表达式中 只能设置**简单**的javascript表达式语句，不能设置**复杂**表达式(例如for循环)
2. 在不改变vue变量值大小的前提下，可以进行一般的 **算术**运算、**比较**运算、**逻辑**运算、**三元**操作符 等运算使用，也可以通过**常量**进行数据体现
3. 插值表达式只能用在html标签的**内容区域**；不能用在其他地方
4. {{}}花括号与变量之间为了美观可以有适当的**空格**，例如{{      msg}}、{{ msg    }}、{{   msg   }}}等都可以



`练习`：

​	在data中声明 score1 和 score2两个变量，分别赋予一定的数字

​	两个变量做算术和，判断总数大小并显示相关信息，大于600显示‘清华’，否则显示'北大'	

### v-text

`目标`：

​	熟练使用 v-text 指令



v-text与{{}}的作用是一样的，都是操控 标签的**内容区域**信息

`语法`：

```html
<标签 v-text="表达式"> </标签>

```



`注意`：

1. 虽然v-text 是标签的属性，但是属性值会添加到标签的内容区域中
2. v-text 的属性值一般要求是普通字符串，如果是html标签，标签的**<>箭头符号**会变为符号实体
3. 如果 标签 内容区域 有默认信息，则会被v-text覆盖掉
4. v-text 可以进行 变量、常量、算术符号、比较符号、逻辑符号、三元运算符号等运算



### v-text-闪烁

`目标`：

​	知道什么是闪烁 和 出现条件



v-text与{{}}  都可以操控 标签 内容区域，但是他们有一点区别

网速非常慢的时候，{{}}  有**闪烁**问题，而 v-text没有(属性就是不会显示出来的)



`什么是闪烁`：

{{ }}花括号  等原生内容 在Vue编译期间 在浏览器**短时**显示的效果就是闪烁

> 闪烁是负面的内容，还不如显示一个白板更好



`出现闪烁的条件`：

- http协议方式打开应用程序文件(给vscode编辑器 安装 live server)
- 调整网速为 慢3G(firebug-->network-->slow 3G)
- 在div容器**之后**引入vue包文件(不要在之前引入)

### v-html

`目标`：

​	熟练使用v-html指令



v-html 与 v-text、{{ }} 的作用一样，都是操控 标签的**内容区域**



`语法`：

```html
<标签 v-html="表达式"> </标签>

```



`v-html、v-text、{{ }}的异同`：

1. v-html对 **html标签** 和 **普通文本** 内容都可以设置显示

2. v-text、{{ }}  只针对  **字符串** 起作用，如果数据中有html标签，那么标签的箭头符号要做<font color=red>符号实体</font>转换，进而使得浏览器上直接"显示箭头"等标签内容，等同于不解析html标签内容

   > <  变为  \&lt;    // less than
   >
   > \> 变为  \&gt;     // great than

3. v-html和v-text没有闪烁问题

4. 它们都可以进行 **变量**、**常量**、**算术运算**、**比较运算**、**逻辑运算**、**三元运算**等技术应用



`应用场景`:

如果 服务器返回的数据中，包含有<font color=red>HTML标签</font>(例如富文本编辑器内容)，就可以使用 v-html 来渲染(v-text和 {{}}都不行)



`默认内容`

```html
<p>{{score}}默认内容</p>
<p v-text="score">默认内容</p>
<p v-html="score">默认内容</p>

```

> 以上三者，v-text和v-html标签有默认内容，但是都会被覆盖掉，而 插值表达式 不会覆盖



`注意`：

1. v-html尽量避免使用(除非完全掌控)，否则会带来危险(XSS攻击 跨站脚本攻击)
2. 标签的默认内容会被v-html覆盖



### v-bind(冒号)

#### 属性绑定-简单使用

`目标`：

​	熟练使用 v-bind指令 对标签属性进行绑定



{{ }}、v-text、v-html可以对标签的**内容区域**进行操作，操作标签的属性需要通过 v-bind 指令



`语法`：

```html
<标签 v-bind:属性名称="表达式" ></标签>
<标签 :属性名称="表达式"></标签>  // 简易方式设置，推荐使用

```



`注意`：

1. 冒号的简易设置推荐使用
2. 如果有需要，绑定的内容可以进行 **变量**、**常量**、**算术运算**、**比较运算**、**逻辑运算**、**三元运算**等技术应用



`案例`：

通过v-bind对img标签的src、width、height属性进行绑定





#### 属性绑定-class属性

`目标`：

​	熟练使用 v-bind 对标签的class属性进行绑定



class属性较比其他属性不一样的地方是，其既可以接收一个值，也可以通过空格分隔接收多个值

例如：

```html
<tag class="apple"></tag>							 <!--接收一个值-->
<tag class="apple pear orange"></tag>		<!--接收多个值-->

```



`class属性绑定的语法`：

```html
1) 对象方式
	<tag :class="{xx:true, xx:false}"></tag>
	<!--true: 设置   false:不设置-->

2) 数组方式
	<tag :class="['xx','yy','zz']"></tag>
	<!--数组元素值如果不是data成员 就要通过单引号圈选，代表是普通字符串-->

```



`注意`：

通过数组方式给class绑定多个值，值如果不是 Vue成员、数值、布尔值，相反就是普通的字母字符串内容，则需要通过**单引号**圈选



`案例`：

通过数组、对象两种方式给p标签的class属性绑定多个值 apple、pear、orange





#### 属性绑定-style属性

`目标`：

​	熟练使用v-bind指令操控style属性



style样式属性较比普通属性也比较特殊，其也可以接收多个值



`具体绑定语法`：

```html
1) 对象方式
	<tag :style="{xx:yy,xx:yy.....}"></tag>
	<!--xx:样式名称，yy:样式的值-->
2) 数组方式
	<tag :style="[{xx:yy},{xx:yy.....}]"></tag>
	<!--根据需要，数组的每个元素都是一个对象，每个对象包含一对或多对css样式-->

```



`注意`：

数组方式绑定style属性，每个数组元素可以包含**一个**或**多个**css样式对



`案例`：

通过数组、对象两种属性绑定方式，实现如下标签效果

```
<p style="color:red; font-size:25px; background-color:lightgreen;"></p>

```



### v-on(@)

#### 事件绑定-简单使用

`目标`：

​	熟练地给标签绑定事件



web端网页应用程序开发，事件是一个不不可或缺的技术

在vue中给元素进行**事件**绑定，需要通过v-on:指令实现，也使用@符号，@是v-on:的简写，使用更方便



事件类型：

> 鼠标事件：onclick  ondblclick onmouseenter onmouseleave onmouseover onmousedown等等
>
> 键盘事件：onkeyup  onkeydown  onkeypress 等等



`语法`：

```html
<tag v-on:事件类型="事件处理"></tag>
<tag @事件类型="事件处理"></tag>  // 简便用法，推荐使用
<div @click="事件处理"></tag>

<script>
var vm new Vue({
  el:xx
  data:xx,
  // 给当前vue实例 声明方法，以供事件调用
  methods:{
    名称：function(){}
  }
})
</script>

```



`注意`：

1. 事件处理驱动 需要通过methods定义
2. 被绑定的事件类型可以是 click、dblclick、keyup、keydown等许多个，注意**不要**设置on标志了



`案例`：

定义一个按钮，使得单击后 控制台 可以输出 “hello，你好呀”

```html
<div id="app">
  <button @click="showinfo()">确定</button>
</div>
<script src="./vue.js"></script>

<script>
  var vm = new Vue({
    el:'#app',
    data:{
    },
    methods:{
      showinfo:function(){
        console.log('你好呀')
      }
    }
  })
</script>

```





#### 事件绑定-传递参数

`目标`：

​	清楚事件中被传递参数的意思



vue“单击”事件参数的3种类型：

1. 有声明()，也有传递实参，形参就代表被传递的实参
2. 没有声明()，第一个形参就是**事件对象**
3. 有声明(),但是没有传递实参，形参就是**undefined**

```html
<div id="app">
  <button @click="dela(301)">删除a</button>
  <button @click="delb()">删除b</button>
  <button @click="delc">删除c</button>
</div>

<script src="./vue.js"></script>

<script>
  var vm = new Vue({
    el:'#app',
    data:{
    },
    methods:{
      dela(id){
        console.log(`id为${id}的商品被删除了`)  // 301
      },
      delb(id){
        console.log(`id为${id}的商品被删除了`)  // undefined
      },
      delc(id){
        console.log(id) // MouseEvent
        console.log(`id为${id}的商品被删除了`)  // MouseEvent
      }
    }
  })
</script>

```



`千万注意`：

事件的参数由于**事件类型**不一样，参数的意思也会有不同，请灵活使用



#### 事件绑定-访问data成员

`目标`：

​	知道事件中如何访问data成员



根据业务需要，事件在执行过程中需要对Vue实例的data数据进行操作，通过<font color=red>this关键字</font>实现，

this代表Vue实例对象，并且针对data或methods成员都可以直接进行调用



`案例`：

​	给data声明city成员，值为“铁岭”

​	设置按钮，使得单击后控制台可以输出“铁岭是一个大城市”

```html
<button @click="getInfo()" >获取数据</button>

<script>
  var vm = new Vue({
    el:'#app',
    data:{
      address:'铁岭'
    },
    methods:{
      getInfo:function(){
        // 通过 this关键字 获得 data区域的数据信息
        console.log(this.address+'是一个大城市');
      }
    }
  })
</script>

```



#### 事件绑定-this是谁

`目标`：

​	知道Vue实例中this是谁



在Vue实例内部包括不限于methods方法中，this关键字 是对象，具体与 new Vue() 是一样的

> this ===  vm 

并且其可以对 **data** 和 **methods**成员进行直接访问

```html
<script>
  var vm = new Vue({
    el:'#app',
    data:{
    },
    methods:{
      showinfo:function(){
        console.log(this)    // Vue实例对象(与外部的vm引用完全)
      }
    }
  })
</script>

```



`注意`：

this 与 vm 的指引完全一致，它们可以通过===判断等于



`一般this指向`：

1. this就是window对象

   ```js
   var age = 20
   function getInfo(){
     console.log(this.age)
   }
   getInfo()  // 20
   
   ```

   

2. this代表调用该方法的当前对象

   ```js
   const tiger = {
     name:'东北虎', 
     act:'猛虎扑食', 
     say(){
       console.log('我的名字是'+this.name+'，我的招牌动作是'+this.act)
     }
   }
   tiger.say()
   
   ```

   

3. this代表元素节点对象

   ```html
   <input type="text" onclick="this.style.color='red'" />
   
   ```

   

`注意`：

js中this的使用千变万化，不用强记，通过console.log输出查看便知



#### 事件绑定-方法简易设置

`目标`：

​	对methods的各个成员进行简易设置



`具体设置`：

根据es6标准，可以给methods各个方法做简易设置如下：

```js
var vm = new Vue({
  el:'#app',
  data:{
  },
  methods:{
    dela(id){
      console.log(`id为${id}的商品被删除了`)  // 301
    },
    delb(id){
      console.log(`id为${id}的商品被删除了`)  // undefined
    },
    delc(id){
      console.log(id) // MouseEvent
      console.log(`id为${id}的商品被删除了`)  // MouseEvent
    },
  }
}
// dela:function(){}   简易设置为  dela(){}
// delb:function(){}   简易设置为  delb(){}
// delc:function(){}   简易设置为  delc(){}

```

> 以后在其他应用中，对象中成员方法都可以把 ":function" 去除，做简易设置，是es6的标准规范



`原理`：

es6标准里边规定，对象成员 与 值的变量名称保持一致，就可以做简易设置

```javascript
var name = "xiaoqiang"
var height = 176
var run = function(){
  console.log('在跑步')
}

var person = {name:name,height:height,run:run}		// 正常创建对象
var person = {name, height, run}					// 简便方式创建对象

```



```javascript
var obj = {
  // walk:function(){
  //   console.log('走直线')
  // }
  //变形
  // walk:function walk(){
  //   console.log('走直线')
  // }
  walk(){
    console.log('走直线')
  }
}

```

> 给一个对象直接声明一个成员方法，也可以简写为如上形式，去除": function"字样







### v-model

在Vue中有一个很重要的指令，名称为v-model，其被称为**双向数据绑定**指令，就是Vue实例对数据进行修改，页面会立即感知，相反页面对数据进行修改，Vue内部也会立即感知

v-model是vue中 唯一实现 <font color=red>双向数据绑定</font>  指令

![](E:/待办事项/JS每日/01day/笔记/img(online)/1-555.png)

v-bind<font color=red>单向</font>数据绑定，只是使得vue的数据渲染给页面元素，页面对数据进行修改，vue不会感知到

v-model<font color=red>双向</font>数据绑定，数据从vue里边渲染给页面，页面对其进行修改，Vue内部会立即感知

#### 简单使用

`目标`：

​	了解v-model的特性



`语法`：

```html
<标签 v-model="data成员"></标签>

```



`注意`：

1. v-model是vue中**唯一**的双向数据绑定指令

2. v-model只针对**value属性**可以绑定，因此经常用在form表单标签中，例如input(输入框、单选按钮、复选框)/select(下拉列表)/textarea(文本域)

3. v-model只能绑定**data成员**，不能设置其他表达式，否则错误

   > 例如 
   >
   > v-model="score+100"  错误
   >
   > v-model="120"  错误
   >
   > v-model="score" 正确的



`效果`：

```html
<div id="app">
  <p>{{ city }}</p>
  <p><input type="text" :value="city" /></p>  <!--v-bind属性绑定-->
  <p><input type="text" v-model="city" /></p>  <!--v-model属性绑定-->
</div>

<script src="./vue.js"></script>

<script>
  var vm = new Vue({
    el:'#app',
    data:{
      city:'铁岭'
    }
  })
  console.log(vm)
</script>

```

> v-model对应的city发生变化后，其他的{{ }} 和 :value的值也会发生变化

#### 响应式

`目标`：

​	知道什么是响应式



`响应式`：

vue实例的data数据如果发生变化，那么页面上用到的地方会重新编译执行，这样就把更新后的内容显示出来了

这个过程就是“响应式”

![](Image/img(online)/1-666.png)

`步骤`：

1. 页面初始加载，vue的数据<font color=red>渲染</font>给div容器

2. 通过v-model修改数据，修改的信息会直接反馈给vue内部

3. vue的数据发生变化，页面上(也包括Vue实例本身)用到该数据的地方会<font color="red">重新编译渲染</font>

   > 2和3 步骤在条件满足情况下会**重复**执行



`注意`：

响应式 是Vue中非常重要的机制，请仔细钻研



#### 加法计算器

`案例`：

利用 **v-model** 和 **事件绑定**  实现 加法计算器案例效果：

```html
  <div id="app">
    <h2>简易加法计算器</h2>
    <p>
      <input type="number" v-model="num1">
      <span>+</span>
      <input type="number" v-model="num2">
      <button @click="jieguo">=</button>
      <span>{{ result }}</span>
    </p>
  </div>
  
  <script src="./vue.js"></script>

  <script>
    var vm = new Vue({
      el:'#app',
      data:{
        num1:'',
        num2:'',
        result:''
      },
      methods:{
        jieguo(){
          // 两个操作数做加法计算，结果给result
          this.result = Number(this.num1)+Number(this.num2)
        }
      }
    })
  </script>

```



#### 简易原理

`目标`：

​	了解简易v-model实现原理



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
</div>

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



`结论`：

1. 事件声明没有小括号()，**第一个形参**就是 事件对象

2. 事件声明，本身可以直接使用**$event**,其也是事件对象




#### 其他表单域使用(自学)

- 绑定文本框

  当文本框的值发生改变后，div中的内容也会发生变化

  ```php+HTML
  <input type="text" v-model="name" />
  <div>{{ name }}</div>
  <script>
      var vm = new Vue({
         el: '#app',
          data: {
              name: ''
          }
      });
  </script>
  
  ```

  

- 绑定多行文本框

  ```php+HTML
  <textarea v-model="name"></textarea>
  <div>{{ name }}</div>
  
  ```

  > 注意：
  >
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

    > xieyi：体现true或false信息

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

  



### v-for

#### 遍历数组

`目标`：

​	使用v-for指令，熟练遍历数组信息

`语法`：

```html
<标签 v-for="小单元 in 数组"></标签>
<标签 v-for="(小单元,下标) in 数组"></标签>

```

`注意`：

​	使用v-for指令的html标签，由于遍历机制，本身会被创建多份出来

`示例`：

```html
<div id="app">
  <ul>
    <li v-for="item in color">{{item}}</li>
  </ul>
  <ul>
    <li v-for="(item,k) in color">{{k}}-----{{item}}</li>
  </ul>
</div>

<script src="./vue.js"></script>

<script>
  var vm = new Vue({
    el:'#app',
    data:{
      color:['red','purple','blue']
    },
    methods:{
    }
  })
</script>

```



#### 遍历对象

`目标`：

​	使用v-for指令，熟练遍历对象信息

`语法`：

```html
<标签 v-for="小单元 in  对象"></标签>
<标签 v-for="(小单元,成员名称) in  对象"></标签>
<标签 v-for="(小单元,成员名称,下标) in  对象"></标签>

```

`示例`：

```html
<div id="app">
  <ul> <li v-for="item in cat">{{item}}</li> </ul>
  <ul> <li v-for="(item,m) in cat">{{m}}----{{item}}</li> </ul>
  <ul> <li v-for="(item,m,k) in cat">{{k}}----{{m}}----{{item}}</li> </ul>
</div>
<script src="./vue.js"></script>
<script>
  var vm = new Vue({
    el:'#app',
    data:{
      cat:{
        name:'kitty',
        age:5,
        walk(){console.log('走直线')}
      }
    }
  })
</script>

```

作业：

1. 开发一款加法计算器，在data中只有两个成员num1和num2，没有result了，计算结果要直接表现在页面上







