### a标签（超链接）

1. target属性

```html
target = "_blank" <!--  链接将在新窗口打开 -->
target = "_self" <!--  链接将在当前窗口打开 -->
```

2. 锚点

   `<a href="#id"></a>`同页面中跳转

   `<a href="xxx（地址）#id"></a>`不同页面中锚点跳转




### DOCTYPE

Doctype作用？标准模式与兼容模式各有什么区别?

    （1）<!DOCTYPE>声明位于HTML文档中的第一行，处于 <html> 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
    （2）标准模式的排版 和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。
HTML5 为什么只需要写 <!DOCTYPE HTML>？


    HTML5 不基于 SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；
    而HTML4.01基于SGML,所以需要对DTD进行引用，才能告知浏览器文档所使用的文档类型。
HTML文件必须加上 DOCTYPE 声明，并统一使用 HTML5 的文档声明：

```html
<!DOCTYPE html>
```

**HTML5标准模版**

```html
<!DOCTYPE html>
  <html lang="zh-CN">
  <head>
  <meta charset="UTF-8">   <!-- 字符集 防止乱码 -->
  <title>HTML5标准模版</title>
  </head>
  <body>
  </body>
</html>
```



### img标签

“alt”属性是图片不显示时，显示的文本（替换文本）

“title”属性是鼠标悬停时显示的文字（提示文本）



### base

在head标签里写`<base target="_blank">`会让页面的所有链接在新窗口打开（减少了代码冗量）



### 表格

- table、tr、td 创建表格的基本标签，缺一不可

- tr里只能放td或th

- td里可以放任意标签

- cellpadding 属性：单元格内边距（默认值是1）

- cellspacing 属性： 控制单元格之间的距离（默认值是2）

- 单元格合并    rowspan=“num”   竖直方向

  ​					 colspan=“num”    水平方向	




### 表单

```html
<input type="text" maxlength="6">   <!-- 输入的最大字符长度 -->
```

> 提交信息必须有form表单
>
> - action 收集的信息提交给那个文件处理
> - name 传递信息的凭证
> - method   有get、post两种传递信息的方法（都不安全）



###  语义化

1.用正确的标签做正确的事情
2.html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析
3.即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的
4.搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO
5.使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解等等