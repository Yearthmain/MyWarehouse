# 浅谈git


要学习一门学科，语言或者一种工具，首先要知道我们所学为何，那么问题来了，挖掘......呸！GIT是什么？

用浅显的话来说嘛，GIT是目前世界上最先进的分布式版本控制系统。这样问题又来了，什么是版本控制系统？

中国山......呸！说到版本控制系统，我们先要知道什么是版本控制，这里我百科了一下，得到如下解释：
**版本控制(Revision control)是一种软体工程技巧，籍以在开发的过程中，确保由不同人所编辑的同一档案都得到更新。**
这是什么意思呢？举一个简单的例子就知道了，小A和小B在共同写一项工程，版本控制的作用就是当小A对这项工程进行修改的时候，小B那里也会得到同样的修改，反之亦然。理解了这个，什么是版本控制系统也就不必多费口舌了。

之前说到GIT是目前世界上一流的分布式版本控制系统，那么除了分布式，还有什么式呢，各有什么优劣呢？

我所知的，版本控制系统分为分布式和集中式。

>* 集中式：
集中式版本控制系统的版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在
互联网上，遇到网速慢的话，你就等着扣奖金吧。而且版本库放在中央服务器中，一旦发生什么不可抗力的事损坏了这个服务器，资料就毁掉了。

> * 分布式：
与集中式相比，分布式版本控制系统的安全性要高得多，首先，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，因为每个人电脑里都有完整的版
本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。也因为此，你工作的时候，甚至不需要联网，因为版本库就在你自己的电脑上。

说了这么多了，差不过该进入正题了，那就是GIT的学习，要学习这个软件，自然要安装它，Linux和Unix暂且不提，要在Windows上安装GIT也是很方便简单的事，在http://msysgit.github.io/下载，安装即可，不过在安装完成后需要进行最后一步设置
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
这样一来，Windows中的GIT就算是成功安装了

那么我们开始学习GIT之旅

第一步，创建一个版本库

那么问题来了（蓝翔蓝翔蓝翔蓝翔~~~~~~~），版本库是什么？

好问题，蓝……呸！版本库是什么呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

创建一个版本库是很简单的事，创建一个空目录，然后通过GIT BUSH进入（命令是cmd的命令），接下来我们将学到GIT的第一个常用命令
```
git init//创建版本库
```
创建了版本库，我们就该学习把自己的资料添加到库中，于是接下来我们学习两个命令

```
git add + FileName//添加文件到暂存区

git commit -m “备注”//提交文件到仓库
```
（tip：**git commit**命令这个-m没有也是可以的，但不建议这样，因为版本控制系统就是想让你记住自己的修改而定的，如果不备注那么很容易忘记）

这里要提一下，所谓文件管理系统，其实只能追踪文件的修改，比如TXT的文件，任何二进制文件的改变，是无法追踪的，比如一个图片，向其内部添加一些东西，使其变大，系统虽然能追踪出图片变大了，却不能看到是什么地方发什么了改变。很不幸的是，Windows中的word也是二进制格式，而且微软犯了个很傻比的错误，导致他们的TXT也会出现各种莫名其妙的错误，所以建议使用notepad++，只要用UTF-8无BOM格式编码就行了

当我们把文件添加进入仓库之后，继续修改文件，这时候另一个命令来了
```
git status//查看工作区和暂存区当前状态
```
当使用git status命令查看到文件被修改，但还没有提交的时候，就可以使用另一个命令来查看文件的修改
```
git diff + FileName//查看文件修改
```
将修改的文件提交到库中的之后你恍然发现自己提交的文件有错，需要修正，但是已经提交了怎么办呢？两个全新的命令来到眼前
```
git log//查看历史版本

git reset --hard HEAD^//版本回退（回退几个版本，就几个^）
```
于是你使用版本回退命令回到上一个版本，紧接着你发现，你没有犯错，是你搞错了（没错，我特么就是在逗你）

怎么办呢，别担心，版本不但能回退，还能前进

这个时候两个有两个方法，一是向上拉，看看之前那个版本的版本ID，什么是版本ID，问的哈，就是那一串长长的奇葩数字，找到以后，取前7位（一般来说超过5位就行了）
```
git reset --hard id
```
这样就万事大吉了，如果你不小心把窗口查了，不能想上去查找版本ID怎么办？也没关系，我会教给你一个新的命令，将拯救你与水火之中
```
git reflog//查看命令历史
```
使用这个命令之后一样能找到之前的版本号，然后方法一样就能让版本移动了

