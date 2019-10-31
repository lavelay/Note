### link和@import区别

    （1）link属于XHTML标签，页面被加载的时，link会同时被加载
    		定义：链入一个文档，通过rel属性声明链入文档与当前文档之间的关系
    （2）@import是CSS提供的，只用于加载CSS，@import引用的CSS会等到页面被加载完再加载;
    （3）@import是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;
    （4）link支持用javascript改变样式，@import不支持


### 字体/文本

- `font-family : arial , '宋体'`

  多个字体时英文写在前面，中文字体写在后面

- 字体字号大小一般都用偶数（12px、16px . . . ）

- escape（“汉字”）可以转化为Unicode字体编码     **%u <=> \ **

- letter-spacing  : 1px ;      字与字之间的距离，可为负值

  word-spacing  : 1px;

- 一个 em 相当于一个汉字的大小

  text-indent : 2em       首行缩进2字符

  text-decoration : underline / overline ;     下划线 / 上划线




### 省略文字

文字超出范围，内容自动裁切，以省略号代替(三个条件缺一不可)

```css
white-space : nowrap;
overflow : hidden;
text-overflow : ellipsis;
```



### 能用transform就不用普通样式

transform会自动开启硬件加速，规避回流和重绘（性能相对较好）



### BFC（块级格式化上下文）

BFC是一种渲染机制，触发一个元素的BFC，相当于在这个元素里面建立起一堵墙，墙里面的内容和外面的内容互不干扰

zoom：1用来触发  haslayout （IE浏览器中的BFC）

zoom是缩放的意思



### display

inline-block 代码换行会解析空格



### css中属性排列顺序

1. 布局定位属性：display / position / float / clear / visibility / overflow (建议 display 第一个写，毕竟关系到显示模式)
2. 自身属性： width / height / margin / padding / border / background
3. 文本属性： color / font / text-decoration / text -align / vertical-align / white-space / break-word
4. 其他属性： content / cursor / border-radius / box-shadow / text-shadow / background...




### overflow常见值

- overfolw : hidden; 超出隐藏。
- overfolw : auto; 当盒子里面的内容超出设置盒子的大小，盒子会自动添加滚动条。
- overflow : scroll; 不论里面内容的多少，始终添加滚动条




### background

- background­-position:10px 20px;

  - 写具体数值
    - 水平位置距离左边10px，垂直距离距离顶部20px
    - 写一个数字时，另外一个值默认center
  - 写方位值
    - 写两个方位值，没有顺序要求
    - 写一个 方位值，另外一个方位值默认center

- backgrpund­-size:contain; 背景图片缩放时候会以合适大小进行缩放，只要宽度或

  者高度铺满容器就会停止。

- background­-size:cover;背景图片缩放时候为了满足容器的宽高同时铺满，会造成

  图片部分显示不全。

- background-size: 写具体数值

  - 写两个值，第一个代表宽，第二个代表高
  - 写一个值，代表宽，高默认auto，等比例缩放
  - 写百分比，参考的是盒子的百分比

- background-attachment（背景附着）

  - scroll 默认值 背景图像会随着内容（滚动条）滚动

  - fixed   固定   背景图像不会随着内容（滚动条）滚动

  - 如果背景附着的值为fixed的时候，背景定位参考的不是盒子的大小，而是浏览器。

- 背景属性连写：

  > background：背景颜色  图片路径  背景平铺  背景滚动  背景位置



### 三大特性

- 继承性
  - 子元素可以继承父元素的样式（text- ，font-  ，line-  这些元素开头的都可以继承，以及color属性）都是文字类的。
  - 特殊情况
    - a标签不会继承父元素文字颜色
    - 标题标签不会继承父元素的文字大小，但会继承颜色

- 层叠性
  - 权重相同的情况下，后面的会层叠掉前面的
- 权重
  - **数位之间没有进制**  比如： 0，0，0，5  +   0，0，0，5 = 0，0，0，10而不是0，0，1，0       所以不会存在10个div能赶上一个类选择器的情况
  - **权重是优先级的算法，层叠是优先级的表现**




### 表格

border-collapse：collapse；        表格的边框合并，只能用在表格上



### 内外边距

- 块元素不设置宽度时

  - 设置padding值，不会撑宽盒子
  - 设置margin值，会往中间挤

- 行内元素只能设置左右的内外边距，不能设置上下的内外边距

- margin：0  auto； 只能使设置了宽度的块元素水平居中

- text-align：center；

  - 可以使 **块元素** 和 **行内块元素** 里边的文字，行内元素，行内块元素水平居中
  - 用在行内元素上无效

- 两个嵌套关系的块元素

  - 如果父元素没有上内边距及边框，则父元素的上外边距会与子元素的上外边距发生合并合并后的外边距为两者中的较大者，合并到父元素上，即使父元素的上外边距为0，也会发生合并。

  - **解决方案：**

    1. 可以为父元素定义1像素的上边框或上内边距
