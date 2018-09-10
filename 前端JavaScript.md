# JavaScript控制行为操作

JavaScript 是 Web 的编程语言。所有现代的 HTML 页面都使用 JavaScript。

JavaScript web 开发人员必须学习的 3 门语言中的一门：

1. **HTML** 定义了网页的内容
2. **CSS** 描述了网页的布局
3. **JavaScript** 网页的行为

#### JavaScript基本语法

- 语句

  - JavaScript 语句是发给浏览器的命令。这些命令的作用是告诉浏览器要做的事情。

  - ```
    document.getElementById("demo").innerHTML = "你好 Dolly";
    ```

    分号 ;

    * 分号用于分隔 JavaScript 语句。通常我们在每条可执行的语句结尾添加分号

  | 语句         | 描述                                                         |
  | ------------ | ------------------------------------------------------------ |
  | break        | 用于跳出循环。                                               |
  | catch        | 语句块，在 try 语句块执行出错时执行 catch 语句块。           |
  | continue     | 跳过循环中的一个迭代。                                       |
  | do ... while | 执行一个语句块，在条件语句为 true 时继续执行该语句块。       |
  | for          | 在条件语句为 true 时，可以将代码块执行指定的次数。           |
  | for ... in   | 用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。 |
  | function     | 定义一个函数                                                 |
  | if ... else  | 用于基于不同的条件来执行不同的动作。                         |
  | return       | 退出函数                                                     |
  | switch       | 用于基于不同的条件来执行不同的动作。                         |
  | throw        | 抛出（生成）错误 。                                          |
  | try          | 实现错误处理，与 catch 一同使用。                            |
  | var          | 声明一个变量。                                               |
  | while        | 当条件语句为 true 时，执行语句块。                           |

- 注释

  - 单行注释以 // 开头。 
  - 多行注释以 /* 开始，以 */ 结尾。 

* 变量和数据类型      （变量是用于存储信息的"容器"）

  * 声明和赋值及命名规则      （使用 var 关键词来声明变量 ）

    * 变量必须以字母开头

    * 变量也能以 $ 和 _ 符号开头（不过我们不推荐这么做）

    * 变量名称对大小写敏感（y 和 Y 是不同的变量）

    * 一条语句中声明很多变量。该语句以 var 开头，并使用逗号分隔变量即可 

      * ```
        var lastname="Doe", age=30, job="carpenter";
        
        一条语句中声明的多个可以赋同一个值:
        var x,y,z=1;
        ```

  * 简单数据类型和复杂数据类型

    * 字符串（String）、数字(Number)、布尔(Boolean)、数组(Array)、对象(Object)、空（Null）、未定义（Undefined）。 

* 表达式和运算符   运算符 = 用于给 JavaScript 变量赋值。算术运算符 + 用于把值加起来。

  **运算符 = 用于赋值。**

  **运算符 + 用于加值。**

  - 赋值运算符

    赋值运算符用于给 JavaScript 变量赋值。

    给定 **x=10** 和 **y=5**，下面的表格解释了赋值运算符：

  | 运算符 | 例子 | 等同于 | 运算结果 |
  | ------ | ---- | ------ | -------- |
  | =      | x=y  |        | x=5      |
  | +=     | x+=y | x=x+y  | x=15     |
  | -=     | x-=y | x=x-y  | x=5      |
  | *=     | x*=y | x=x*y  | x=50     |
  | /=     | x/=y | x=x/y  | x=2      |
  | %=     | x%=y | x=x%y  | x=0      |

  - 算术运算符   y=5，下面的表格解释了这些算术运算符： 

  | 运算符 | 描述         | 例子          | x 运算结果 | y 运算结果 |
  | ------ | ------------ | ------------- | ---------- | ---------- |
  | +      | 加法         | x=y+2         | 7          | 5          |
  | -      | 减法         | x=y-2         | 3          | 5          |
  | *      | 乘法         | x=y*2         | 10         | 5          |
  | /      | 除法         | x=y/2         | 2.5        | 5          |
  | %      | 取模（余数） | x=y%2         | 1          | 5          |
  | ++     | 自增         | x=++y   x=y++ | 6          | 6          |
  |        |              | x=y++         | 5          | 6          |
  | --     | 自减         | x=--y         | 4          | 4          |
  |        |              | x=y--         | 5          | 4          |

  - 比较运算符

    比较运算符在逻辑语句中使用，以测定变量或值是否相等。

    x=5，下面的表格解释了比较运算符：

  | 运算符 | 描述                                               | 比较    | 返回值  |
  | ------ | -------------------------------------------------- | ------- | ------- |
  | ==     | 等于                                               | x==8    | *false* |
  |        |                                                    | x==5    | *true*  |
  | ===    | 绝对等于（值和类型均相等）                         | x==="5" | *false* |
  |        |                                                    | x===5   | *true*  |
  | !=     | 不等于                                             | x!=8    | *true*  |
  | !==    | 不绝对等于（值和类型有一个不相等，或两个都不相等） | x!=="5" | *true*  |
  |        |                                                    | x!==5   | *false* |
  | >      | 大于                                               | x>8     | *false* |
  | <      | 小于                                               | x<8     | *true*  |

  | >=   | 大于或等于 | x>=8 | *false |
  | ---- | ---------- | ---- | ------ |
  | <=   | 小于或等于 | x<=8 | *true  |

  - 逻辑运算符

    逻辑运算符用于测定变量或值之间的逻辑。

    给定 x=6 以及 y=3，下表解释了逻辑运算符：

  | 运算符 | 描述 | 例子                      |
  | ------ | ---- | ------------------------- |
  | &&     | and  | (x < 10 && y > 1) 为 true |
  | \|\|   | or   | (x==5 \|\| y==5) 为 false |
  | !      | not  | !(x==y) 为 true           |

