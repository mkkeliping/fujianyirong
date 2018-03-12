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
```.xml
<servlet>  
    <servlet-name>springMVC</servlet-name> 
    // 多个DispatcherServlet配置通过名字来区别，每个都有上下文对象（WebApplicationContext）子容器）
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    //当有访问时，会保存在servletcontext中，也可以取出相关值  
    <init-param>  
        <param-name>contextConfigLocation</param-name>
        指明了配置文件的文件名，不使用默认配置文件名，而使用springMVC.xml配置文件。  
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
    <url-pattern>/</url-pattern> 
    //拦截条件，如果是*.form就是拦截所有的以.form结尾的文件。拦截*.do、*.htm， 例如：/user/add.do传统简单实用。
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
/images/```**```映射到ResourceHttpRequestHandler进行处理，location指定静态资源的位置.可以是web application根目录下、jar包里面，这样可以把静态资源压缩到jar包中。cache-period 可以使得静态资源进行web cache 
方法三：使用<mvc:default-servlet-handler/>
```.xml
使用<mvc:default-servlet-handler/>
```
会把"/```**```" url,注册到SimpleUrlHandlerMapping的urlMap中,把对静态资源的访问由HandlerMapping转到org.springframework.web.servlet.resource.DefaultServletHttpRequestHandler处理并返回.DefaultServletHttpRequestHandler使用就是各个Servlet容器自己的默认Servlet.spring会先执行order值比较小的.DefaultAnnotationHandlerMapping的order属性值是：0<mvc:resources/ >自动注册的 SimpleUrlHandlerMapping的order属性值是： 2147483646<mvc:default-servlet-handler/>自动注册 的SimpleUrlHandlerMapping 的order属性值是： 2147483647,所以先进行匹配DefaultAnnotationHandlerMapping再按照order 升序找。
## 请求如何映射到具体的Action中的方法
映射到action，有两种方法，一种是基于xml文件，利用SimpleUrlHandlerMapping、BeanNameUrlHandlerMapping进行Url映射和拦截请求。这种方式少用。
另一种采用注解映射，使用DefaultAnnotationHandlerMapping。
```.xml
<bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">
```
但前面我们配置了<mvc:annotation-driven />，他会自动注册这个bean,就不须要我们显示的注册这个bean了.以上都可以注入interceptors，实现权限控制等前置工作。并在action类上使用：@Controller,@RequestMapping("/user")进行映射到具体的action中。相当于学习的SSH中取消struts直接利用注解进行访问。
## Spring中的拦截器
* Spring为我们提供了：
 org.springframework.web.servlet.HandlerInterceptor接口，
 org.springframework.web.servlet.handler.HandlerInterceptorAdapter适配器，实现这个接口或继承此类，可以非常方便的实现自己的拦截器。
* 拦截器执行时间：Action之前执行:可以进行编码、安全控制等处理；生成视图之前执行：有机会修改ModelAndView；在afterCompletion中：可以根据ex是否为null判断是否发生了异常，进行日志记录。
* 拦截器执行方式Spring拦截器没有总的拦截器，拦截器相当于HandlerMapping级别的。拦截器执行方式：当一个请求执行时，首先进行HandlerMapping，查找有没有处理器处理这个请求，如果有就进行拦截器，拦截器完成后交给目标控制器。
* 使用拦截器：
```.xml
<mvc:interceptors>   
    <bean class="com.app.mvc.MyInteceptor" />   
</mvc:interceptors> //总拦截器，拦截所有url,为每个HandlerMapping配置一个拦截器，在映像中总会找到一个控制器，也就会执行拦截器

