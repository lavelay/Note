## 1.任意数求和

```javascript
function sum () {
    var total = null;
    for(var i = 0; i < arguments.length; i++) {
        var item = arguments[i];
        item = parseFloat(item);
        !isNaN(item) ? total +=item : null;
    }
    return total;
}
```



## 2.获取页面中所有ID

获取页面中所有ID为HAHA的标签（兼容所有浏览器，不能使用querySelecterAll）

```javascript
function queryAllById(id) {
    var nodeList = document.getElementsByTagName('*');
    var ary = [];
    for (var i = 0; i < nodeList.length; i++) {
        var item = nodeList[i];
        item.id === id ? ary.push(item) : null;
    }
    return ary;
}
console.log(queryAllById('HAHA'));
```

简单的方法：`console.log(HAHA);`

在JS中，默认会把元素的ID设置为变量（不用再获取设置），若ID重复，获取的结果就是一个集合，包括所有的ID项，不重复就是一个元素对象（类似于ById获取的结果）



```javascript
var a = 9;
function fn() {
    a = 0;
    return function (b) {
        return b+a++;
    }
}
var f = fn();  
console.log(f(5)); // 5
console.log(fn()(5));// 5
console.log(f(5));// 6
console.log(a);// 2
```