* 分支结构

  - if…else...
  - switch…case…default...

* 循环结构

  - for循环
  - while循环
  - do…while循环

* 数组

  - 创建数组

    - 下面的代码创建名为 cars 的数组： 

    - ```
      1.常规方式: var cars=new Array();
              cars[0]="Saab";
              cars[1]="Volvo";
              cars[2]="BMW";
      
      2.简洁方式: (condensed array):
      	   var cars=new Array("Saab","Volvo","BMW");
      	   
      3: 字面: (literal array):
      		var cars=["Saab","Volvo","BMW"];
      ```

  - 操作数组中的元素  

  -  通过指定数组名以及索引号码，你可以访问某个特定的元素。 

    - ```
      以下实例可以访问myCars数组的第一个值：
      var name=myCars[0];
      
      以下实例修改了数组 myCars 的第一个元素:
      myCars[0]="Opel";
      ```

* 函数

  - 声明函数

    - 函数就是包裹在花括号中的代码块，前面使用了关键词 function： 

      - ```
        function functionname()
        {
        执行代码
        }
        ```

      - 可以在某事件发生时直接调用函数（比如当用户点击按钮时），并且可由 JavaScript 在任何位置进行调用。 

      - JavaScript 对大小写敏感。关键词 function 必须是小写的，并且必须以与函数名称相同的大小写来调用函数。 

      - **当您声明函数时，请把参数作为变量来声明**： 

      - ```
        function myFunction(var1,var2)
        {
        代码
        }
        ```

  - 调用函数及参数

    - 在调用函数时，您可以向其传递值，这些值被称为参数。

    - 这些参数可以在函数中使用。

    - 您可以发送任意多的参数，由逗号 (,) 分隔：

      - ```
        myFunction(argument1,argument2)
        ```

        **变量和参数必须以一致的顺序出现。第一个变量就是第一个被传递的参数的给定的值，以此类推。 **

  - 返回值

    - 有时，我们会希望函数将值返回调用它的地方。

      通过使用 return 语句就可以实现。

      在使用 return 语句时，函数会停止执行，并返回指定的值。

      * ``` 
        function myFunction()
        {
            var x=5;
            return x;
        }
        ```

      * ```
        var myVar=myFunction();
        myVar 变量的值是 5，也就是函数 "myFunction()" 所返回的值。
        即使不把它保存为变量，您也可以使用返回值：
        document.getElementById("demo").innerHTML=myFunction();
        "demo" 元素的 innerHTML 将成为 5，也就是函数 "myFunction()" 所返回的值。
        ```

      * 

  - 匿名函数

  - 立即调用函数

#### 面向对象

- 对象的概念
  - JavaScript 中的所有事物都是对象：字符串、数值、数组、函数... 
  - JavaScript 提供多个内建对象，比如 String、Date、Array 等等。 对象只是带有属性和方法的特殊数据类型。
    - 布尔型可以是一个对象。
    - 数字型可以是一个对象。
    - 字符串也可以是一个对象
    - 日期是一个对象
    - 数学和正则表达式也是对象
    - 数组是一个对象
    - 甚至函数也可以是对象
- 创建对象的字面量语法
- 访问成员运算符
- 创建对象的构造函数语法
  - this关键字
- 添加和删除属性
  - delete关键字
- 全局对象
  - Number / String / Boolean
  - Date / Math / RegEx / Array

#### BOM

- window对象的属性和方法
- history对像
  - forward() / back() / go()
- location对象
- navigator对象
- screen对象

***

***

#### DOM

