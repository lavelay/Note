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
      var dt = new Date(input);
      // 获取年月日
      var y = dt.getFullYear();
      var m = (dt.getMonth() + 1).toString().padStart(2, '0');
      var d = dt.getDate().toString().padStart(2, '0');
      if (pattern.toLowerCase() === 'yyyy-mm-dd') {
        return `${y}-${m}-${d}`;
      } else {
        // 获取时分秒
        var hh = dt.getHours().toString().padStart(2, '0');
        var mm = dt.getMinutes().toString().padStart(2, '0');
        var ss = dt.getSeconds().toString().padStart(2, '0');
        return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
      }
    }
  }
```



### 全局过滤器

```js
// 定义一个全局过滤器

Vue.filter('dataFormat', function (input, pattern = '') {
  var dt = new Date(input);

  // 获取年月日
  var y = dt.getFullYear();
  var m = (dt.getMonth() + 1).toString().padStart(2, '0');
  var d = dt.getDate().toString().padStart(2, '0');
  // 如果 传递进来的字符串类型，转为小写之后，等于 yyyy-mm-dd，那么就返回 年-月-日
  // 否则，就返回  年-月-日 时：分：秒
  if (pattern.toLowerCase() === 'yyyy-mm-dd') {
    return `${y}-${m}-${d}`;
  } else {
    // 获取时分秒
    var hh = dt.getHours().toString().padStart(2, '0');
    var mm = dt.getMinutes().toString().padStart(2, '0');
    var ss = dt.getSeconds().toString().padStart(2, '0');
    return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
  }
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



Vue实例代码：

```js
  var vm = new Vue({
    el:'#app',
    data:{
      newbrand:'', // 被添加的新品牌
      xu:12, // 记录最大的id值
      ……
      
    },
    methods:{
      // 添加新品牌
      add(){
        // 判断有新品牌才执行添加动作
        if(this.newbrand.trim().length!==0){
          // 新品牌信息需要添加到brandsList成员中去
          // 通过"对象"维护新品牌数据
          var obj = {
            id:++this.xu,
            name: this.newbrand,
            ctime: new Date()
          }
          // 把obj放到brandsList数组中去(靠前放)
          this.brandsList.unshift(obj)
          // 把添加好的品牌清除掉
          this.newbrand = ''
        }
      }
    }
  }
```

`注意`：

​	添加新品牌的**xu序号**，是临时设置的，真实项目中不用维护，数据库会自动生成



## vscod设置代码片段

vscode编辑器：设置--->User snippets---->html.json，配置如下内容

```json
{
	"Print to console": {
		"prefix": "log",
		"body": [
			"console.log()",
		],
		"description": "Log output to console"
	},
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



### 品牌管理-筛选

v-for做遍历，目标可以是data成员，也可以是methods方法

```html
<标签 v-for="(item,k) in data成员" :key="item.id">
<标签 v-for="(item,k) in methods方法()" :key="item.id">
<标签 v-for="(item,k) in 复杂表达式" :key="item.id">
```

> 模板容器可以通过“复杂表达式”体现要使用的数据，不仅v-for可以使用

`步骤`：

1. 给关键字输入框设置v-model="keywords"

2. 在data中声明keywords成员

3. 在methods方法中声明guolv()方法，实现数据筛选

4. 模板中包括v-for，把brandsList都替换为guolv()方法




`模板代码`：

```html
<tr>
  <td>
    <input type="text" v-model="newbrand" />
    <button @click="add">添加</button>
  </td>
  <td><input type="text" placeholder="请输入关键字" v-model="keywords"></td>
</tr>
<table v-if="guolv().length>0">
  ……
  <tr v-for="(item,k) in guolv()" :key="item.id">
    ……
  </tr>
</table>

```

`Vue实例的methods方法`：

```js
// 筛选品牌
guolv(){
  // filter()实现集合的筛选过滤
  // 1. 遍历目标
  // 2. item 遍历出来的成员值
  // 3. 回调函数要求return返回布尔值
  //     true:收集当前项目
  //     false:排除当前项目
  // 4. 会把过滤筛选的结果给返回，但是需要return
  return this.brandsList.filter(item=>{
    // 判断item.name是否包含keywords
    // 大串.includes(小串)  布尔值ture/false
    // 大串.includes('')  始终返回true
    return item.name.includes(this.keywords)
  })
}
```

> 注意：
>
> 1. filter(箭头函数)里边设置箭头函数参数，会使得内部this与外部保持一样的指引(new Vue())
> 2. filter回调函数内部必须设置return，返回判断结果
> 3. guolv()方法必须通过return返回整体筛选结果



```html
<tr>
  <td>
    <input type="text" v-model="newbrand" />
    <button @click="add">添加</button>
  </td>
  <td><input type="text" placeholder="请输入关键字" v-model="keywords"></td>
</tr>
<table v-if="brandList.filter(item=>{ return item.name.includes(this.keywords) }).length>0">
  ……
  <tr v-for="(item,k) in brandList.filter(item=>{ return item.name.includes(this.keywords) })" 
      :key="item.id">
    ……
  </tr>
</table>
```

> 即把methods方法的逻辑表达式直接设置到模板里边运行



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



`案例1`：

通过computed计算属性**获取**并**应用**筛选的品牌数据

步骤：

1. 创建计算属性

   在Vue实例内部创建计算属性(与el、data、methods并列位置处)

   ```js
   // 声明计算属性
   computed:{
     // 创建一个名称为result的计算属性
     result(){
       // 可以正常使用this关键字
       return this.brandList.filter(item=>{
         return item.name.includes(this.keywords)
       })
     }
   },
   
   ```

2. 应用计算属性

   ```html
   <table v-if="result.length>0">
     <tr>
       <td></td>
       <td>序号</td>
       <td>名称</td>
       <td>创建时间</td>
       <td>操作</td>
     </tr>
     <tr v-for="(item,k) in result" :key="item.id">
       <td><input type="checkbox"></td>
       <td>{{ item.id }}</td>
       <td>{{ item.name }}</td>
       <td>{{ item.ctime | timeFormat('北京') }}</td>
       <td><button @click="del(k)">删除</button></td>
     </tr>
   </table>
   
   ```

   > 之前走guolv()方法，现在走result计算属性了



### 品牌应用

1. **回车键** 被触碰就添加新品牌

2. **ESC键** 被触碰就把已经输入的新品牌给做清除操作，取消添加

```html
<input type="text" v-model="newbrand" @keyup.enter="add" @keyup.esc="newbrand=''" />
```



### 获得焦点-私有

```js
// 自定义指令
directives:{
  // 名字没有v-前缀，使用的时候有
  dian:{
    // 配置成员方法
    // inserted是众多成员之一
    // inserted：代表页面上各种指令被解析渲染完毕后的“时机”
    // 参数m：应该该指令的元素节点对象
    //        m.style.color="red"
    //        m.focus()
    //        m.style.width='500px'
    inserted:function(m){
      m.style.color='red'
      m.focus()
    }
  }
}
```

应用指令：

```html
<input type="text" v-dian v-model="newbrand" @keyup.enter="add" @keyup.esc="newbrand=''" />
```

​	无论是全局指令 还是 私有指令，声明的时候都不用设置v-前缀，使用的时候再添加上即可



### 获得焦点-全局

```js
Vue.directive('dian2',{
  inserted(m){
    // m：代表使用指令的html对象(dom对象)
    // console.dir(m)
    // 使得m对象获得焦点
    m.focus()
  }
})
```

应用：

```html
<input type="text" v-dian2 v-model="newbrand" @keyup.enter="add" @keyup.esc="newbrand=''" />
```



### template

在Vue实例内部可以声明template，其内容可以覆盖掉原生的div容器的

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

如果定义了render成员，那么其提供的内容会渲染到页面中，并且会**覆盖**原容器，包括template

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
      // render：设置内容去覆盖渲染容器并显示
      // render:function(create){
      //   // return是固定用法
      //   // return create(标签,内容区域信息)
      //   return create('span','广州')  // <span>广州</span>
      // },
      // render:function(h){
      //   return h('span','广州')  // <span>广州</span>
      // },
      // render:h=>{
      //   return h('span','广州')  // <span>广州</span>
      // },
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

```js
    console.group('java班级')
    console.log('王一')
    console.log('王二')
    console.group('前端班级')
    console.log('张一')
    console.log('张二')
    console.log(
      '%c%s',
      'color:red;font-size:25px;background-color:lightblue;border:2px solid green;',
      '张三'
    )
```



[Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)




## [vue实例的生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)

+ 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！
+ [生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)：就是生命周期事件的别名而已；
+ 生命周期钩子 = 生命周期函数 = 生命周期事件
+ 主要的生命周期函数分类：

 - 创建期间的生命周期函数：

   + beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
   + created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
   + beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
   + mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示

 - 运行期间的生命周期函数：

  + beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
  + updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！

 - 销毁期间的生命周期函数：

  + beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
  + destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。


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