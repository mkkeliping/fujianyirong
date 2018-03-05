# jQuery 教程
## jQuery简介
jQuery是“写的更少，但做的更多”的轻量级 JavaScript 库，基本可以完成操作：HTML 元素选取和元素操作、CSS 操作、HTML 事件函数、JavaScript 特效和动画、HTML DOM 遍历和修改、Utilities。
## jQuery使用
### 添加jQuery库
本地版添加：首先下载jQuery库，可去官网[下载](http://jquery.com/download/#Download_jQuery),其中development是开发版未压缩供开发使用，另一个是production是压缩版供成品使用。下载完成后利用下述代码把其加进来，或者可以利用从Google 或 Microsoft 加载 CDN jQuery 核心文件。
```
<head>
<script type="text/javascript" src="jquery.js"></script> //本地加载jQuery库
</head>
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs //使用 Google 的 CDN
/jquery/1.4.0/jquery.min.js"></script>
</head>
<head>
<script type="text/javascript" src="http://ajax.microsoft.com/ajax/jquery //Microsoft 的 CDN
/jquery-1.4.min.js"></script>
</head>
```
### jQuery 语法
* 基础语法是：$(selector).action()
  美元符号定义 jQuery，相当于把元素加进到jQuery
  选择符（selector）“查询”和“查找” HTML 元素
  jQuery 的 action() 执行对元素的操作  
### jQuery 选择器
* 元素选择器
  ```
  jQuery 使用 CSS 选择器来选取 HTML 元素。
  $("p") 选取 <p> 元素。
  $("p.intro") 选取所有 class="intro" 的 <p> 元素。
  $("p#demo") 选取所有 id="demo" 的 <p> 元素。
  ```
* jQuery 属性选择器
  jQuery 使用 XPath 表达式来选择带有给定属性的元素。
 ```
  $("[href]") 选取所有带有 href 属性的元素。
  $("[href='#']") 选取所有带有 href 值等于 "#" 的元素。
  $("[href!='#']") 选取所有带有 href 值不等于 "#" 的元素。
  $("[href$='.jpg']") 选取所有 href 值以 ".jpg" 结尾的元素。
  ```
* jQuery CSS 选择器
  jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性。下面的例子把所有 p 元素的背景颜色更改为红色：
 ```
 $("p").css("background-color","red");
 ```
[用户手册](http://www.w3school.com.cn/jquery/jquery_ref_selectors.asphttp://www.w3school.com.cn/jquery/jquery_ref_selectors.asp)
