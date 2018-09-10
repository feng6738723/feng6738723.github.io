# css 页面渲染

层叠样式表 (**C**ascading **S**tyle **S**heets) 简单说就是如何修饰网页信息的显示样式。 

### 1. 简介

* CSS的作用 ：样式定义**如何显示** HTML 元素
* CSS的工作原理
* 规则，属性和值

```
选择符:  表示要定义样式的对象，可以是元素本身，也可以是一类元素或者制定名称的元素.
属性:   属性是指定选择符所具有的属性，它是css的核心，css2共有150多个属性
属性值： 属性值包括法定属性值及常见的数值加单位，如25px，或颜色值等。

说明：
1）每个CSS样式由两部分组成，即选择符和声明，声明又分为属性和属性值；
2）属性必须放在花括号中，属性与属性值用冒号连接。
3）每条声明用分号结束。
4）当一个属性有多个属性值的时候，属性值与属性值不分先后顺序。
5）在书写样式过程中，空格、换行等操作不影响属性显示。
```

***

***

***

### 2.样式表的创建(内部样式 外部样式 内联样式)及区别

##### A、内部样式 

```
语法：
<style type="text/css">
/*css语句*/
</style>

注：使用style标记创建样式时，最好将该标记写在<head></head>;
```

##### B、外部样式  

```
方法一：外部样式表的创建：
<link rel="stylesheet" type="text/css" href="目标文件的路径及文件名全称" />
说明：
使用link元素导入外部样式表时，需将该元素写在文档头部，即<head>与</head>之间。
rel（relation）：用于定义文档关联，表示关联样式表；
type：定义文档类型；


方法二：外部样式表的导入
<style type="text/css">
@import url(目标文件的路径及文件名全称);
</style>
注：@和import之间没有空格 url和小括号之间也没有空格；必须结尾以分号结束；
```

##### C、内联样式 （行间样式，行内样式，嵌入式样式） 

```
语法：<标签 style="属性：属性值;属性:属性值;"></标签>
```

***

***

***



### 3.样式表的优先级

A、内联样式表的优先级别最高 

B、内部样式表与外部样式表的优先级和书写的顺序有关，后书写的优先级别高。 



#### 两种引入外部样式表link和import之间的区别

```
差别1：本质的差别：link属于XHTML标签，而@import完全是CSS提供的一种方式。

差别2：加载顺序的差别：当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，而@import引用的CSS会等到页面全部被下载完再被加载。所以有时候浏览@import加载CSS的页面时开始会没有样式（就是闪烁），网速慢的时候还挺明显。

差别3：兼容性的差别：@import是CSS2.1提出的，所以老的浏览器不支持，@import只有在IE5以上的才能识别，而link标签无此问题。

差别4：使用dom(document object model文档对象模型 )控制样式时的差别：当使用javascript控制dom去改变样式的时候，只能使用link标签，因为@import不是dom可以控制的.
```

***

***

***

***

### 4.CSS选择符（选择器）

* 类型选择符，元素选择符/（element选择器	) 

```
语法：元素名称{属性：属性值；}

说明：

a)元素选择符就是以文档语言对象类型作为选择符，即使用结构中元素名称作为选择符。例如body、div、p,img,em,strong,span......等。

b)所有的页面元素都可以作为选择符;

用法：
1)如果想改变某个元素得默认样式时，可以使用类型选择符；
（如：改变一个div、p、h1样式）

2) 当统一文档某个元素的显示效果时，可以使用类型选择符
（如：改变文档所有p段落样式）
```

* id选择符，

```
语法：#id名{属性：属性值;}
说明：
A）当我们使用id选择符时，应该为每个元素定义一个id属性
如：<div id="div1"></div>
B）id选择符的语法格式是“#”加上自定义的id名
如：#box{width:300px; height:300px;}

C) 起名时要取英文名，不能用关键字：(所有的标记和属性都是关键字)
如：head标记
D）一个id名称只能对应文档中一个具体的元素对象，因为id只能定义页面中某一个唯一的元素对象。
E) 最大的用处：创建网页的外围结构。
```

* class选择符，

```
语法：.class名{属性：属性值;}
说明：
A）当我们使用class选择符时，应先为每个元素定义一个类名称
B）class选择符的语法格式是："如：<div class="top"></div>"
用法：class选择符更适合定义一类样式；
```

* 通配符，

```
语法：*{属性：属性值；}
说明：通配选择符的写法是“*”，其含义就是所有元素。
用法：常用来重置样式。
```

* 群组选择符 

```
语法：选择符1，选择符2，选择符3{属性：属性值;}
说明：当有多个选择符应用相同的样式时，可以将选择符用“，”分隔的方式，合并为一组。
```

* 包含选择符，

