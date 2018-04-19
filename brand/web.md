## 前端界面知识点
### jsp前端三阶段
```.jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```
* 一阶段是利用pageEncoding把其服务器在将JSP文件编译成.java文件时会根据pageEncoding的设定读取jsp
* 二阶段是Servlet文件（.java）到Java字节码文件（.class），默认是UTF-8
* 三阶段是从服务器到浏览器，这在一过程中用到的指令是contentType这里输出是用户看到的界面主要用到contentType和charset
### 界面显示大小设置
```.jsp
 <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```
* viewport是设置以适应不同尺寸的屏幕界面，content=""。
* width=device-width，这个是设置宽度为设备的宽度，
* initial-scale=1是设置初始缩放。即页面初始缩放程度。这是一个浮点值，是页面大小的一个乘数。例如，如果你设置初始缩放为“1.0”，
那么，web页面在展现的时候就会以target density分辨率的1:1来展现。如果你设置为“2.0”，那么这个页面就会放大为2倍。
* maximum-scale最大缩放。即允许的最大缩放程度。浮点值，用以指出页面大小与屏幕大小相比的最大乘数。例如，如果你将这个值设置为“2.0”
那么这个页面与target size相比，最多能放大2倍



