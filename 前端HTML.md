# HTML

超文本标记语言，标准通用标记语言下的一个应用。

“超文本”就是指页面内可以包含图片、链接，甚至音乐、程序等非文字元素。

结构包括“头”部分（英语：Head）、和“主体”部分（英语：Body），其中“头”部提供关于网页的信息，“主体”部分提供网页的具体内容  

### HTML网页结构

下面是一个可视化的网页结构：

![](http://ogjdtuxan.bkt.clouddn.com/html_struct.png) 

其中白色区域才是在网页中可见的部分

### 编码格式

目前在大部分浏览器中，直接输出中文会出现中文乱码的情况，这时候我们就需要在头部将字符声明为 UTF-8。  

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>页面标题</title>
</head>
<body>
 
<h1>我的第一个标题</h1>
 
<p>我的第一个段落。</p>
 
</body>
</html> 
```

### HTML&lt;head>元素

head&gt; 元素包含了所有的头部标签元素。在 &lt;head&gt;元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。

可以添加在头部区域的元素标签为: &lt;title>, &lt;style>, &lt;meta>, &lt;link>, &lt;script>, &lt;noscript>, &lt;base>.  

&lt;title> 		定义了文档的标题

&lt;base>		定义了页面链接标签的默认链接地址
&lt;link>       	定义了一个文档和外部资源之间的关系
&lt;meta>		定义了HTML文档中的元数据
&lt;script>		定义了客户端的脚本文件
&lt;style>	        定义了HTML文档的样式文件 

#### 1.文本

* 标题 <h1-h6> 和段落   <p></p>
* 粗体 <strong> 或<b>  和斜体  <em>或<i>
* 上标  <sup>  和下标  <sub>
* 语义化标记
  * 加粗  <b>  和强调 <strong>
  * 引用:   <cite>
  * 缩写词  <abbr>  和首字母缩写词
  * 定义地址  <address>  
  * 长的引用  <blockquote>
  * 所有者联系信息
  * 内容的修改

#### 2.列表（list）

* 有序列表（ordered list）  <ol> +  列表的描述 <li>
* 无序列表（unordered list)   <ul>  + 列表的描述  <li>
* 自定义列表（definition list）<dl>   + 列表的项目或名字 <dt>  + 列表的描述 <dd>

#### 3.链接（anchor）

* 页面链接   < a href= "url">*链接文本*</a> 
* 锚链接 < a href="#tips">返回id= tips元素点</a> 
* 功能链接

#### 4.图像（image）

* 图像储存位置    < img src=" url " alt="some_text"> 
* 图像高度及宽度   < img src="luolin.jpg" alt="Pulpit rock" width="100" height="100"> 

#### 5.表格（table）

* 基本的表格结构  
* 表格由 <table> 标签来定义，表头由<th>标签定义 行由 <tr> 标签定义 ，列由 <td> 标签定义 
* 表格的标题   <caption>
* 表格头内容   <thead>
* 表格主体   <tbody>
* 表格脚注   <tfoot>

#### 6.表单（form）

* 如何收集信息
* 表单控件（input）
  * 文本框  < input type="">
  * 密码框   < input type="password">  
  * 文本域   <input type="text">  
  * 单选按钮  <input type="radio"> 
  * 复选按钮  <input type="checkbox">   
  * 下拉按钮  <select>  + <optgroup> +  <option>  
  * 提交按钮  <input type="submit">  
  * 图像按钮  <input type="image"> 
  * 文件上传  <input type="file">
* 组合表单元素
  * 表单内的相关元素分组   <fieldset>
  * <legend>   为 <fieldset>元素定义标题 
* HTML5的表单控件
  * 日期    < input type="datetime" name="bdaytime"> 
  * 电子邮件    < input type="email" name="email"> 
  * URL     <input type="url" name="homepage"> 
  * 搜索  <input type="search" name="googlesearch"> 

#### 7. 音频视频（audio / video）

* 视频格式和播放器   
* 视频托管服务
* 添加视频的准备工作
* video标签和属性
* audio标签和属性

#### 8.其他

* 文档类型
* 注释  <!--  -->
* 属性
  * id
  * class
* 块级元素  /  行级元素
* 内联框架（internal frame）
* 页面信息（meta）
* 转义字符（实体替换符）





















