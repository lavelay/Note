## Promise构造函数

Promise是一个构造器(俗称构造函数)，用来创建Promise类型的对象 。就像Array是一个构造器，用来创建数组类型对象。

### 格式

```js
var p = new Promise((resolve,reject)=>{
  // 某个条件下，执行resolve()
	// 某个条件下，执行reject()
});
```

- 这个构造器的实参是一个函数，这个函数的特殊之处在于它有两个形参，这两个形参也是函数。
- 在函数体的内部， 我们做一些事情，然后根据情况来调用resolve()或者是reject()
- p是一个Promise对象。

从语法上讲，如下代码也是正确的，只是没有什么意义。

```js
var p = new Promise( ()=> {} )
console.info(p)
typeof p  // "object"
```

（1）我们给Promise传入了一个空函数作为实参。
（2）如果你不给Promise构造器传递任何的参数，则会报语法错误。



### 构造器中的代码会立即执行

```js
var p = new Promise((resolve,reject)=>{
	console.log(1);
	resolve();
	console.log(2)
});
```

以上代码中会正常输出1,2 。 调用resolve()这个方法会修改promise的状态，而不会中断函数的执行。



## Promise 对象的三种状态

####  `pending` 

pending,"行将发生的"。相当于是一个初始状态。 
创建Promise对象时，相当于是初始状态。这个初始状态会随着你调用resolve，或者是reject函数而切换到另一种状态。

```js
var p = new Promise((resolve,reject)=>{ console.info('发呆.....' )})
console.dir(p);
```

#### `resolved`

创建Promise对象时，在实参函数中调用了resolve方法。

```js
var p = new Promise((resolve,reject)=>{ console.info('发呆.....' ); resolve();})
console.dir(p)
```

####  `rejected`

创建Promise对象时，调用reject方法。

```js
var p = new Promise((resolve,reject)=>{ console.info('发呆.....' ); reject()})
console.dir(p)
```



### 三种状态的理解

- 状态是可转化

  最初创建promise对象时，默认状态是pending，如果在函数体内部调用了第一个参数对应的函数，则状态变成了resolved；如果调用了第二个参数对应的函数，则状态变成了rejected。

  ```js
   pending ----- 	resolve()   --> resolved;
   pending ----- error() --> rejected ;
  ```


- 状态转换是不可逆的。一旦从pending ---> resolved（或者是rejected），就不可能再回到pending。也不能由resolved变成rejected，或者反过来。 



## promise的值PromiseValue

一个promise对象除了状态之外，还有PromiseValue。在构造函数内部，这个值指的是调用resolve和reject方法时传入的实参值。

```js
var p = new Promise( (resolve,reject) => { resolve(123); } );
//  此时，prommise对象p的状态是 resolved，值是123。

var p = new Promise( (resolve,reject) => { reject(1); } );
//  此时，prommise对象p的状态是 rejected，值是1。 
```

> 单独来看PromiseValue似乎没有什么意义，它的使用场景在于结合promise对象的实例方法一起来用。



## Promise实例的方法

在js中，对象会从它的构造器的原型对象中继承方法。例如：

```
var arr = new Array();
arr.push(); 
```

上面的push方法其实是Array.protoType中的属性。

```
arr.push === Array.protoType.push ; // true
```

同样的道理，一个promise对象也会从Promise.prototype中得方法。

