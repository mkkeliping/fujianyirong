# spring-boot
## spring boot简介
Spring Boot 是一个**轻量级框架**，可以完成基于 Spring 的应用程序的大部分配置工作，也就是Spring Boot 的目的是提供一组工具，以便快速构建容易配置的 Spring 应用程序。                           
官方定义：Spring Boot 使您能轻松地创建独立的、生产级的、基于 Spring 且能**直接运行的应用程序**。我们对 Spring 平台和第三方库有自己的看法，所以您从一开始只会遇到极少的麻烦。               
首先，它**有主见**，也就是它会根据现在流行默认配置一些变量。比如嵌入一个tomcat容器。其次，它**可定义**，可以根据自己喜好进行自定义springboot程序，
## spring 开始使用
### Starter
starter 是 Spring Boot 的一个重要组成部分，用于限制您需要执行的手动配置依赖项数量，也就是可以进行配置项目所需要的依赖项（比如 Maven POM）应用程序类型所独有的。所有 starter 都使用以下命名约定：       
* spring-boot-starter-web 用于构建 RESTful Web 服务，它使用 Spring MVC 和 Tomcat 作为嵌入式应用程序容器。
* spring-boot-starter-jdbc 用于建立 JDBC 连接池。它基于 Tomcat 的 JDBC 连接池实现。
[其他starter依赖项参考](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-starter)
### 自动配置
如果您允许的话，Spring Boot 会使用其 @EnableAutoConfiguration 注释自动配置您的应用程序。自动配置基于类路径中的 JAR 和定义 bean 的方式：Spring Boot 使用您在 CLASSPATH 中指定的 JAR，形成一个有关如何配置某个自动行为的观点。Spring Boot 使用您定义 bean 的方式来确定如何自动配置自身。例如，如果您为 JPA bean 添加了 @Entity 注释，Spring Boot 会自动配置 JPA，这样您就不需要 persistence.xml 文件。
## 编写HELLO WORLD
* 新建一个maven项目。第一种：详细参考[maven创建]()，第二种：利用sts直接创建一个spring starter boot项目，选取相应的依赖创建即可。
* pom解释：其中的<parent>表示它指定了 Spring Boot 父 POM，并包含常见组件的定义。您不需要手动配置这些组件。<dependency>她们告诉spring boot该程序是什么，然后spring会形成自己的观点，下载相关的依赖，plugin 插件生成该 Spring Boot 应用程序。解释：创建web项目，应用程序 starter spring-boot-starter-web。基于这个 starter，Spring Boot 形成了该应用程序的以下观点：使用 Tomcat 作为嵌入式 Web 服务器容器、使用 Hibernate 进行对象-关系映射 (ORM)、使用 Apache Jackson 绑定 JSON、使用 Spring MVC 作为 REST 框架。简单自定义：略，用时查资料。
* 创建可执行JAR。要在 Eclipse 中运行 Maven 构建，请右键单击 POM 文件并选择 Run As > Maven Build。在 Goals 文本字段中，输入 clean 和 package，然后单击 Run 按钮。这一步是打jar包，这个相当于整个项目，可以执行，也方便部署。
* 运行可执行jar。                                       
 **注:**           
 测试：run as maven build..      goals 输入 clean test <br> 
 打包：run as maven build..      goals 输入 clean package<br> 
 打包并发送到本地仓库：run as maven build..    goals 输入 clean install
 ## BUG调试
 问题描述：端口被占用，BUG页面显示                                    
 
 
 ![端口被占用](https://github.com/mkkeliping/fujianyirong/blob/master/picture/springbug1.png)          
 
解决方法：在src->main->resources目录下新建一个文件，名称为application.properties（这是SpringBoot统一的配置文件）加了以下一行内容：（取个电脑上可用的端口号，如下面的9527，看过星爷电影的都懂的）server.port = 9527。重新运行即可使用。
 




 
