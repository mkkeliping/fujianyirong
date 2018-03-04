# git简介
Git是分布式版本控制系统（注意区别集中式和分布式。分布式相当于在你的电脑中不需要联网即可访问，集中是相当于网络中的星装结构）
# git安装
git可以在多个平台进行安装，在这主要描述window的安装。可以去官网下载安装包，也可以利用国内镜像下载，下载完点击安装。在安装过程中选择安装地点，其他一路点击继续即可，安装完成后可以点开开始键里面如果有git brach说明安装成功。在这里面即可输入git命令。<br>
安装成功后，还需要设置一下你的家门，第一次需要进行此命令操作，利用命令：
```
git config --global user.name Your Name  你的名字
git config --global user.email email@example.com你的邮箱
```
# 使用git
##  创建版本库
版本库又名仓库，英文名repository，也就是一个目录，可以利用git命令进行追踪。在本地创建版本库步骤：<br>
首先切换到要变成仓库的文件夹——————>使用命令git init把文件夹变成仓库——————>ls -ah 就可看到隐藏的文件夹.git,说明仓库创建成功。 注意不要破坏此文件结构。
##  添加到版本库
注：<br>
* 所有的版本控制系统只能追踪文本文件的修改，git依然如此。而图片，视频等一系列二进制文件不能追踪器文件的修改，图片也只能查看到其大小变化比如从几k到几k.
* 对于Windows用户来说一定不要用电脑自带的编辑器，原因百度。可以使用Notepad++来代替记事本。要把文本编辑器改为utf-8(上面文本栏编码一处可以进行修改)
<br>添加到版本库：
```
git add 文件名.txt(格式写上)//添加到版本库
git commit -m  提交的本次文件修改说明//提交文件，提交的说明要有意义。让人一目了然。
```
在添加文件和提交文件的过程中，添加文件需要一个一个进行添加，但是提交文件时可以一块进行提交。
## 版本回退
* 版本控制就像玩游戏，你不断的进行修改，不断的进行提交，每次提交就相当于拍个快照，对提交的内容进行一个简单的介绍。当你提交了多个版本，你想回到之前的版本时，怎么办那，可以利用命令
```
git log  //查看当前提交的所有版本
git log  --pretty=oneline//查看所有提交版本的简单形式，其中包含版本号ID，提交说明
git reset --hard HEAD 
//表示当前版本，后面多加一个^表示上一版本，为了方便表示可以利用HEAD~表示返回上几个版本，例如：HEAD~100
```
* 当我们返回到之前版本时，如果再想回来怎么办，我们可以进行以下操作：
```
git reset --hard ID号 //如果我们没有关闭代码栏，我们可以查看上面的ID.可以利用版本ID进行返回版本。
git reflog //查看你的所有操作。这个作用是我们关闭电脑或者找不到版本ID的情况下可以利用这个进行查看
```
注：版本变换可以这么快是因为Git内部有个指向当前版本的HEAD指针，当版本变换时只需要把指针进行变换即可，指针指向哪里版本号就定位在那里。<br>
当版本号进行变换
## 工作区和暂存区
工作区就是工作目录，是一个可以看到的工作空间。在仓库中可以把工作区和暂存区这么理解。我们mkdir todoList,然后git init todoList,这时，todoList中可以看到的就是工作区，在todoList仓库（版本库）中，有stage（或者叫index）的暂存区。还有创建仓库时就为我们创建好的分支master。
![工作区与暂存区工作流程图片](https://github.com/mkkeliping/fujianyirong/blob/master/picture/gitStatus.jpg)<br><br>
注：<br>
如图所示，要提交一个文件，必须从一个状态提交到另一个状态，不能跨状态进行提交。在工作去编辑了一个readme1，提交到暂存区，这时又修改了工作区变成readme2，当使用命令git commit命令进行提交时，提交的时readme1。
```.c
git checkout -- file  //没有提交到暂存区，回到工作区上一版本文件，是开始编辑的状态。
git checkout -- file   //提交到暂存区，在工作区进行修改，这时工作区回到提交到暂存区的状态
git reset HEAD file    //提交到暂存区，回到工作区，使之需要开始的一系列步骤，这时不在暂存区。
                        //一旦你提交到远程就不可以了，可能会被看到。
```
在不知道命令时可以利用git status命令查看目前状态，系统会提供相关命令。
## 删除文件
当文件没有用时，我们删除文件，同时可以删除git里面文件，如果仅仅删除工作空间文件还可以恢复
```
rm file.txt   //删除文件
git rm file.txt  git commit  //删除git仓库中的文件，并且提交，这时仓库中删除，不能再返回。
git checkout -- file.txt  //如果没有删除仓库中文件，只是删除工作区的文件可以利用此命令恢复。
```
## 远程仓库
* 首先在GitHub中创建仓库，然后需要关联本地仓库
```
git remote add origin git@github.com:michaelliao/learngit.git //后面的可以找到仓库进行复制相关地址
```
第一次进行关联会出现SSH警告，这时我们只需要输入YES然后点击回车即可.
* 本地库推送到远程库
```
git push -u origin master 
```
注：<br>
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。远程库的名字就是origin,默认叫法，可以修改。<br>
第一次推送需要加上-u目的是为了建立本地和远程的关联。在下次进行推送时，可以直接使用git push.<br>
在推送过程中如果推送失败，那是因为你的SSH Key公钥不在我的账户列表中，解决办法:<br>
打开git brash————输入命令：ssh -keygen -t rsa -c 邮箱，一路回车————在提示的目录文件中打开会看到id——rsa.pub和-ssh id_rsa,复制公有的文件锁，相当于一把钥匙，可以上传远程仓库—————打开GitHub，找到SSHKEY界面，new一个，粘贴进去提交就成功了。
* 从远程库克隆
```
git clone git@github.com:michaelliao/gitskills.git
```
后面地址有两种形式，一种是原生态的git协议，这个形式速度较快。另一种是HTTP协议，为了支持必须使用此形式的下载。
# git github gitlab的区别
Git是版本控制系统，Github是在线的基于Git的代码托管服务，Github有个小缺陷 (也不能算是缺陷吧), 就是你的repo(repository的缩写，表示“仓库”)都需要public(公开), 如果你想要创建private(私人)的repo, 那得付钱。
不过, 幸好, Gitlab解决了这个问题, 可以在上面创建免费的私人repo。
# gitlab使用
## gitlab的界面介绍
* Profile Settings：配置文件,可以配置个人信息<br>
* Account Settings：账户设置，可以修改用户名和私有令牌用于访问代码资源。可以设置用户名<br>
## gitlab中新建文件
* Project path：项目的路径，一般可以认为是项目的名称<br>
* Import prject from：从哪导入项目，提供Github/Bitbucket等几个选项<br>
* Description（项目的描述）：可选项，对项目的简单描述<br>
* Visibility Level（项目可见级别）：提供Private（私有的，只有你自己或者组内的成员能访问）/Internal（所有登录的用户）/Public(公开的，所有人都可以访问)三种选项。<br>