2. 可以为父元素添加overflow：hidden；（推荐使用：触发BFC，独立的布局区域，不会受到外界元素的干扰）
    3. 浮动 

    

### nth-   选择器

- nth-child(n):当前容器所有子元素中的第N个

  - .box  li:nth-child(1)；BOX容器所有子元素中的第一个并且标签名是LI的 

- nth-of-type(n)：先给当前容器按照某一个标签名进行分组，获取组中的第N个

  - .box  li:nth-of-type（1）：先获取BOX中所有的LI，再获取LI中的第一个

  - .box  li:nth-of-type（even）{  background：blue；}                              

    ​    （EVEN  偶数  ODD  奇数     隔行变色）




### **占位符选择器**

>  **E::placeholder {}** ,  修改占位符样式



### 属性选择器

```css
	/*通过属性来选择标签*/
	a[href] {
		color: red;
	}
	div[class] {
		color: pink;
	}

	/*通过完整的属性值,来选择标签*/
	[href="abc.html"] {
		font-size: 50px;
		color: yellow;
	}
	[type="text"] {
		font-size: 30px;
		border: 1px solid red;
	}

	/*通过属性后边的值以某些字符开头来选择标签*/
	[href^="a"] { 
		font-size: 30px;
		color: orange;
	}

	/*通过属性后边的值以某些字符结尾来选择标签*/
	[href$="l"] {
		font-size: 50px;
		color: orange;
	}

	/*通过属性后边的值包含某些字符来选择标签*/
	[href*="b"] {
		color: red;
		font-size: 100px;
	}
```



### ICO图标

- 网址后加   /favicon.ico     可以得到该网站的ico图标
- 引入ico图标：<link rel="icon" href="favicon.ico" />     

- 转换ico图标： http://www.bitbug.net/        比特虫网站。




### box-shadow 阴影

- 第一个值是阴影的水平偏移量
- 第二个值是阴影的垂直偏移量
- 第三个值的阴影的模糊范围，没有负值
- 第四个值是阴影的大小
- 第五个值是阴影的颜色
- 阴影默认是外阴影

内阴影：box-shadow : inset  0 0 0 0 #333 ;

多组阴影用逗号隔开 :  box-shadow : 0 0 30px 0 red, inset 0 0 150px green;



###透明度

取值范围是0-1，0.1的0可以省略掉（ .1 ）

- rgba

  控制单颜色的透明

- opacity

  控制元素整体透明度,子元素也会透明

  

### input去除默认边框

border : 0 ;

outline : 0 ;



###Float  浮动

- 特点

  1. 浮动的元素脱离文档流的控制，不占据原来的位置

  2. 浮动可以使块元素在一行上显示

  3. 浮动只能浮动到父元素的左边和右边，会受到父元素内边距的约束

  4. 浮动元素顶对齐，代码换行不会生成缝隙

  5. 浮动元素有了行内块的显示特点

     - 块元素浮动后，不会默认默认父元素的宽度了，默认宽高为0，内容会撑开宽高
     - 行内元素浮动之后可以设置宽高了

  6. 浮动元素只会影响下边的元素，不会影响上边不浮动的文档流里边的块元素




###定位

让盒子垂直水平居中

```css
.son{
    position:absolute;
  	//这种方法子元素必须是设置的宽高，内容撑开的宽高无效！
  	left:0;
  	right:0;
  	top:0;
  	bottom:0;
  	margin:auto;
  	width:100px;
  	height:100px;
  	background-color:red;
}
```



### 鼠标样式

```css
cursor: default     默认值
		pointer		点击小手
		text		文本
		move		移动
		help		帮助
		not-allowed 禁止
```



### 清除图片底部缝隙

方法一：将vertical-align的值，设置为除baseline以外的值

方法二：将图片设置为块元素



### 字体图标

1. 下载字体图标，复制到字体文件夹（fonts）
2. 找到说明文件demo_index.html
3. 按照说明文件复制到css（注意路径）
4. 定义类名，使用字体图标（.inconfont）
5. 哎标签里边复制字体图标编码，调用.iconfont


  **推荐网站： http://icomoon.io**



### logo优化

- logo  里面 首先放一个 h1 标签 ，目的是为了提权，告诉搜索引擎，这个地方很重要
- h1里面在放一个链接，   给链接一个 大小 和  logo 的背景图片
- 链接里面要放文字，  但是文字不要显示出来， 要用 text-indent  移到盒子外面 （text-indent: -9999px)   然后overflow:hidden
- 最后给链接一个 title  这样鼠标放到logo 上，  就可以看到提示文字了




### 精灵图

 1.提高页面的加载速度
 2.减轻服务器的压力，减少请求次数



### z-index

 提高元素的层级，必须设置定位的元素才能生效



### 边框细线技巧

给li   margin-left :  -1px ;   margin-top: -1px ;  让li重合



### 过渡  transition

- transition-property：all；                  那些属性需要过渡
- transition-duration：1s；                  过渡时间
- transition-timing-function：linear；过渡的时间曲线
- transition-delay：100ms；                过渡的延迟