```
语法：选择符1 选择符2{属性：属性值;}
说明：选择符1和选择符2用空格隔开，含义就是选择符1中包含的所有选择符2;
用法：当我的元素存在父级元素的时候，我要改变自己本身的样式，可以不另加选择符，直接用包含选择器的方式解决。
```

* 伪类选择符(伪类选择符CSS中已经定义好的选择器,不能随便取名)，

```
语法 ：
a:link{属性：属性值;}超链接的初始状态;
a:visited{属性：属性值;}超链接被访问后的状态;
a:hover{属性：属性值;}鼠标悬停，即鼠标划过超链接时的状态;
a:active{属性：属性值;}超链接被激活时的状态，即鼠标按下时超链接的状态;
要让他们遵守一个爱恨原则LoVe/HAte,也就是Link--visited--hover--active。
说明：
A）当这4个超链接伪类选择符联合使用时，应注意他们的顺序，正常顺序为：
a:link,a:visited,a:hover,a:active,错误的顺序有时会使超链接的样式失效；
B）为了简化代码，可以把伪类选择符中相同的声明提出来放在a选择符中；
例如：a{color:red;} a:hover{color:green;} 表示超链接的三种状态都相同，只有鼠标划过变颜色。伪对象选择符(设置在对象后发生的内容。用来和content属性一起使用 ) 

```

* 伪对象选择符(设置在对象后发生的内容。用来和content属性一起使用 ) 

##### CSS选择符的权重

css中用四位数字表示权重，权重的表达方式如：0，0，0，0 

类型选择符的权重为0001 

class选择符的权重为0010 

id选择符的权重为0100

 伪类选择符的权重为0001  

包含选择符的权重：为包含选择符的权中之和

 内联样式的权重为1000 

```
* 当不同选择符的样式设置有冲突的时候，高权重选择 符的样式会覆盖低权重选择符的样式。

例如：b .demo的权重是1+10=11
.demo的权重是10
所以经常会发生.demo的样式失效

* 相同权重的选择符，样式遵循就近原则：哪个选择符最后定义，就采用哪个选择符样式。 （注意：是css样式中定义该选择符的先后，而不是html中使用先后）
```



*****





### 5.浮动属性的简单应用

语法：float:none/left/right;

float:定义网页中其它文本如何环绕该元素显示 
浮动的目的：就是让竖着的东西横着来 
有三个取值：
left:元素活动浮动在文本左面
right:元素浮动在右面
none:默认值，不浮动。

### 1. Display(显示) 与 Visibility（可见性）

隐藏一个元素可以通过把display属性设置为"none"，或把visibility属性设置为"hidden"。但是请注意，这两种方法会产生不同的结果。

display:none可以隐藏某个元素，且隐藏的元素不会占用任何空间。也就是说，该元素不但被隐藏了，而且该元素原本占用的空间也会从页面布局中消失 

visibility:hidden可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间。也就是说，该元素虽然被隐藏了，但仍然会影响布局。

### 2.Display - 关于块级元素和行级元素的总结

* 1.**块级元素(block)特性：**
  - 总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示;
  - 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制;
* **块级元素主要有：**
  -  address , blockquote , center , dir , div , dl , fieldset , form , h1 , h2 , h3 , h4 , h5 , h6 , hr , isindex , menu , noframes , noscript , ol , p , pre , table , ul , li
* 2.**内联元素(inline)特性：**
  * 内联元素只需要必要的宽度，不强制换行。
  * 和相邻的内联元素在同一行;
  * 宽度(width)、高度(height)、内边距的top/bottom(padding-top/padding-bottom)和外边距的top/bottom(margin-top/margin-bottom)都不可改变，就是里面文字或图片的大小;
* **内联元素主要有：**
  - a , abbr , acronym , b , bdo , big , br , cite , code , dfn , em , font , i , img , input , kbd , label , q , s , samp , select , small , span , strike , strong , sub , sup ,textarea , tt , u , var

**可变元素(根据上下文关系确定该元素是块元素还是内联元素)：**

- applet ,button ,del ,iframe , ins ,map ,object , script

**CSS中块级、内联元素的应用：**

利用CSS我们可以摆脱上面表格里HTML标签归类的限制，自由地在不同标签/元素上应用我们需要的属性。

主要用的CSS样式有以下三个：

- display:block  -- 显示为块级元素
- display:inline  -- 显示为内联元素
- display:inline-block -- 显示为内联块元素，表现为同行显示并可修改宽高内外边距等属性

我们常将<ul>元素加上display:inline-block样式，原本垂直的列表就可以水平显示了。



##### 3.如何改变一个元素显示