如下：
![image.png](https://upload-images.jianshu.io/upload_images/4071608-0cf7450fb610bc14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- then()
- catch()
- finally()



##  then()方法

> then方法的作用是为Promise对象添加**状态改变**时的回调函数。
>
> 实际上new Promise()操作本身是同步的，then/catch/finally方法才是异步执行的。

### 格式

它可以写两个参数，如下：

```javascript
promise对象.then(参数1，参数2)
```

它的第二个参数是可选的，即可以只写一个参数。

```
promise对象.then(参数1)
```

它的两个参数都是函数。第一个参数是Resolved状态的回调函数，第二个参数是Reject状态的回调函数。

###  调用逻辑

它的两个参数都是函数。它们的执行逻辑是:

- 如果promise对象的状态是resolved，则`promisec对象.then()`会自动调用第一个函数; 
- 状态是rejected，则`promisec对象.then()`会调用第二个函数，如果此时then方法并没有设置第二个参数，就会报错; 

 ```javascript
var p = new Promise((resolve,reject)=>{
   resolve();
});

p.then(()=>{console.info("then,成功")}, ()=>{console.info("then,失败")});
//------------------------------------------------------------------------------
var p = new Promise((resolve,reject)=>{
   reject();
});
p.then(()=>{console.info("then,成功")}, ()=>{console.info("then,失败")});
 ```



### 实参的值

then的参数是两个回调函数，分别在p对象是resolve和reject自动调用。 在调用它们时，会自动把promise对象的promisevalue当作实参给它们传递进去。

示例代码1：

```js
var p = new Promise((resolve,reject)=>{
	resolve(1); //主动调用resolve，并传入
});
// 此时，P的状态是resolved，且值promiseValue 是1.

p.then((res)=>{
    // 因为p的状态是resolved，所以自动执行then的第一个参数，并且把promisevalue传进来。
	console.log("then,ok",res);
});
```

示例代码2：

```js
var p = new Promise((resolve,reject)=>{
	reject(2); //主动调用reject，并传入实参
});
// 此时，P的状态是rejected，且值promiseValue 是2.

p.then((res)=>{
    // 因为p的状态是resolved，所以这句代码不会执行。
	console.log("then,ok",res);
},(err)=>{
    // 因为p的状态是rejected，所以自动执行then的第二个参数，并且把promisevalue传进来。
	console.log("then,err",err);
});
```



### 返回值

then()方法的返回值也是一个promise对象，但是，它的返回值是一个新的promise对象（与调用then方法的并不是同一个对象），所以它支持链式写法。

那既然 p2也是一个promise对象，那么，p2的状态（promiseStatus）和值(promiseValue)分别是什么？

p2的状态及promiseValue按如下规则来确定

- 如果p1的状态是pending,则p2的状态也是pending。
- 如果p1的状态是resolved，then()会去执行f_ok，则p2的状态由f_ok的返回值决定。
  - 如果f_ok返回值不是promise对象，则p2的状态是resolved，且p2的promiseValue就是f_ok函数的return值。
  - 如果f_ok返回值是一个promise对象，则p2的状态及promiseValue以这个promise对象为准。
- 如果p1的状态是rejected，then()会去执行f_err，则p2的状态由f_err的返回值决定。
  - 如果f_err返回值不是promise对象，则p2的状态是resolved，且p2的promiseValue就是f_err函数的return值。
  - 如果f_err返回值是一个promise对象，则p2的状态及promiseValue以这个promise对象为准。



### catch()方法

Promise.prototype.catch是.then(null, reject)的别名，用于指定发生错误时的回调函数 。比较经典的用法是这样：

```javascript
new Promise((resolve,reject){

}).then(function(result){
 // 如果promise对象的状态是resolved的，就会到这里来，并且result会接收promiseValue的值
}).catch(function(err){
 // 如果promise对象的状态是rejected的，就会到这里来，并且err会接收promiseValue的值
});
/// 上面的代码如何拆分来写的话，等价于：
var p1 = new Promise((resolve,reject){

});
var p2 = p1.then(function(result){

});
var p3 = p2.catch(function(err){

});
```



### finally()方法

无论状态如何，都会执行

下面我们来看一下`promise.finally(f);`，
（1）`f`是一个无参函数，不论该`promise`最终是fulfilled还是rejected。
（2）`finally`不改变`promise`的状态。



### 方法异步验证

```js
new Promise((resolve, reject) => {
  console.log(1);
  resolve();
})
  .then(() => {
    console.log('执行resolve');
  })
  .catch(() => {
    console.log('执行reject');
  })
	.finally(() => {
    console.log('执行finally');
  })；

console.log(2);
/* 
	执行结果：
					 1 2 '执行resolve' '执行finally' 
 	可说明new Promise()本身是同步操作，then/catch/finally为异步
*/
```



## 使用promise改造回调函数

```javascript
const fs = require('fs');
function readFile(filename) {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, 'utf8', (err, data) => {
      if (err) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
}

readFile('./server.js1')
  .then(rs => {
    console.log(rs);
  })
  .catch(err => {
    console.log('err', err);
  }); 
```



## async函数

es2017 引入async函数，让异步操作更加方便，写法上更接近同步。

`async`

它用来修饰一个函数，会返回一个promise对象，可以使用then方法添加回调函数。当函数执行时，如果遇到 了await就会先返回，等到异步操作完成，再接着执行函数体后面的语句。

`await`

- 接一个promise对象， 它会自动解析这个promise对象中的promiseValue。
- 只能出现在async函数中。
- 一般在后面接一个函数，而这个函数会返回一个promise对象

如下示例：

```javascript
const fs = require('fs');
function readFile(filename) {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, 'utf8', (err, data) => {
      if (err) {
          resolve(null);
      } else {
        resolve(data);
      }
    });
  });
}
async function dosomething(){
    let rs = await readFile();
    // if(rs)
} 
```



## 应用

> 目的：通过promise的处理，让异步操作书写的像同步代码一样，不需要书写多层的嵌套结构

```javascript
// 将读取文件功能进行封装
function readFile(path) {
  // 将当前读取文件的promise对象返回
  return new Promise((ok, err) => {
    // 在promise中进行异步操作设置
    fs.readFile(path, 'utf-8', (error, data) => {
      // 如果有错误产生，触发catch
      if (error) {
        // 调用err()
        err('读取文件错误');
      } else {
        // 成功时调用ok()触发then()
        ok(data);
      }
    })
  });
}

// 进行多次异步的文件读取操作
//  - 当给then()设置的返回值是promise对象，这个对象会成为then的返回值
readFile('./1.json')
  .then((data) => {
    // 第一次文件读取
    console.log(data);  // 第一次输出

    // 希望读取第二次文件
    return readFile('./21.json')
  })
  .then((data) => {
    console.log(data); // 第二次输出

    // 希望读取第三次文件
    return readFile('./3.json');
  })
  .then((data) => {
    console.log(data);  // 第三次输出
  })
  .catch((err) => {
    console.log(err);
  });
```



## 用async await 改写

> ES6认为promise的.then() .catch()还是有些麻烦，又推出了一种新的写法，用来简化

```javascript
// 使用async和await时，只需要设置ok的调用即可
function readFile(path) {
  return new Promise((ok, err) => {
    fs.readFile(path, 'utf-8', (error, data) => {
      // 无论成功还是失败都触发ok
      if (error) {
        ok(null); // 失败时传入一些错误信息
      } else {
        ok(data); // 成功时传入数据
      }
    })
  });
}
// --- 常用的写法:
// 1 后续设置一个async函数
async function myFun() {
  // 2 调用可以返回promise对象的函数readFile()
  //  - 调用前设置await
  let data1 = await readFile('./1.json');
  // console.log(data1); // 可以根据data1的结果进行ifelse判断

  let data2 = await readFile('./2.json');
  console.log(data2);

  let data3 = await readFile('./3.json');
  console.log(data3);
}
myFun();
```

1. 解决了异步调用彼此嵌套的**回调地狱**问题
2. 解决了多个异步过程**顺序执行**问题



## 并行执行

主要是依赖Promise.all和Promise.race

- `Promise.all:`是**所有的Promise执行完毕后**（reject|resolve）返回一个Promise对象。
- 所有`promise`对象都`resolved`完成，返回所有参数的`resolve`结果。
- 其中一个`promise`对象`rejected`失败，此实例返回失败，失败原因是第一个失败的结果。
- `Promise.race`是**任意一个Promise对象执行完毕后返回**一个Promise对象。

一旦**其中一个`promise`对象**返回成功或失败， 返回的实例就会返回成功或失败的结果。



##### Promise.all 

```js
Promise.all([p1, p2]).then(data=>{
    console.log(data)
})
.catch(e => console.log(e)；
```



##### Promise.race

```js
// Promise.race([p1, p2, p3])里面哪个结果获得的快，就返回那个结果，不管结果本身是成功状态还是失败状态。

let p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success')
  },1000)
})

let p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('failed')
  }, 500)
})

Promise.race([p1, p2]).then((result) => {
  console.log(result)
}).catch((error) => {
  console.log(error)  // 打开的是 'failed'
})
```





```js
Promise.resolve(1)
  .then(2)
  .then(Promise.resolve(3))
  .then(console.log)

// 1

// then 方法接受的参数是函数，而如果传递的并非是一个函数，它实际上会将其解释为 then(null)，这就会导致前一个 Promise 的结果会穿透下面
```

#### [关于 ES6 中 Promise 的题](https://segmentfault.com/a/1190000016848192)

#### [45道Promise题](https://juejin.cn/post/6844904077537574919#heading-2)