> 过渡的连写，过渡时间为必写，其他的不写取默认
>
> transition：all  1s  linear  100ms ；



###  CSS W3C 统一验证工具

CssStats 是一个在线的 CSS 代码分析工具

```
网址是：  http://www.cssstats.com/
```

W3C 统一验证工具：    http://validator.w3.org/unicorn/     可以检测本地文件



### CSS 压缩

通过上面的检测没有错误，为了提高加载速度和节约空间（相对来说，css量很少的情况下，几乎没啥区别），可以通过css压缩工具把css进行压缩。还可以去站长之家进行快速压缩。

 http://tool.chinaz.com/Tools/CssFormat.aspx  



### 图片规范

### - 内容图

- 优先考虑 JPEG 格式，条件允许的话优先考虑 WebP 格式
- 尽量不使用PNG格式，PNG8 色位太低，PNG24 压缩率低，文件体积大
- **PC平台单张的图片的大小不应大于 200KB。**

### - 背景图

​	背景图多为图标等颜色比较简单、文件体积不大、起修饰作用的图片

- PNG 与 GIF 格式，优先考虑使用 PNG 格式,PNG格式允许更多的颜色并提供更好的压缩率
- 图像颜色比较简单的，如纯色块线条图标，优先考虑使用 PNG8 格式，避免不使用 JPEG 格式
- 图像颜色丰富而且图片文件不太大的（40KB 以下）或有半透明效果的优先考虑 PNG24 格式
- 图像颜色丰富而且文件比较大的（40KB - 200KB）优先考虑 JPEG 格式
- 条件允许的，优先考虑 WebP 代替 PNG 和 JPEG 格式




### 背景渐变

```css
自左向右:background-image: linear-gradient(to right,white, gray);
自右向左:background-image: linear-gradient(to left,white, gray);
自上向下:background-image: linear-gradient(to bottom,white, gray);
自下向上:background-image: linear-gradient(to top,white, gray);
注意:多组颜色之间逗号隔开
```

多背景图片

```css
background:url(test1.jpg) no-repeat  10px 20px/50px 60px,
	   url(test2.jpg) no-repeat  10px 20px/70px 90px,
	   url(test3.jpg) no-repeat  10px 20px/110px 130px #ccc;
	   多背景图片用逗号隔开 背景颜色只能设一次，前面的背景会叠在之后的背景之上，背景色要定义在最后一组
```



### 伪类和伪元素

- **伪类：**

  ​        用于已有元素处于某种状态时为其添加对应的样式，这个状态是根据用户行为而动态变化的。例如：当用户悬停在指定元素时，可以通过:hover来描述这个元素的状态，虽然它和一般css相似，可以为已有元素添加样式，但是它只有处于DOM树无法描述的状态下才能为元素添加样式，所以称为伪类

- **伪元素：**

  ​		用于创建一些不在DOM树中的元素，并为其添加样式。例如，我们可以通过:before来在一个元素之前添加一些文本，并为这些文本添加样式，虽然用户可以看见这些文本，但是它实际上并不在DOM文档中

  1. **::before/:before**
     :before在被选元素前插入内容。需要使用content属性来指定要插入的内容。被插入的内容实际上不在文档树中。
  2. **::after/:after**
     :after在被元素后插入内容，其用法和特性与:before相似。
  3. **::first-letter/:first-letter**
     :first-letter匹配元素中文本的首字母。被修饰的首字母不在文档树中。
  4. **::first-line/:first-line**
     :first-line匹配元素中第一行的文本。这个伪元素只能用在块元素中，不能用在内联元素中。
  5. **::selection**
     ::selection匹配用户被用户选中或者处于高亮状态的部分。在火狐浏览器使用时需要添加-moz前 缀。该伪元素只支持双冒号的形式。
  6. **::placeholder**
     ::placeholder匹配占位符的文本，只有元素设置了placeholder属性时，该伪元素才 能生效。
     该伪元素不是CSS的标准，它的实现可能在将来会有所改变，所以要决定使用时必须谨慎。
     在一些浏览器中（IE10和Firefox18及其以下版本）会使用单冒号的形式。

==伪类与伪元素的区别在于：有没有创建一个文档树(DOM tree)之外的元素==

- **伪元素使用单冒号还是双冒号：**
  	    css3规范中要求使用双冒号（::）表示伪元素，以此来区分伪类和伪元素，比如::before和::after等伪元素使用双冒号（::），:hover和:active伪类使用单冒号（:）。除了一些低于IE8版本的浏览器外，大部分浏览器都支持伪元素的双冒号(::)表示方法。
    		然而除了少部分伪元素如::backdrop必须使用双冒号（::），大部分伪元素都支持单冒号和双冒号的写法，比如::after，写成:after一样可以正常运行。
    		w3c标准中说到，虽然CSS3标准要求伪元素使用双冒号的写法，但也依然支持单冒号的写法。为了向后兼容，我们建议你在目前还是使用单冒号的写法。