* 把列表项显示为内联元素   li {display:inline;} 

  * ````
    li{display:inline;}
    </style>
    </head>
    <body>
    
    <p>链接列表水平显示：</p>
    
    <ul>
    <li><a href="/html/" target="_blank">HTML</a></li>
    <li><a href="/css/" target="_blank">CSS</a></li>
    <li><a href="/js/" target="_blank">JavaScript</a></li>
    <li><a href="/xml/" target="_blank">XML</a></li>
    </ul>
    ````

  * ![1530329410034](C:\Users\44903\AppData\Local\Temp\1530329410034.png)

* 把span元素作为块元素   span {display:block;} 

  * ```
    span
    {
    	display:block;
    }
    </style>
    </head>
    <body>
    
    <h2>Nirvana</h2>
    <span>Record: MTV Unplugged in New York</span>
    <span>Year: 1993</span>
    <h2>Radiohead</h2>
    <span>Record: OK Computer</span>
    <span>Year: 1997</span>
    ```

  * ![1530329469328](C:\Users\44903\AppData\Local\Temp\1530329469328.png)

***



### 6.颜色（color） 

* 如何定义颜色
* 颜色术语和背景
* 背景色

### 7.文本（text / font）

* 文本颜色

  * 颜色属性被用来设置文字的颜色。颜色是通过CSS最经常的指定

    - ```
      十六进制值 - 如: ＃FF0000
      一个RGB值 - 如: RGB(255,0,0)
      颜色的名称 - 如: red
      ```

* 文本的大小（font-size )   属性设置文本的大小 

  * ```
    字体大小的值可以是绝对或相对的大小。
    绝对大小：
    设置一个指定大小的文本
    不允许用户在所有浏览器中改变文本大小
    确定了输出的物理尺寸时绝对大小很有用
    相对大小：
    相对于周围的元素来设置大小
    允许用户在浏览器中改变文字大小
    Remark 如果你不指定一个字体的大小，默认大小和普通文本段落一样，是16像素（16px=1em）。
    ```

  * ```
    h1 {font-size:40px;}
    h2 {font-size:30px;}
    p {font-size:14px;}
    ```

* 字型（font- family）设置文本的字体系列。 

  * font-family 属性应该设置几个字体名称作为一种"后备"机制，如果浏览器不支持第一种字体，他将尝试下一种字体。

  * ```
    font-family 属性应该设置几个字体名称作为一种"后备"机制，如果浏览器不支持第一种字体，他将尝试下一种字体。
    
    p{font-family:"Times New Roman", Times, serif;}
    ```

* 斜体  (font-style:italic  )   粗体 (font-weight ) 

* 下划线( text-decoration)  从设计的角度主要是用来删除链接的下划线 

  * ```
    h1 {text-decoration:overline;}
    h2 {text-decoration:line-through;}
    h3 {text-decoration:underline;}
    ```

* 行间距(line-height)、字母间距(letter-spacing)和单词间距(word-spacing)

* 对齐方式    (text-align)   文本可居中或对齐到左或右,两端对齐 

  * ```
    h1 {text-align:center;}
    p.date {text-align:right;}
    p.main {text-align:justify;}
    ```

* 缩进  (text-ident)    文本缩进属性是用来指定文本的第一行的缩进。 

  * ```
    p {text-indent:50px;}
    ```

* 链接样式（:link / :visited / :active / :hover）

  * ```
    a:link {color:#000000;}      /* 未访问链接*/
    a:visited {color:#00FF00;}  /* 已访问链接 */
    a:hover {color:#FF00FF;}  /* 鼠标移动到链接上 */
    a:active {color:#0000FF;}  /* 鼠标点击时 */
    ```

  * 

* CSS3新属性

  - 投影
  - 首字母和首行文本(p:first-letter / p:first-line)
  - 响应用户



****



### 8.盒子（box model）

所有HTML元素可以看作盒子，CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。

盒模型允许我们在其它元素和周围元素边框之间的空间放置元素。

