###  让定位盒子垂直水平居中

```css
1.position:absolute; top:50%; left:50%; margin-top:-100px; margin-left:-100px;
2.position:absolute; top:50%; left:50%; transform:translate(-50%,-50%)
3.position:absolute; top:calc(50% - 100px); left:calc(50% - 100px);
4.position:absolute; top:0; bottom:0; left:0; right:0; margin:auto;
5.父(display: table-cell; vertical-align: middle;)   子(margin:0 auto;)
6.display:flex; justify-content:center; align-items:center;
```



### transform 变形

- **当同时有位移和其他属性的时候，记得要将位移放到最前面**

- ```css
  transform-origin : right bottom;     /* 设置 旋转中心点位右下角 */
  ```

- translate  位移与定位的区别

  - 定位：
    - 会影响其他盒子位置（脱离标准流）；
    - 行内元素定位，直接变为块级元素；
  - 位移：
    - 不影响其他元素的位置；
    - 在行内元素无效；

- skew
  
  - transform : skew(30deg , 0deg); 把元素水平方向上倾斜30度，处置方向保持不变。可以为负值，第二个参数不写默认为0




### animation 动画

```css
/* animation : 动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 起始或结束的状态*/
animation : move 2s ease 0s infinite alternate forwards;

/* 动画结束后的状态 默认是backwards  回到起始的状态 可以设置停留在结束状态 forwards */
animation-fill-mode:forwards;

/* 暂停动画 经常和鼠标经过等配合使用 */
animation-play-state:puased;
```

|      值      |        描述         |
| :---------: | :---------------: |
|   linear    |        匀速         |
|    ease     |     默认。慢-快-慢      |
|   ease-in   |       低速开始        |
|  ease-out   |       低速结束        |
| ease-in-out |      低速开始和结束      |
|   steps（）   | 指定了时间函数中的间隔数量（步长） |

steps 就是分几步来完成动画  有了steps就不用写ease或者linear了

animation : move 4s steps(5) forwards;



### 视口

- meta视口标签(标准viewport设置)

  - ```css
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    ```

    



### 物理像素&物理像素比

- 物理像素点指的是屏幕显示的最小颗粒，是物理真实存在的，这是出厂时就设置好的
- 开发时候1px不一定等于1个物理像素
- PC端页面1px等于一个物理像素，但是移动端不尽相同
- 1px能显示的物理像素点的个数，称为物理像素比或屏幕像素比




### 3D 转换

- 视距 perspective
  - 加在body：下面所有子元素，形成统一的透视感；
  - 加在各自父亲上：管理下面的子元素形成各自的透视感；


- XY 方向可以设置px值和%（因为有宽高）；
- Z 轴只能设置 px，不能设置%（原因是盒子没有厚度）；


- ```css
   /* 写在一起*/
      transform: translateX(100px) translateY(100px) translateZ(100px);

      /* 三个方向同时写的简写 */
      transform: translate3d(100px,100px,100px);
   ```
  ```

  ```
  
- transform-style 控制子元素是否开启三维立体环境
  - transform-style : flat; 不开启  默认
  - transform-style : preserve-3d; 开启立体空间
  - 代码写给父级，但影响的是子盒子

- 自定义轴向旋转
  
  ```css
  img:hover {
      /* 1, 1, 0为空间向量坐标 x y z */
      transform: rotate3d(1, 1, 0, 45deg);
  }
  ```
  
  



### 图片格式

- dpg：京东自主研发推出DPG图片压缩技术，经测试该技术，可直接节省用户近50%的浏览流量，极大的提升了用户的网页打开速度。全部浏览器的兼容支持，压缩后的图片和webp的清晰度对比没有差距。
- webp：谷歌开发的一种能加快图片加载速度的图片格式。图片压缩体积大约只有JPEG的2/3，并能节省大量的服务器宽带资源和数据空间；




### flex布局

- 父级display : flex ;


- 当为父盒子设为flex布局后，子元素的float、clear和vertical-align属性失效


