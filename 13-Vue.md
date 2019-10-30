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

`应用场景`:

如果 服务器返回的数据中，包含有<font color=red>HTML标签</font>(例如富文本编辑器内容)，就可以使用 v-html 来渲染(v-text和 {{}}都不行)

`默认内容`

```html
<p>{{score}}默认内容</p>
<p v-text="score">默认内容</p>
<p v-html="score">默认内容</p>
```

> 以上三者，v-text和v-html标签有默认内容，但是都会被覆盖掉，而 插值表达式 不会覆盖

1. v-html尽量避免使用(除非完全掌控)，否则会带来危险(XSS攻击 跨站脚本攻击)
2. 标签的默认内容会被v-html覆盖



### v-bind(冒号)

```html
<标签 v-bind:属性名称="表达式" ></标签>
<标签 :属性名称="表达式"></标签>  // 简易方式设置，推荐使用
```



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

```
<h1 :style="h1StyleObj">这是一个善良的H1</h1>
```



## Vue指令之`v-for`和`key`属性

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



## Vue指令之`v-if`和`v-show`

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

`结论`

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
  


### v-for

#### 遍历数组

```html
<标签 v-for="小单元 in 数组"></标签>
<标签 v-for="(小单元,下标) in 数组"></标签>
```

#### 遍历对象

```html
<标签 v-for="小单元 in  对象"></标签>
<标签 v-for="(小单元,成员名称) in  对象"></标签>
<标签 v-for="(小单元,成员名称,下标) in  对象"></标签>
```



## Vue指令之`v-on的缩写`和`事件修饰符`

### 事件修饰符：

+ .stop       阻止冒泡

+ .prevent    阻止默认事件

+ .capture    添加事件侦听器时使用事件捕获模式

+ .self       只当事件在该元素本身（比如不是子元素）触发时触发回调

+ .once       事件只触发一次



## 品牌管理案例

### 根据条件筛选品牌

```
<tr v-for="item in list | filterBy searchName in 'name'">
  <td>{{item.id}}</td>
  <td>{{item.name}}</td>
  <td>{{item.ctime}}</td>
  <td>
    <a href="#" @click.prevent="del(item.id)">删除</a>
  </td>
</tr>
```

2. 在2.x版本中[手动实现筛选的方式](https://cn.vuejs.org/v2/guide/list.html#显示过滤-排序结果)：

+ 筛选框绑定到 VM 实例中的 `searchName` 属性：

```
<hr> 输入筛选名称：
<input type="text" v-model="searchName">
```

+ 在使用 `v-for` 指令循环每一行数据的时候，不再直接 `item in list`，而是 `in` 一个 过滤的methods 方法，同时，把过滤条件`searchName`传递进去：

```
<tbody>
      <tr v-for="item in search(searchName)">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.ctime}}</td>
        <td>
          <a href="#" @click.prevent="del(item.id)">删除</a>
        </td>
      </tr>
    </tbody>
```

+ `search` 过滤方法中，使用 数组的 `filter` 方法进行过滤：

```
search(name) {
  return this.list.filter(x => {
    return x.name.indexOf(name) != -1;
  });
}
```



## 过滤器

概念：Vue.js 允许你自定义过滤器，**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache 插值和 v-bind 表达式**。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符指示；

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
    }
  }
```



> 使用ES6中的字符串新方法 String.prototype.padStart(maxLength, fillString='') 或 String.prototype.padEnd(maxLength, fillString='')来填充字符串；



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



## 键盘修饰符以及自定义键盘修饰符

### 1.x中自定义键盘修饰符【了解即可】

```
Vue.directive('on').keyCodes.f2 = 113;
```

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
```

2. 自定义指令的使用方式：

```
<input type="text" v-model="searchName" v-focus v-color="'red'" v-font-weight="900">
```



## Vue 1.x 中 自定义元素指令【已废弃,了解即可】

```
Vue.elementDirective('red-color', {
  bind: function () {
    this.el.style.color = 'red';
  }
});
```

使用方式：

```
<red-color>1232</red-color>
```

## 相关文章

1. [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
2. [vue.js 2.x 文档](https://cn.vuejs.org/)
3. [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
4. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
5. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)