# maven
### maven简介
Maven是一个项目管理和综合工具，提供开发人员一个开发的周期，开发人员使用可以方便的进行创建报表，检查，构建和测试自动化设置。
Maven项目的结构和内容在一个XML文件中声明，pom.xml 项目对象模型（POM），这是整个Maven系统的基本单元，通过这个文件完成maven的功能操作。
maven最强大的功能就是能够自动下载项目依赖库，我们不需要下载相应jar包，当我们配置好后，maven可以为我们自动下载。
### maven安装
首先下载maven，下载完成后。打开myeclipse或者eclipse--->windows---->preferences---->搜索maven---->找到installation---->点击add
把文件加进来和tomcat差不多。
### maven本地库
Maven的本地资源库是用来存储所有项目的依赖关系(插件jar和其他文件，这些文件被Maven下载)到本地文件夹。很简单，当你建立一个Maven项目
所有相关文件将被存储在你的Maven本地仓库。可以打开你的maven看到。
### maven中央存储库
当你建立一个 Maven 的项目，Maven 会检查你的 pom.xml 文件，以确定哪些依赖下载。首先，Maven 将从本地资源库获得 Maven 的本地资源库依赖资
源，如果没有找到，然后把它会从默认的 [Maven 中央存储库](http://repo1.maven.org/maven2/)
### maven依赖机制
当创建一个maven文件时，首先扫描pom.xml,看到相关maven操作，首先搜索本地库，如果没有在搜索中央库，最后搜索远程仓库。
### maven pom
当创建一个maven项目时，会有且仅有一个pom.xml项目对象模型。这个项目中必须有三个必填字段: groupId（项目组的编号独一无二，就比如一家银行的所有项目、就相当于我们公司com.yirong.sx），artifactId(项目名称)，version（项目版本号，通常与项目组号连在一起，比如com.company.bank:consumer-banking:1.0）g关于是否继承父类，我们可以选择默认。
### maven生命周期
**构建生命周期**             
准备资源----->编译代码----->包装----->安装    开始创建项目时的周期：clean（清洁阶段）----->default(或 build)（依赖阶段）----->执行包
清洁生命周期：clean----->default(或 build)----->site           
默认（或生成）生命周期和网站的生命周期：[查看详细介绍](https://www.yiibai.com/maven/maven_build_life_cycle.html)          

### maven项目文档
在你的项目文件已构建完成。 Maven 会在 target  目录中创建一个 site 目录，Maven会使用一个文件处理引擎： Doxia，它将会读取多个源格式并将它们转换为通用文档模型文档。APT[纯文本文档格式](http://maven.apache.org/doxia/format.html)
XDoc	[Maven1.x 的文档格式]
(http://jakarta.apache.org/site/jakarta-site2.html)
FML	[用于常问问题(FQA)文件](http://maven.apache.org/doxia/references/fml-format.html)
XHTML	[可扩展HTML](http://en.wikipedia.org/wiki/XHTML)             
## maven BUG
问题描述：点击new---->project---->maven project---->在里面选择org.apache.maven.archetypes:maven-archetype-quickstart:jar:1.1t---->点击下一步会出现---->完成---->出现两个个方框提示找不到，错误提示为：Maven-Could not resolve artifact org.apache.maven.archetypes:maven-archetype-quickstart:jar:1.1。<br>
解决问题：我们可以打开myeclipse---->windows---->preferences---->搜索maven---->点击第一个---->添加第二个---->在第一行复制 ：http://repo1.maven.org/maven2/archetype-catalog.xml，第二行随便起个名字，完成即可。当新建maven项目时，选择自己起的名字就可以新建成功了。                  
![maven 新建bug解决图]()