- 常见父项属性
  - flex-direction : 设置主轴方向

    | 方向           |              |
    | :------------- | ------------ |
    | row            | 默认从左到右 |
    | row-reverse    | 从右到左     |
    | column         | 从上到下     |
  | column-reverse | 从下到上     |
  
- justify-content : 设置主轴上的子元素排列方式（使用之前要确定好主轴是哪个）
  
- align-content : 设置侧轴上的子元素排列方式（多行）
  
    | 排列方式      |                                          |
    | ------------- | ---------------------------------------- |
    | flex-start    | 默认值 从头部开始 若主轴是X轴 则从左到右 |
    | flex-end      | 从尾部开始排列                           |
    | center        | 在主轴居中对齐                           |
  | space-arounds | 平分剩余空间                             |
  | space-between | 先两边贴边  再平分剩余空间               |

  - flex-wrap : 设置子元素是否换行
  
    | 是否换行 |               |
  | -------- | ------------- |
    | nowrap   | 默认值 不换行 |
  | wrap     | 换行          |
  
  - align-items : 设置侧轴上的子元素排列方式（单行）
  
    | 排列方式   |                                  |
    | ---------- | -------------------------------- |
  | flex-start | 从上到下                         |
    | flex-end   | 从下到上                         |
  | center     | 垂直居中                         |
    | stretch    | 拉伸（默认值，子盒子不要给高度） |

  - flex-flow : 复合属性，相当于同时设置了flex-direction和flex-wrap

    - flex-flow : row wrap ;

  - align-self 控制子项自己在侧轴上的排列方式（设给子项）
  
    - align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性，默认值是auto，表示继承父元素的align-items属性，如果没有父元素，等同于stretch
  
  


> **align-content和align-items的区别**
>
> 1. align-items 适用于单行情况下，只有上对齐，下对齐，居中和拉伸
> 2. align-content 适应于换行（多行）的情况下，单行无效，可以设置上对齐，下对齐，居中，拉伸以及平均分配剩余空间等属性值
> 3. 单行找align-items  多行找align-content



### rem布局

em相对于父元素的字体大小，rem相对于html元素的字体大小，rem的优点是可以通过修改html字体大小来改变页面中元素的大小，可整体控制



### 媒体查询

- 媒体查询按从小到大顺序写代码


- 引入资源

  - ```css
    <link rel="stylesheet" href="index1.css" media="screen and (min-width:320px)">
    <link rel="stylesheet" href="index2.css" media="screen and (min-width:640px)">
    ```




### Less

> less(leaner style sheets)是一门css拓展语言，也称css预处理器，在现有css语法上加入了程序式语言的特性，引入了变量，运算以及函数等功能，大大简化了css的编写，降低了css的维护成本。用更少的代码做更多的事。 

- 运算
  - 运算符中间左右用空格隔开1px + 5
  - 对于两个不同单位的值之间的运算，运算结果的值取第一个值的单位
  - 如果两个值之间只有一个值有单位，则运算结果就取该单位




### 移动端特殊样式清除

```css
/* css3盒子模型 */
box-sizing:border-box;
-webkit-box-sizing:border-box;
/* 点击高亮清除，设置为transparent完成透明 */
-webkit-tap-heighlight-color:transparent;
/* 在移动端浏览器默认的外观在IOS上加上这个属性才能给按钮和输入框自定义样式 */
-webkit-appearance:none;
/* 禁用长按页面时弹出菜单 */
img, a {-webkit-touch-callout:none;}
```



### 流式布局（百分比布局）

**流式布局是：**页面元素的宽度按照屏幕分辨率进行适配调整，但整体布局不变。代表作栅栏系统（网格系统）
网页中主要的划分区域的尺寸使用百分数（搭配min-*、max-*属性使用）
**布局特点：**屏幕分辨率变化时，页面里元素的大小会变化而但布局不变。
**缺点明显：**主要的问题是如果屏幕尺度跨度太大，那么在相对其原始设计而言过小或过大的屏幕上不能正常显示。因为宽度使用%百分比定义，但是高度和文字大小等大都是用px来固定，所以在大屏幕的手机下显示效果会变成有些页面元素宽度被拉的很长，但是高度、文字大小还是和原来一样（即，这些东西无法变得“流式”），显示非常不协调。



