# 登录模块

登录（login页面，点击登录按钮触发）：

- 填写账号密码时有自然校验：  data中设置loginFormRules对每一项设置校验规则  prop绑定到对应表单中


- 根据Element-ui中的表单验证方法validate，发送数据接口到后端进行验证。

  - 校验失败，返回提示消息：登录失败。

  - 校验成功：

    - 使用window.sessionStorage.setItem()存储返回的token信息。

    - 使用编程式导航：this.$router.push('/home')跳转至主页

      ​

# 退出

退出（home页，点击退出按钮触发）

- this.$confirm().then().catch() ，confirm()中问用户是否确认退出，如果确认退出，then()方法中，使用window.sessionStorage.removeItem('token')将存储在本地缓存中的token值删除掉。
- then()方法中同时使用编程式导航this.$router.push('/login')跳转至登录页面。



# 路由守卫

router.js中不仅配置路由模块，并且使用路由守卫检测用户是否处于登录状态

```js
router.beforeEach(function(to,from,next){
	//1.使用window.sessionStorage获取token信息
  	var token =  window.sessionStorage.getItem('token')
    //2.判断token的值是否为空并且将要去的路由to.path是否为/login
    //若有一个条件不满足 则强制用户登录
    if(token  === null && to.path !== '/login'){
		return next('/login');
    } 
  	next() //这里一定要写
})
```

# axios请求拦截器

每一次使用axios向后端发送请求时，都要在请求拦截器中设置token认证，验证是否处于登录状态。

核心是取出token  然后再请求头中进行认证

```js
axios.interceptors.request.use(
  function(config) {
    // 给axios配置token
    var token = window.sessionStorage.getItem("token");
    if (token !== null) {
      config.headers.Authorization = token;
    }
    return config;
  },
  function(error) {
    return Promise.reject(error);
  }
);
```





