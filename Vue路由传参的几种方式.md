## Vue路由传参的几种方式

vue路由传参是指嵌套路由时父路由向子路由传递参数，否则操作无效。传参方式可以划分为params传参和query传参，params传参又可以分为url中显示参数和不显示参数两种方式。

## push方法跳转

### 手写完整的path：

this.$router.push({path:`/user/${userId}`})

这样传递参数的话，配置路由的时候需要在path上加参数path：user/：userId。

这种接收参数的方式是this.$route.params.userId。

### query方式传参和接收参数

```js
传参: 
this.$router.push({
        path:'/xxx',
        query:{
          id:id
        }
      })
  
接收参数:
this.$route.query.id
注意:传参是this.$router,接收参数是this.$route,这里千万要看清了！！！
```

**this.$router 和this.$route有何区别？**
在控制台打印两者可以很明显的看出两者的一些区别：

![1562153034052](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562153034052.png)

- 1.$router为VueRouter实例，想要导航到不同URL，则使用$router.push方法

- 2.$route为当前router跳转对象，里面可以获取name、path、query、params等

  ### params方式传参和接收参数

  ```
  传参: 
  this.$router.push({
          name:'xxx',
          params:{
            id:id
          }
        })
    
  接收参数:
  this.$route.params.id
  注意:params传参，push里面只能是 name:'xxxx',不能是path:'/xxx',因为params只能用name来引入路由，如果这里写成了path，接收参数页面会是undefined！！！
  ```

注意：如果提供了path，params将会被忽略，但是query不属于这种情况。。。

如果使用完整路径和query传参，刷新页面时不会造成路由传参的参数丢失。

另外，二者还有点区别，直白的来说query相当于get请求，页面跳转的时候，可以在地址栏看到请求参数，而params相当于post请求，参数不会再地址栏中显示

## router-link标签跳转

### params传参（url中显示参数）

**定义路由：在定义path路由路径时定义参数名和格式，如  path: "/one/login/:num"**

```js

//第一步：引用vue和vue-router ，Vue.use（VueRouter）
import Vue from 'vue'
import Router from 'vue-router'
Vue.use(Router)
 
//第二步：引用定义好的路由组件
import ChildOne from '../components/childOne'
import ChildTwo from '../components/childTwo'
import Log from '../components/log.vue'
import Reg from '../components/reg.vue'
 
//第三步：定义路由（路由对象包含路由名、路径、组件、参数、子路由等），每一个路由映射到一个组件
//第四步：通过new Router来创建router实例
export default new Router({
  mode: 'history',
  routes: [
    {
      path: '/one',
      name: 'ChildOne',
      component: ChildOne,
      children:[
        {
          path:'/one/log/:num',
          component:Log,
        },
        {
          path:'/one/reg/:num',
          component:Reg,
        },
      ],
    },
    {
      path: '/two',
      name: 'ChildTwo',
      component: ChildTwo
    }
  ]
})

```

**在父路由组件上使用router-link进行路由导航，传参用<router-link to="/one/login/001">的形式向子路由组件传递参数。使用router-view进行子路由页面内容渲染，父路由组件childOne.vue 如下：**

```html

<template>
  <div style="border:1px solid red;color:red;">
    <p>这是父路由childOne对应的组件页面</p>
    <p>下面可以点击显示嵌套的子路由 </p>
    <router-link to="/one/log/123">显示登录页面</router-link>
    <router-link to="/one/reg/002">显示注册页面</router-link>
    <router-view></router-view>
  </div>
</template>
```

**子路由通过 this.$route.params.num 的形式来获取父路由向子路由传递过来的参数，子路由组件login.vue如下**

```html

<template>
  <div style="border:1px solid orange;color:orange;">
    <p>登录界面：这是另一个嵌套路由的内容</p>
    <h3>{{this.$route.params.num}}</h3>
  </div>
</template>
```

注意：如上所述路由定义的path: "/one/login/:num"路径和to="/one/login/001"必须书写正确，否则不断点击切换路由，会因为不断将传递的值显示添加到url中导致路由出错，如下

![1562152446775](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562152446775.png)

传递的值存在url中存在安全风险，为防止用户修改，另一种方式不在url中显示传递的值

### params传参（url中不显示参数）

**定义路由时添加name属性给映射的路径取一个别名，router>index.js文件修改router如下**

```js
export default new Router({
  mode: 'history',
  routes: [
    {
      path: '/one',
      name: 'ChildOne',
      component: ChildOne,
      children:[
        {
          path:'/one/log/',
          name:'Log',
          component:Log,
        },
        {
          path:'/one/reg/',
          name:'Reg',
          component:Reg,
        },
      ],
    },
    {
      path: '/two',
      name: 'ChildTwo',
      component: ChildTwo
    }
  ]
})
```

- **在父路由组件上使用router-link进行路由导航，使用   <router-link :to="{name:'home',params:{id:001}}>    形式传递参数。**** 注意   ': to= ' 前面的冒号，childOne.vue组件修改如下：**

  ```html
  
  <template>
    <div style="border:1px solid red;color:red;">
      <p>这是父路由childOne对应的组件页面</p>
      <p>下面可以点击显示嵌套的子路由 </p>
      <router-link :to="{name:'Log',params:{num:666}}">显示登录页面</router-link>
      <router-link :to="{name:'Reg',params:{num:888}}">显示注册页面</router-link>
      <router-view></router-view>
    </div>
  </template>
  ```

  **子路由组件页面获取父路由传参方式不变，reg.vue 文件如下**

```html

<template>
  <div style="border:1px solid orange;color:orange;">
    <p>登录界面：这是另一个嵌套路由的内容</p>
    <h3>子路由获取的参数：{{this.$route.params.num}}</h3>
  </div>
</template>
```

**注意：上述这种利用params不显示url传参的方式会导致在刷新页面的时候，传递的值会丢失；**

### 使用Query实现路由传参

**定义路由 router>index.js文件如下**

```js
export default new Router({
  mode: 'history',
  routes: [
    {
      path: '/one',
      name: 'ChildOne',
      component: ChildOne,
      children:[
        {
          path:'/one/log/',
          component:Log,
        },
        {
          path:'/one/reg/',
          component:Reg,
        },
      ],
    },
    {
      path: '/two',
      name: 'ChildTwo',
      component: ChildTwo
    }
  ]
})

```

**修改路由导航** **<router-link :to="{path:'/one/log',query:{num:123}}"> ，** **childOne.vue 文件修改如下**

```html

<template>
  <div style="border:1px solid red;color:red;">
    <p>这是父路由childOne对应的组件页面</p>
    <p>下面可以点击显示嵌套的子路由 </p>
    <router-link :to="{path:'/one/log',query:{num:123}}">显示登录页面</router-link>
    <router-link :to="{path:'/one/reg',query:{num:999}}">显示注册页面</router-link>
    <router-view></router-view>
  </div>
</template>
```

**子路由组件通过** **this.$route.query.num 来显示传递过来的参数，reg.vue 文件如下**

```html
<template>
  <div style="border:1px solid purple;color:purple;">
    <p>注册界面：这是二级路由页面</p>
    <h3>{{this.$route.query.num}}</h3>
  </div>
</template>
```

PS: 在第一步的定义路由中我们都使用了mode：history 作用就是去除路由跳转时路由路径前的 “#”

常用的mode模式有两种：

默认为hash模式，最明显的标志是，URL上有#号 localhost:8080/#/，路由会监听#后面的信息变化进行路由匹配

另一种为history模式，不会有#出现，很大程度上对URL进行了美化。需要**注意**history模式在打包后的路由跳转需要服务器配合

