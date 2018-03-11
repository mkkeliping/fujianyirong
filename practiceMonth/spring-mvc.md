##  Spring mvc简介
简单易用，不用浪费精力在框架上，尽量使用大众的框架。SPRING MVC框架是当前最优秀的框架，由于支持注解，易用性又有了进一步提高。在这里注意
struts，也是优秀的mvc框架。
## 核心类与接口
* DispatcherServlet   -- 前置控制器
* HandlerMapping接口 -- 处理请求的映射
接口的实现类有两种方式，一种是SimpleUrlHandlerMapping 通过配置文件，把一个URL映射到Controller另一种是：DefaultAnnotationHandlerMapping  通过注解，把一个URL映射到Controller类上