- DOM树
- 访问元素
  - getElementById() / querySelector()
  - getElementsByClassName() / getElementsByTagName() / querySelectorAll()
  - parentNode / previousSibling / nextSibling / firstChild / lastChild
- 操作元素
  - nodeValue
  - innerHTML / textContent / createElement() / createTextNode() / appendChild() / removeChild()
  - className / id / hasAttribute() / getAttribute() / setAttribute() / removeAttribute()
- 事件处理
  - 事件类型
    - UI事件：load / unload / error / resize / scroll
    - 键盘事件：keydown / keyup / keypress
    - 鼠标事件：click / dbclick / mousedown / mouseup / mousemove / mouseover / mouseout
    - 焦点事件：focus / blur
    - 表单事件：input / change / submit / reset / cut / copy / paste / select
  - 事件绑定
    - HTML事件处理程序（不推荐使用，因为要做到标签与代码分离）
    - 传统的DOM事件处理程序（只能附加一个回调函数）
    - 事件监听器（旧的浏览器中不被支持）
  - 事件流：事件捕获 / 事件冒泡
  - 事件对象（低版本IE中的window.event）
    - target（低版本IE中的srcElement）
    - type
    - cancelable
    - preventDefault()
    - stopPropagation()（低版本IE中的cancelBubble）
  - 鼠标事件 - 事件发生的位置
    - 屏幕位置：screenX和screenY
    - 页面位置：pageX和pageY
    - 客户端位置：clientX和clientY
  - 键盘事件 - 哪个键被按下了
    - keyCode属性
    - String.fromCharCode(event.keyCode)
  - HTML5事件
    - DOMContentLoaded
    - hashchange
    - beforeunload

#### JavaScript API

- HTML5中的API：geolocation / localStorage / sessionStorage / history





# 使用jQuery

#### jQuery概述

1. Write Less Do More（用更少的代码来完成更多的工作）
2. 使用CSS选择器来查找元素（更简单更方便）
3. 使用jQuery方法来操作元素（解决浏览器兼容性问题、应用于所有元素并施加多个方法）

#### 引入jQuery

- 下载jQuery的开发版和压缩版
- 从CDN加载jQuery

```
<script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
<script>
    window.jQuery || 
        document.write('<script src="js/jquery-3.3.1.min.js"></script>')
</script>
```

#### 查找元素

* 选择器
  * \* / element / #id / .class / selector1, selector2
  * ancestor descendant / parent>child / previous+next / previous~siblings
* 筛选器
  - 基本筛选器：:not(selector) / :first / :last / :even / :odd / :eq(index) / :gt(index) / :lt(index) / :animated / :focus
  - 内容筛选器：:contains('…') / :empty / :parent / :has(selector)
  - 可见性筛选器：:hidden / :visible
  - 子节点筛选器：:nth-child(expr) / :first-child / :last-child / :only-child
  - 属性筛选器：[attribute] / [attribute='value'] / [attribute!='value'] / [attribute^='value'] / [attribute$='value'] / [attribute|='value'] / [attribute~='value']
* 表单：:input / :text / :password / :radio / :checkbox / :submit / :image / :reset / :button / :file / :selected / :enabled / :disabled / :checked

#### 执行操作

* 内容操作
  - 获取/修改内容：html() / text() / replaceWith() / remove()
  - 获取/设置元素：before() / after() / prepend() / append() / remove() / clone() / unwrap() / detach() / empty() / add()
  - 获取/修改属性：attr() / removeAttr() / addClass() / removeClass() / css()
  - 获取/设置表单值：val()
* 查找操作
  - 查找方法：find() / parent() / children() / siblings() / next() / nextAll() / prev() / prevAll()
  - 筛选器：filter() / not() / has() / is() / contains()
  - 索引编号：eq()
* 尺寸和位置
  - 尺寸相关：height() / width() / innerHeight() / innerWidth() / outerWidth() / outerHeight()
  - 位置相关：offset() / position() / scrollLeft() / scrollTop()
* 特效和动画
  - 基本动画：show() / hide() / toggle()
  - 消失出现：fadeIn() / fadeOut() / fadeTo() / fadeToggle()
  - 滑动效果：slideDown() / slideUp() / slideToggle()
  - 自定义：delay() / stop() / animate()
* 事件
  - 文档加载：ready() / load()
  - 用户交互：on() / off()

# jQuery

jQuery是一个JavaScript函数库。

jQuery是一个轻量级的"写的少，做的多"的JavaScript库。

jQuery库包含以下功能：

- HTML 元素选取
- HTML 元素操作
- CSS 操作
- HTML 事件函数
- JavaScript 特效和动画
- HTML DOM 遍历和修改
- AJAX
- Utilities