下面的图片说明了盒子模型(Box Model)：

 ![CSS box-model](http://www.runoob.com/images/box-model.gif)

```
Margin(外边距) - 清除边框外的区域，外边距是透明的。
Border(边框) - 围绕在内边距和内容外的边框。
Padding(内边距) - 清除内容周围的区域，内边距是透明的。
Content(内容) - 盒子的内容，显示文本和图像。
```

###### 元素的宽度和高度

当您指定一个CSS元素的宽度和高度属性时，你只是设置内容区域的宽度和高度。要知道，完全大小的元素，你还必须添加填充，边框和边距。.

下面的例子中的元素的总宽度为300px：

```
div {
    width: 300px;
    border: 25px solid green;
    padding: 25px;
    margin: 25px;
}

让我们自己算算：
300px (宽)
+ 50px (左 + 右填充)
+ 50px (左 + 右边框)
+ 50px (左 + 右边距)
= 450px
试想一下，你只有250像素的空间。让我们设置总宽度为250像素的元素:

div {
    width: 220px;
    padding: 10px;
    border: 5px solid gray;
    margin: 0; 
}

最终元素的总宽度计算公式是这样的：
总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距
元素的总高度最终计算公式是这样的：
总元素的高度=高度+顶部填充+底部填充+上边框+下边框+上边距+下边距
```

* 盒子大小的控制（width / height）
* 盒子的边框、外边距和内边距（border / margin / padding）
* 盒子的显示和隐藏（display / visibility）
* CSS3新属性
  * 边框图像（border-image）
  * 投影（border-shadow）
  * 圆角（border-radius）

### 边框border

 **border-style**属性用来定义边框的样式 

![1530327774668](C:\Users\44903\AppData\Local\Temp\1530327774668.png)

* 边框宽度 （border-width ）属性为边框指定宽度。 

  * 

  ```
  p.one
  {
      border-style:solid;
      border-width:5px;
  }
  p.two
  {
      border-style:solid;
      border-width:medium;
  }
  CSS 没有定义 3 个关键字的具体宽度，所以一个用户可能把 thick 、medium 和 thin 分别设置为等于 5px、3px 和 2px，而另一个用户则分别设置为 3px、2px 和 1px。
  ```

* 边框颜色  border-color属性用于设置边框的颜色.

  * 可以设置的颜色 

    ```
    name - 指定颜色的名称，如 "red"
    RGB - 指定 RGB 值, 如 "rgb(255,0,0)"
    Hex - 指定16进制值, 如 "#ff0000"
    
    p.one
    {
    	border-style:solid;
    	border-color:#0000ff;
    }
    p.two
    {
    	border-style:solid;
    	border-color:#ff0000 #0000ff;
    }
    p.three
    {
    	border-style:solid;
    	border-color:#ff0000 #00ff00 #0000ff;
    }
    p.four
    {
    	border-style:solid;
    	border-color:#ff0000 #00ff00 #0000ff rgb(250,0,255);
    }
    ```

  * ![1530328497007](C:\Users\44903\AppData\Local\Temp\1530328497007.png)

  *  border-color单独使用是不起作用的，必须得先使用border-style来设置边框样式。 

  * ```
    p.one
    {
        border-style:solid;
        border-color:red;
    }
    p.two
    {
        border-style:solid;
        border-color:#98bf21;
    }
    
    ```

    ![1530328543415](C:\Users\44903\AppData\Local\Temp\1530328543415.png)

* 单独设置每条边

  * border-style属性可以有1-4个值： 

  * ```
    border-style:dotted solid double dashed;
    上边框是 dotted
    右边框是 solid
    底边框是 double
    左边框是 dashed
    
    border-style:dotted solid double;
    上边框是 dotted
    左、右边框是 solid
    底边框是 double
    
    border-style:dotted solid;
    上、底边框是 dotted
    右、左边框是 solid
    
    border-style:dotted;
    四面边框是 dotted
    ```

  * 

### 9.列表，表格和菜单

* 列表的项目符号（list-style）
* 表格的边框和背景（border-collapse）
* 表单控件的外观
* 表单控件的对齐
* 浏览器的开发者工具

### 10.图像

* 控制图像的大小（display: inline-block）

* 背景图像

  * background	 简写属性，作用是将背景属性设置在一个声明中 

    * ```
      body {background:#ffffff url('img_tree.png') no-repeat right top;}
      
      当使用简写属性时，属性值的顺序为：:
      background-color
      background-image
      background-repeat
      background-attachment  指(背景图像是否固定或者随着页面的其余部分滚动。)
      background-position
      以上属性无需全部使用，你可以按照页面的实际需要使用.
      ```

    * 

  * background-color   (定义了元素的背景颜色.) 

    * CSS中，颜色值通常以以下方式定义:
      - 十六进制 - 如："#ff0000"
      - RGB - 如："rgb(255,0,0)"
      - 颜色名称 - 如："red"

  * background-image    (描述了元素的背景图像) 

    * ```
      body {background-image:url('paper.gif');}
      ```

  * background-repeat  设置不让图像平铺  设置背景图像是否及如何重复 

    * ```
      body
      {
      background-image:url('img_tree.png');
      background-repeat:no-repeat;
      }
      ```

  * background-position   (设置背景图像的起始位置）

    * ```
      body
      {
      background-image:url('img_tree.png');
      background-repeat:no-repeat;
      background-position:right top;
      }
      ```

* 对齐图像

### 11.布局

* 控制元素的位置（position / z-index
  - 普通流
  - 相对定位
  - 绝对定位
  - 固定定位
  - 浮动元素（float / clear）
* 网站布局
  - HTML5布局
* 适配屏幕尺寸
  - 固定宽度布局
  - 流体布局
  - 布局网格