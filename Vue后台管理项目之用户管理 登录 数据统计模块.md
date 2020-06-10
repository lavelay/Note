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