### 自适应布局

自适应布局的特点是分别为不同的屏幕分辨率定义布局，即创建多个静态布局，每个静态布局对应一个屏幕分辨率范围。改变屏幕分辨率可以切换不同的静态局部（页面元素位置发生改变），但在每个静态布局中，页面元素不随窗口大小的调整发生变化。可以把自适应布局看作是静态布局的一个系列。
**布局特点：**屏幕分辨率变化时，页面里面元素的位置会变化而大小不会变化。



### 响应式布局

响应式设计的目标是确保一个页面在所有终端上（各种尺寸的PC、手机、手表、冰箱的Web浏览器等等）都能显示出令人满意的效果，对CSS编写者而言，在实现上不拘泥于具体手法，但通常是糅合了流式布局+弹性布局，再搭配媒体查询技术使用。——分别为不同的屏幕分辨率定义布局，同时，在每个布局中，应用流式布局的理念，即页面元素宽度随着窗口调整而自动适配。即：创建多个流体式布局，分别对应一个屏幕分辨率范围。可以把响应式布局看作是流式布局和自适应布局设计理念的融合。
**布局特点：**每个屏幕分辨率下面会有一个布局样式，即元素位置和大小都会变。
**优点：**适应pc和移动端，如果足够耐心，效果完美
**缺点：**（1）媒体查询是有限的，也就是可以枚举出来的，只能适应主流的宽高。（2）要匹配足够多的屏幕大小，工作量大，设计也需要多个版本。



### 响应式和弹性布局的对比

**响应式布局：**改变浏览器宽度，“布局”会随之变化，不是一成不变的，例如导航栏在大屏幕下是横排，在小屏幕下是竖排，在超小屏幕下隐藏为菜单，也就是说如果有足够的耐心，在每一种屏幕下都应该有合理的布局，完美的效果。
rem布局：改变浏览器宽度，页面所有元素的高宽都等比例缩放，也就是大屏幕下导航是横的，小屏幕下还是横的只不过变小了。



### 布局选择

1.如果只做pc端，那么静态布局（定宽度）是最好的选择；
2.如果做移动端，且设计对高度和元素间距要求不高，那么弹性布局（rem+js）是最好的选择，一份css+一份js调节font-size搞定；
3.如果pc，移动要兼容，而且要求很高那么响应式布局还是最好的选择，前提是设计根据不同的高宽做不同的设计，响应式根据媒体查询做不同的布局。



### bootstrap

- 规定一行是12份，如果份数少于12份，则占不满container的宽度，会有留白；如果大于12份，则会另起一行显示。
- index.html 初始化：

```css
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <!-- 要求 当前网页 使用 IE浏览器 最高版本的内核 来渲染 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    
    <!-- 视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放 -->
    <meta name="viewport" content="width=device-width, initial-scale=1">
      
    <title>Bootstrap Template</title>

    <!-- Bootstrap 的文件引入 -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
      
    <!-- 条件注释:小于IE9的版本 -->
    <!--[if lt IE 9]>
	  <!--解决ie9以下浏览器对html5新增标签的不识别，并导致CSS不起作用的问题-->
      <script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      
      <!--解决ie9以下浏览器对 css3 Media Query  的不识别 -->
      <script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>
  </body>
```

- 列偏移

```html
<!-- 左右对齐-->
<div class="row">
    <!-- 如果只有一个盒子 那么就偏移 = 12-4-4  -->
    <div class="col-lg-4">1</div>
    <div class="col-lg-4 col-lg-offset-4">2</div>
</div>

<!-- 居中-->
<div class="row">
     <!-- 如果只有一个盒子 那么就偏移 = (12 - 8) /2 -->
     <div class="col-md-8 col-md-offset-2">中间盒子</div>
</div>
```

- ```css
  .hidden-xs  //在最小尺寸的时候隐藏
  .visible-lg  //在最大尺寸的时候显示
  ```

  

### 背景线性渐变

必须加浏览器私有前缀

```css
background:-webkit-linear-gradient(left, red, green); //起始方向可以是度数或者方位名词
```

