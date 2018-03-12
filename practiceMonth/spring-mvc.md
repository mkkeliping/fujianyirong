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
## 核心流程图
## DispatcherServlet说明
使用spring mvc，配置DispatcherServlet是第一步，这个与我所学习的SSH框架中的web.xml配置文件中的servlet配置一致。DispatcherServl是前置控制器，也是一个servlet，可以配置多个，作用是拦截相符的文件夹，把其分发到相应的controler(action)中来处理。
代码部分
```
<servlet>  
    <servlet-name>springMVC</servlet-name> // 多个DispatcherServlet配置通过名字来区别，每个都有上下文对象（WebApplicationContext）子容器）
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>//当有访问时，会保存在servletcontext中，也可以取出相关值  
    <init-param>  
        <param-name>contextConfigLocation</param-name>指明了配置文件的文件名，不使用默认配置文件名，而使用springMVC.xml配置文件。  
        <param-value>classpath*:/springMVC.xml</param-value> 这里可以有三种形式
        1. 不写,使用默认值:/WEB-INF/<servlet-name>-servlet.xml
        2、<param-value>/WEB-INF/classes/springMVC.xml</param-value>
        3、<param-value>classpath*:springMVC-mvc.xml</param-value>
        4、多个值用逗号分隔
    </init-param>  
    <load-on-startup>1</load-on-startup>//表示启动顺序，让这个Servlet随Servletp容器一起启动。
</servlet> 
<servlet-mapping>  
    <servlet-name>springMVC</servlet-name> //拦截成功后，去找这个名字
    <url-pattern>/</url-pattern> //拦截条件，如果是*.form就是拦截所有的以.form结尾的文件。拦截*.do、*.htm， 例如：/user/add.do传统简单实用。
</servlet-mapping>  
```
## 父子上下文
* 在我所学习SSH中有listening监听器。Spring会创建一个WebApplicationContext上下文，称为父上下文（父容器） ，保存在 ServletContext中。
* DispatcherServlet是一个Servlet,可以同时配置多个，每个 DispatcherServlet有一个自己的上下文对象（WebApplicationContext），称为子上下文（子容器）， 它也保存在 ServletContext中。
* 子上下文可以访问父上下文中的内容，但父上下文不能访问子上下文中的内容。
## springMVC-mvc.xml 配置文件片段讲解 
```.xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans  
    xmlns="http://www.springframework.org/schema/beans"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xmlns:tx="http://www.springframework.org/schema/tx"  
    xmlns:context="http://www.springframework.org/schema/context"    
    xmlns:mvc="http://www.springframework.org/schema/mvc"    
    xsi:schemaLocation="http://www.springframework.org/schema/beans   
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd   
    http://www.springframework.org/schema/tx   
    http://www.springframework.org/schema/tx/spring-tx-3.0.xsd  
    http://www.springframework.org/schema/context  
    http://www.springframework.org/schema/context/spring-context-3.0.xsd  
    http://www.springframework.org/schema/mvc  
    http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd">  
  
  
    <!-- 自动扫描的包名 -->  
    <context:component-scan base-package="com.app,com.core,JUnit4" ></context:component-scan>  
     注：这里是自动扫描包，扫描包中指定的类的注解，常用的注解有
        @Controller 声明Action组件
        @Service    声明Service组件    @Service("myMovieLister") 
        @Repository 声明Dao组件
        @Component   泛指组件, 当不好归类时. 
        @RequestMapping("/menu")  请求映射
        @Resource  用于注入，( j2ee提供的 ) 默认按名称装配，@Resource(name="beanName") 
        @Autowired 用于注入，(srping提供的) 默认按类型装配 
        @Transactional( rollbackFor={Exception.class}) 事务管理
        @ResponseBody
        @Scope("prototype")   设定bean的作用域
      
    <!-- 默认的注解映射的支持 -->  
    <mvc:annotation-driven />  
      注：这是一种简写模式，会自动注册DefaultAnnotationHandlerMapping与AnnotationMethodHandlerAdapter 两个bean，是spring MVC为@Controllers分           发请求所必须的
          数据绑定支持，@NumberFormatannotation支持，@DateTimeFormat支持，@Valid支持，读写XML的支持（JAXB），读写JSON的支持（Jackson）
          我们处理响应ajax请求时，就使用到了对json的支持，对action写JUnit单元测试时，要从spring IOC容器中取DefaultAnnotationHandlerMapping与             AnnotationMethodHandlerAdapter 两个bean，来完成测试，取的时候要知道是<mvc:annotation-driven />这一句注册的这两个bean。
    <!-- 视图解释类 -->  
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
        <property name="prefix" value="/WEB-INF/jsp/"/>  
        <property name="suffix" value=".jsp"/><!--可为空,方便实现自已的依据扩展名来选择视图解释类的逻辑  -->  
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />  
    </bean>  
      
    <!-- 拦截器 -->  
    <mvc:interceptors>  
        <bean class="com.core.mvc.MyInteceptor" />  
    </mvc:interceptors>  
      注：会为每一个HandlerMapping，注入一个拦截器。其实我们也可以手动配置为每个HandlerMapping注入一个拦截器。
    <!-- 对静态资源文件的访问  方案一 （二选一） -->  
    <mvc:default-servlet-handler/>  
      注：使用默认的Servlet来响应静态文件
    <!-- 对静态资源文件的访问  方案二 （二选一）-->  
    <mvc:resources mapping="/images/**" location="/images/" cache-period="31556926"/>  
    <mvc:resources mapping="/js/**" location="/js/" cache-period="31556926"/>  
    <mvc:resources mapping="/css/**" location="/css/" cache-period="31556926"/> 
    注：匹配URL  /images/**  的URL被当做静态资源，由Spring读出到内存中再响应http。
  
</beans>   
 
```
## 如何访问到静态的文件，如jpg,js,css
如果你的DispatcherServlet拦截"/"，为了实现REST风格，拦截了所有的请求，那么同时对.js,.jpg等静态文件的访问也就被拦截了
方法一：激活Tomcat的defaultServlet来处理静态文件，要写在DispatcherServlet的前面， 让 defaultServlet先拦截请求，这样请求就不会进入Spring了。应该性能最优吧。Tomcat, Jetty, JBoss, and GlassFish 自带的默认Servlet的名字 -- "default"。每种格式写一遍。
```
<servlet-mapping>   
    <servlet-name>default</servlet-name>  
    <url-pattern>*.jpg</url-pattern>     
</servlet-mapping>    
<servlet-mapping>       
    <servlet-name>default</servlet-name>    
    <url-pattern>*.js</url-pattern>    
</servlet-mapping>    
<servlet-mapping>        
    <servlet-name>default</servlet-name>       
    <url-pattern>*.css</url-pattern>      
</servlet-mapping>    
```
方法二：在spring3.0.4以后版本提供了mvc:resources ，
```.xml
<!-- 对静态资源文件的访问 -->     
<mvc:resources mapping="/images/**" location="/images/" />  
```
/images/```*```映射到ResourceHttpRequestHandler进行处理，location指定静态资源的位置.可以是web application根目录下、jar包里面，这样可以把静态资源压缩到jar包中。cache-period 可以使得静态资源进行web cache 
