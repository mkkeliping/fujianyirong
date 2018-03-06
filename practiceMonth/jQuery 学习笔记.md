# jQuery 教程
## jQuery简介
jQuery是“写的更少，但做的更多”的轻量级 JavaScript 库，基本可以完成操作：HTML 元素选取和元素操作、CSS 操作、HTML 事件函数、JavaScript 特效和动画、HTML DOM 遍历和修改、Utilities。
## jQuery使用
### 添加jQuery库
本地版添加：首先下载jQuery库，可去官网[下载](http://jquery.com/download/#Download_jQuery),其中development是开发版未压缩供开发使用，另一个是production是压缩版供成品使用。下载完成后利用下述代码把其加进来，或者可以利用从Google 或 Microsoft 加载 CDN jQuery 核心文件。
  ```.html
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
* 美元符号定义 jQuery，相当于把元素加进到jQuery
*  选择符（selector）“查询”和“查找” HTML 元素
*  jQuery 的 action() 执行对元素的操作  
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
   $("p").css("background-color","red")
   ```
   元素选择器的其他应用请参考：[用户手册](http://www.w3school.com.cn/jquery/jquery_ref_selectors.asphttp://www.w3school.com.cn/jquery/jquery_ref_selectors.asp)
### jQuery 事件
* jQuery 事件处理方法是 jQuery 中的核心函数，事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。术语由事件“触发”（或“激发”）经常会被使用。事件相当于条件语句，放到<head>部分，执行相关操作。
* jQuery 名称冲突：jQuery 使用 $ 符号作为 jQuery 的简介方式。如果其他也要用jQuery 的$符号那么就会有冲突，我们可以使用var jq=jQuery.noConflict()，帮助您使用自己的名称（比如 jq）来代替 $ 符号。这时就用jq作为标志函数
 注： 由于 jQuery 是为处理 HTML 事件而特别设计的，那么当您遵循以下原则时，您的代码会更恰当且更易维护：<br>
     把所有 jQuery 代码置于事件处理函数中<br>
     把所有事件处理函数置于文档就绪事件处理器中<br>
     把 jQuery 代码置于单独的 .js 文件中<br>
     如果存在名称冲突，则重命名 jQuery 库<br>
  
## jQuery效果

 **显示与隐藏效果**             
 
 ```.html
 $(selector).hide(speed,callback); 
 $(selector).show(speed,callback);
 $(selector).toggle(speed,callback);
  ```
selector表示选中的条件，比如选中段落，或者ID之类的东东，speed表示显示与隐藏的速度，可以取以下值："slow"、"fast" 或毫秒，可选的 callback 参数是隐藏或显示完成后所执行的函数名称。

 **淡入与淡出效果**
 ```
 $(selector).fadeIn(speed,callback); //淡入
 $(selector).fadeOut(speed,callback); //淡出
 $(selector).fadeToggle(speed,callback); //淡入与淡出切换
 $(selector).fadeTo(speed,opacity,callback); //加入透明度
 ```
 
 **滑动**
 ```
 $(selector).slideDown(speed,callback); //向下滑动
 $(selector).slideUp(speed,callback);   //向上滑动
 $(selector).slideToggle(speed,callback); //切换滑动
 ```
 
 **动画**
 ```
 $(selector).animate({params},speed,callback);
 ```
paramsb表示动画样式。对于params，可以直接写出变化的样式格式css，可以写出多个样式，也就是里面包括多种样式依次交换，也可以进行字体变化[详细](http://www.w3school.com.cn/jquery/jquery_animate.asp)

 **stop()**
 ```
 $(selector).stop(stopAll,goToEnd);
 ```
 stopAll,goToEnd都是默认false， stopAll表示即仅停止活动的动画，如果为false(默认)允许任何排入队列的动画向后执行，如果为TRUE表示所有的都停止。goToEnd 参数规定是否立即完成当前动画默认为false，不立即完成当前动画，如果为true表示立即完成当前动画，一步到位。
 
**jQuery Callback 函数**
   ```
   1:$("p").hide(1000);
     alert("The paragraph is now hidden");
   2:$("p").hide(1000,function(){
    alert("The paragraph is now hidden");
    });
   ```
 代码是按顺序执行的，第一种情况p没有隐藏提示框就会出来，为了避免这种事情，我们可以使用第二种情况Callback，把函数写在里面就会消失了再出现。
 
**jQuery 方法链接**          

Chaining 允许我们在一条语句中允许多个 jQuery 方法（在相同的元素上）如需链接一个动作，您只需简单地把该动作追加到之前的动作上。

## jQuery HTML
### jQuery获得内容和属性
jQuery DOM 操作:DOM = Document Object Model（文档对象模型）使得访问和操作元素属性变得容易。
text() - 设置或返回所选元素的文本内容
html() - 设置或返回所选元素的内容（包括 HTML 标记）
val() - 设置或返回表单字段的值，可以是自己输入的值。
attr("a") -a表示一个属性，比如herf等
这个表示可以获得id=text的文本内容、文本网页版、以及文本输入的信息和属性值。[参考文档](http://www.w3school.com.cn/jquery/jquery_dom_get.asp)
当然，可以获取，同样也可以进行修改，（）中的内容就是修改所要显示的文本。

* jQuery - 添加元素
append() - 在被选元素的**结尾**插入内容
prepend() - 在被选元素的**开头**插入内容
after() - 在被选元素**之后**插入内容
before() - 在被选元素**之前**插入内容

* jQuery - 删除元素
通过 jQuery，可以很容易地删除已有的 HTML 元素。
$("#div1").remove(); //删除，删完就没了
$("#div1").empty();  //删除被选元素的子元素。
$("p").remove(".italic"); //过滤被删除的元素，也就是删除时再访问一个条件。删除P文件的要删除所有class=.italic的文件。、

* jQuery - 获取并设置 CSS 类
通过 jQuery，可以很容易地对 CSS 元素进行操作。
addClass(.css名称) - 向被选元素添加一个或多个类
removeClass(.css名称) - 从被选元素删除一个或多个类
toggleClass(.css名称) - 对被选元素进行添加/删除类的切换操作样式css
css(.css名称) - 设置或返回样式属性

* jQuery - css() 方法
css("propertyname") 方法设置或返回被选元素的一个或多个样式属性。
css("propertyname","value"); //可以设置多个 CSS 属性

* jQuery - 尺寸：可以显示所选事务的尺寸。其他略
### jQuery 遍历
jQuery 提供了多种遍历 DOM 的方法。遍历方法中最大的种类是树遍历（tree-traversal）
* parent()//直接父节点
* parents()//所有的父节点
* parentsUntil()//介于两个给定元素之间的所有祖先元素
* children()//所有孩子
* find()//find() 方法返回被选元素的后代元素，一路向下直到最后一个后代，然后把样式给改了。
* siblings() //siblings() 方法返回被选元素的所有同胞元素
* next()//返回被选元素的下一个同胞元素
* nextAll()//回被选元素的所有跟随的同胞元素
* nextUntil()//返回介于两个给定参数之间的所有跟随的同胞元素。
* prev()//就是向前，与向后一样。
* prevAll()
* prevUntil()
* first(), last() 和 eq()，选中元素的第一个，最后一个或者等于。
## jQuery - AJAX 简介