<mvc:interceptors >     
  <mvc:interceptor>     
        <mvc:mapping path="/user/*" /> <!-- /user/*  -->     
        <bean class="com.mvc.MyInteceptor"></bean>     
    </mvc:interceptor>     
</mvc:interceptors>  //总拦截器，拦截匹配url

<bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">        
 <property name="interceptors">        
     <list>        
         <bean class="com.mvc.MyInteceptor"></bean>       
     </list>        
 </property>        
</bean>   //HandlerMappint上的拦截器如果是REST风格的URL，静态资源就不会被拦截。因为我们精准的注入了拦截器。


```
注：  如果使用了<mvc:annotation-driven />， 它会自动注册DefaultAnnotationHandlerMapping 与AnnotationMethodHandlerAdapter 这两个bean,所以就没有机会再给它注入interceptors属性，就无法指定拦截器。当然我们可以通过人工配置上面的两个Bean，不使用 <mvc:annotation-driven />，就可以 给interceptors属性 注入拦截器了。其实我也不建议使用 <mvc:annotation-driven />，而建议手动写详细的配置文件，来替代 <mvc:annotation-driven />，这就控制力就强了。
## 如何实现全局的异常处理
总错误处理
```.xml
<bean id="exceptionResolver" class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">  
    <property name="defaultErrorView">     
        <value>/error/error</value>  
    </property>  
    <property name="defaultStatusCode">     
        <value>500</value>  
    </property>      
<property name="warnLogCategory">     
        <value>org.springframework.web.servlet.handler.SimpleMappingExceptionResolver</value>  
    </property>      
</bean>   
```
这里主要的类是SimpleMappingExceptionResolver类，和他的父类AbstractHandlerExceptionResolver类，我们可以将不同的异常映射到不同的jsp页面（通过exceptionMappings属性的配置）。也可以通过HandlerExceptionResolver接口，写一个自己的异常处理程序。spring的扩展性是很好的。也可以为所有的异常指定一个默认的异常提示页面（通过defaultErrorView属性的配置），如果所抛出的异常在exceptionMappings中没有对应的映射，则Spring将用此默认配置显示异常信息。
```.html
<%@ page language="java" contentType="text/html; charset=GBK"  
    pageEncoding="GBK"%>  
<%@ page import="java.lang.Exception"%>  
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">  
<html>  
<head>  
<meta http-equiv="Content-Type" content="text/html; charset=GBK">  
<title>错误页面</title>  
</head>  
<body>  
<h1>出错了</h1>  
<%   
Exception e = (Exception)request.getAttribute("exception");   //key是exception，也是在SimpleMappingExceptionResolver类默认指定的
out.print(e.getMessage());   
%>  
</body>  
</html>  
```
## 如何给spring3 MVC中的Action做JUnit单元测试
 使用了spring3 MVC后，给action做单元测试变得很方便, JUnitActionBase类是所有JUnit的测试类的父类,这是个JUnit测试类，我们可以new Request对象，来参与测试，太方便了。给request指定访问的URL，就可以请求目标Action了。
## 转发与重定向
可以通过redirect/forward:url方式转到另一个Action进行连续的处理。
可以通过redirect:url 防止表单重复提交 。写法如下：return "forward:/order/add"; return "redirect:/index.jsp";
带参数重定向RedirectAttributes
```.java
public String save(@ModelAttribute("group") Group group, RedirectAttributes redirectAttributes) {   
    accountManager.saveGroup(group);   
    redirectAttributes.addFlashAttribute("message", "操作成功"); //带参数的重定向
    return "redirect:/account/group/";   
}  
```
## 处理ajax请求
1. 引入jar包jackson-core-asl-1.7.2.jar  jackson-mapper-asl-1.7.2.jar
2. spring的配置文件中要有这一行，才能使用到spring内置支持的json转换。如果你手工把POJO转成json就可以不须要使用spring内置支持的json转换。    <mvc:annotation-driven />
3. 使用@ResponseBody注解
## 关于写几个配置文件的说明
有人把配置文件写两份，原有的applicationContext.xml，这个文件从spring2.0-2.5时一直在使用。别一个是新加的spring MVC的配置文件，springMVC相关的配置，数据源，事务相关配置都可以写在一个配置文件中。最好写一个。如果写两个，就会扫描两次，注意不要重复，写两个可能出现其他的异常。
## 如何取得Spring管理的bean 
方法一是利用web.xml中的servlet进行；另一种是在web.xml配置listening进行管理；做通用的方法是神器是
```.xml
<!-- 用于持有ApplicationContext,可以使用SpringContextHolder.getBean('xxxx')的静态方法得到spring bean对象 -->  
<bean class="com.xxxxx.SpringContextHolder" lazy-init="false" /> 
```
## 多视图控制器
略，用时再查资料
## <mvc:annotation-driven /> 到底做了什么工作
一句 <mvc:annotation-driven />实际做了以下工作：（不包括添加自己定义的拦截器）
```.xml
 <!-- 注解请求映射  -->  
   <bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">           
    <property name="interceptors">  
        <list>     
            <ref bean="logNDCInteceptor"/>   <!-- 日志拦截器，这是你自定义的拦截器 -->  
            <ref bean="myRequestHelperInteceptor"/>   <!-- RequestHelper拦截器，这是你自定义的拦截器-->    
            <ref bean="myPermissionsInteceptor"/>  <!-- 权限拦截器，这是你自定义的拦截器-->    
            <ref bean="myUserInfoInteceptor"/>  <!-- 用户信息拦截器，这是你自定义的拦截器-->    
        </list>           
    </property>           
</bean>      
<bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter">  
    <property name="messageConverters">     
        <list>     
            <ref bean="byteArray_hmc" />     
            <ref bean="string_hmc" />     
            <ref bean="resource_hmc" />     
            <ref bean="source_hmc" />     
            <ref bean="xmlAwareForm_hmc" />     
            <ref bean="jaxb2RootElement_hmc" />     
            <ref bean="jackson_hmc" />     
        </list>     
    </property>     
</bean>     
<bean id="byteArray_hmc" class="org.springframework.http.converter.ByteArrayHttpMessageConverter" /><!-- 处理.. -->  
<bean id="string_hmc" class="org.springframework.http.converter.StringHttpMessageConverter" /><!-- 处理.. -->  
<bean id="resource_hmc" class="org.springframework.http.converter.ResourceHttpMessageConverter" /><!-- 处理.. -->  
<bean id="source_hmc" class="org.springframework.http.converter.xml.SourceHttpMessageConverter" /><!-- 处理.. -->  
<bean id="xmlAwareForm_hmc" class="org.springframework.http.converter.xml.XmlAwareFormHttpMessageConverter" /><!-- 处理.. -->  
<bean id="jaxb2RootElement_hmc" class="org.springframework.http.converter.xml.Jaxb2RootElementHttpMessageConverter" /><!-- 处理.. -->  
<bean id="jackson_hmc" class="org.springframework.http.converter.json.MappingJacksonHttpMessageConverter" /><!-- 处理json-->  
```
注：springMVC.xml配置文件是核心[参考链接](http://elf8848.iteye.com/blog/875830/#)