### Query插件

- jQuery Validation
- jQuery Treeview
- jQuery Autocomplete
- jQuery UI

#### 避免和其他库的冲突

先引入其他库再引入jQuery的情况。 

```
<script src="other.js"></script>
<script src="jquery.js"></script>
<script>
	jQuery.noConflict();
    jQuery(function() {
        jQuery('div').hide();
    });
</script>
```

先引入jQuery再引入其他库的情况。 

```
<script src="jquery.js"></script>
<script src="other.js"></script>
<script>
    jQuery(function() {
        jQuery('div').hide();
    });
</script>
```

#  Ajax

AJAX 是一种与服务器交换数据的技术，可以在不重新载入整个页面的情况下更新网页的一部分。 

- 原生的Ajax

下面的表格列出了所有的 jQuery AJAX 方法：

| 方法                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [$.ajax()](http://www.runoob.com/jquery/ajax-ajax.html)      | 执行异步 AJAX 请求                                           |
| $.ajaxPrefilter()                                            | 在每个请求发送之前且被 $.ajax() 处理之前，处理自定义 Ajax 选项或修改已存在选项 |
| [$.ajaxSetup()](http://www.runoob.com/jquery/ajax-ajaxsetup.html) | 为将来的 AJAX 请求设置默认值                                 |
| $.ajaxTransport()                                            | 创建处理 Ajax 数据实际传送的对象                             |
| [$.get()](http://www.runoob.com/jquery/ajax-get.html)        | 使用 AJAX 的 HTTP GET 请求从服务器加载数据                   |
| [$.getJSON()](http://www.runoob.com/jquery/ajax-getjson.html) | 使用 HTTP GET 请求从服务器加载 JSON 编码的数据               |
| [$.getScript()](http://www.runoob.com/jquery/ajax-getscript.html) | 使用 AJAX 的 HTTP GET 请求从服务器加载并执行 JavaScript      |
| [$.param()](http://www.runoob.com/jquery/ajax-param.html)    | 创建数组或对象的序列化表示形式（可用于 AJAX 请求的 URL 查询字符串） |
| [$.post()](http://www.runoob.com/jquery/ajax-post.html)      | 使用 AJAX 的 HTTP POST 请求从服务器加载数据                  |
| [ajaxComplete()](http://www.runoob.com/jquery/ajax-ajaxcomplete.html) | 规定 AJAX 请求完成时运行的函数                               |
| [ajaxError()](http://www.runoob.com/jquery/ajax-ajaxerror.html) | 规定 AJAX 请求失败时运行的函数                               |
| [ajaxSend()](http://www.runoob.com/jquery/ajax-ajaxsend.html) | 规定 AJAX 请求发送之前运行的函数                             |
| [ajaxStart()](http://www.runoob.com/jquery/ajax-ajaxstart.html) | 规定第一个 AJAX 请求开始时运行的函数                         |
| [ajaxStop()](http://www.runoob.com/jquery/ajax-ajaxstop.html) | 规定所有的 AJAX 请求完成时运行的函数                         |
| [ajaxSuccess()](http://www.runoob.com/jquery/ajax-ajaxsuccess.html) | 规定 AJAX 请求成功完成时运行的函数                           |
| [load()](http://www.runoob.com/jquery/ajax-load.html)        | 从服务器加载数据，并把返回的数据放置到指定的元素中           |
| [serialize()](http://www.runoob.com/jquery/ajax-serialize.html) | 编码表单元素集为字符串以便提交                               |
| [serializeArray()](http://www.runoob.com/jquery/ajax-serializearray.html) | 编码表单元素集为 names 和 values 的数组                      |

- 基于jQuery的Ajax

  - 加载内容

    * jQuery load() 方法

    * ``` 
      $(selector).load(URL,data,callback);
      
      必需的 URL 参数规定您希望加载的 URL。
      可选的 data 参数规定与请求一同发送的查询字符串键/值对集合。
      可选的 callback 参数是 load() 方法完成后所执行的函数名称
      ```

- jQuery get() 和 post() 方法 

  - 用于通过 HTTP GET 或 POST 请求从服务器请求数据。 

    - *GET* - 从指定的资源请求数据

    - *POST* - 向指定的资源提交要处理的数据

    - ```
      $.get(URL,callback);
      
      必需的 URL 参数规定您希望请求的 URL。
      可选的 callback 参数是请求成功后所执行的函数名。
      ```

    - ```
      $.post(URL,data,callback);
      
      必需的 URL 参数规定您希望请求的 URL。
      可选的 data 参数规定连同请求发送的数据。
      可选的 callback 参数是请求成功后所执行的函数名。
      ```

    - 