细心的朋友还会发现，GIT版本不论是前进还是回退都快的一逼，这是为什么呢？

我们便深入了解一下GIT版本原理，之前的命令有使用到HEAD，学过数据结构的大概会猜到，没错，就是链表，版本的回退与前进仅仅是改变一下链表next域的指向，所以才会那么快。
既然扯到这里，那我们便提一提之前遇到的两个区

 > * 工作区：
就是之前创建GIT仓库的那个文件目录，这个目录在电脑上是可视的，可以假想版本库是一座仓库，而工作区就是仓库以外，围墙以内的区域。

> * 暂存区：
之前提到版本库，版本库中最重要的东西之一就是缓存区，当我们使用add命令添加文件的时候，其实就是把文件添加到这里来，接着使用commit之后才会吧文件放入仓库。

为什么要设计这么一个缓存区呢，意义何在？
我们举个例子就知道了
修改了A文件
**git add**之后
再一次修改A文件
这个时候你**git checkout --A**,
A文件回到暂存时保存的状态,也就是第2步的状态
如果需要回到未修改的状态,需要运行**git reset HEAD**
可以用它防止**git checkout**误操作，而且,**git diff**优先把修改的和暂存比较,没有暂存时才拿上次提交的文件比较。

上面的例子提到了一个新的命令，这个命令是什么作用呢？

```
git checkout -- FileName//丢弃工作区的修改
```
人总有犯错的时候，如果你上传了多个文件到仓库中，却不小心包含了会造成XX门的文件，你继续工作之后忽然想起自己不小心上传了那个文件，如果不版本回退，就等着被炒鱿鱼，如果版本回退，那这期间就工作就白做了，这个时候，一个新的命令出现在眼前
```
git rm -- FileName//删除文件
```
有了这个命令，妈妈再也不担心我传错文件了。
之前我们所学的git上传文件都是上传到本地的仓库中，那么如何实现联机，远程共享呢？
答案就是：远程仓库。
关于远程仓库，Github网站做的很好，只要你去注册一个账号，就有了免费的远程仓库。
麻……既然看到了这里，我就假设你已经注册了账号，接下来需要做一些简单的设置：
>1：创建SSH Key。
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
>2：验证SSH Key.

登陆GitHub，打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。

如果完成了这一切，那么恭喜你，你现在已经成功了一半了，接下来我们将要创建一个远程仓库，并把本地仓库的资料推送到远程仓库中。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库，接着在Repository name填入仓库名称，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库。
最后的最后，就是推送本地仓库内容到远程的操作了，这几步错了就麻烦了，请认真完成：
```
$ git remote add origin git@github.com:email/Repositoryname.git
```
这个命令是关联本地与远程仓库，成功关联之后，就是用推送命令完成推送
```
$ git push -u origin master
```
由于是第一次推送，所有有个-u的参数，以后就可以不用加了
既然能够推送本地到远程，那么反之，克隆远程到本地自然也是可以的
```
$ git clone git@github.com:email/Repositoryname.git
```
有了这些功能，也许你已经感受到GIT的强大了，然而，它的强大远远不止于此，你之所见，只是冰山一角。现在我们学习GIT的分支管理系统。
什么是分支管理系统呢，我们举一个例子就明白了：
分支管理系统就如同超弦理论里讲到的平行空间，世界之间发生着不同的事，然而，如果不同世界之间互不影响，那倒没什么，如果在某一时刻，世界重合了呢？就说明你完全可以做不同的事情，在未完成的时候互不影响，在完成之后融合两个“世界”！
那么，如何创造新的“世界”呢，命令如下
```
$ git branch NewBranch//创建新分支
$ git checkout NewBranch//切换分支1
Switched to a new branch 'NewBranch'//切换分支2
```
我们可以使用**git branch**命令查看分支，在当前分支前面会有星号
```
$ git branch
* dev
  master
```
之前提到的合并世界让人热血沸腾，接下来将要学习的就是这个命令
```
$ git merge NewBranch//合并分支
```
分支已经合并，再留着这个新的分支已经没有什么意义，干脆将其删除
```
$ git branch -d NewBranch//删除分支
```