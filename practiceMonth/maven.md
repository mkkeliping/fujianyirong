# maven
## maven简介
Maven是一个项目管理和综合工具，提供开发人员一个开发的周期，开发人员使用可以方便的进行创建报表，检查，构建和测试自动化设置。
Maven项目的结构和内容在一个XML文件中声明，pom.xml 项目对象模型（POM），这是整个Maven系统的基本单元，通过这个文件完成maven的功能操作。
maven最强大的功能就是能够自动下载项目依赖库，我们不需要下载相应jar包，当我们配置好后，maven可以为我们自动下载。
## maven安装
首先下载maven，下载完成后。打开myeclipse或者eclipse--->windows---->preferences---->搜索maven---->找到installation---->点击add
把文件加进来和tomcat差不多。
## maven本地库
Maven的本地资源库是用来存储所有项目的依赖关系(插件jar和其他文件，这些文件被Maven下载)到本地文件夹。很简单，当你建立一个Maven项目
所有相关文件将被存储在你的Maven本地仓库。可以打开你的maven看到。
## maven中央存储库
当你建立一个 Maven 的项目，Maven 会检查你的 pom.xml 文件，以确定哪些依赖下载。首先，Maven 将从本地资源库获得 Maven 的本地资源库依赖资
源，如果没有找到，然后把它会从默认的 [Maven 中央存储库](http://repo1.maven.org/maven2/)
