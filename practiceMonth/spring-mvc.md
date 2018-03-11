##  Spring mvc简介
简单易用，不用浪费精力在框架上，尽量使用大众的框架。SPRING MVC框架是当前最优秀的框架，由于支持注解，易用性又有了进一步提高。在这里注意
struts，也是优秀的mvc框架。
## 核心类与接口
* DispatcherServlet   -- 前置控制器
* HandlerMapping接口 -- 处理请求的映射
接口的实现类有两种方式，一种是SimpleUrlHandlerMapping 通过配置文件，把一个URL映射到Controller另一种是：DefaultAnnotationHandlerMapping  通过注解，把一个URL映射到Controller类上
* HandlerAdapter接口 -- 处理请求的映射
AnnotationMethodHandlerAdapter类，通过注解，把一个URL映射到Controller类的方法上
* Controller接口 -- 控制器
由于我们使用了@Controller注解，添加了@Controller注解注解的类就可以担任控制器（Action）的职责,
所以我们并没有用到这个接口。
* HandlerInterceptor 接口--拦截器自己实现这个接口，来完成拦截器的工作。
* ViewResolver接口的实现类
UrlBasedViewResolver类 通过配置文件，把一个视图名交给到一个View来处理，InternalResourceViewResolver类，比上面的类，加入了JSTL的支持
* View接口JstlView类
* LocalResolver接口
* HandlerExceptionResolver接口 --异常处理  SimpleMappingExceptionResolver实现类
* ModelAndView类
