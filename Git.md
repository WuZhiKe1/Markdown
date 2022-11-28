

# 分布式版本控制系统

<font style='color:#DA924A'>特点:</font>基于服务器、客户端的运行模式

●服务 器保存文件的所有更新版本
●客户端是服务器的完整备份，并不是只保留文件的最新版本

<font style='color:#DA924A'>优点:</font>

1. 联网运行，支持多人协作开发。
2. 客户端断网后支持离线本地提交版本更新。
3. 服务器故障或损坏后，可使用任何一一个客户端的备份进行恢复。

----

# 初识Git

[<font color='cornflowerblue'>安装Git</font>](https://git-scm.com/)

<font color='#D26B6B'>配置Git   </font>桌面鼠标右击  打开 Git  Bash  here 终端

输入

<font color='#DA924A'> git config --global user.name"用户名"</font>

<font color='#DA924A'> git config --global user.email"邮箱地址"</font>

通过git config --global user.name和git config --global user.email配置的用户名和邮箱地址，会被写

入到C:/Users/用户名文件夹/.gitconfig文件中。这个文件是Git 的全局配置文件,配置-次即可永久生效。



可以使用记事本打开此文件，从而查看自己曾经对Git做了哪些全局性的配置。

<font color='#DA924A'>可以使用git help config 命令，无需联网即可在浏览器中打开帮助手册</font>

<font color='#D26B6B'>更简明的帮住手册   git config -h</font>

 

Git之所以<font style = 'color: #DA924A'>快速和高效</font>，主要依赖于它的如下两个特性:

1. 直接记录快照，而非差异比较.
2. 近乎所有操作都是本地执行





Git快照是在原有文件版本的基础，上重新生成一份新的文件，<font color='#DA924A'> 类似于备份</font>。

为了效率，如果文件没有修改,Git
不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

<font color='#DA924A'>缺点</font>:占用磁盘空间较大。

<font color='#DA924A'>优点</font>:版本切换时非常快，因为每个版本都是完整的文件快照，切换版本时直接恢复目标版本的快照即可。

<font color='#DA924A'>特点</font>:空间换时间。



在Git中的绝大多数操作都<font color='#DA924A'>只需要访问本地文件和资源</font>，一般不

需要来自网络上其它计算机的信息。

<font color='#DA924A'>特性:</font>

1. 断网后依旧可以在本地对项目进行版本管理。
2. 联网后，把本地修改的记录同步到云端服务器即可。

----

# 获取Git仓库

1. 将尚未进行版本控制的本地目录转换为Git仓库。

2. 从其它服务器克隆一个已存在的Git仓库。

   

----

# 现有目录初始化Git仓库



1. 在项目目录中，通过鼠标右键打开"Git Bash Here"。
2. 执行 <font color='#DA924A'>git init</font> 命令将当前的目录转化为Git仓库。
   
   

<font color='#DA924A'>git init</font>命令会创建一一个名为 .<font color='#DA924A'>git 的隐藏目录</font>,这个  .git  目录就是当前项目的Git仓库，里面包含了初始的必要
文件，这些文件是Git仓库的必要组成部分 （打开文件的查看将 隐藏项目选择可查看）。



----

# 使用Git管理的项目

**<font color='#D26B6B'>拥有:</font>**

## <font color='#DA924A'>三个区域：</font>

1. 工作区：处理工作的区域。
2. 暂存区：已完成的工作的临时存放区，等待被提交。
3. Git 仓库：最终存放区域。



## 工作区域中的文件状态

四种状态分为<font color='#DA924A'>两大类</font>：

<font color='#DA924A'>未被Git管理：</font>

1. 未跟踪（Untracked）：不被Git管理的文件（新建的文件...）。

<font color='#DA924A'>已被Git管理：</font>

1. 未修改(Unmodified) ：  工作区中文件的内容和Git仓库中文件的内容保持一致。
2. 已修改(Modified )：工作区中文件的内容和Git仓库中文件的内容不一致。
3. 已暂存(Staged)：工作区中被修改的文件已被放到暂存区，准备将修改后的文件保存到Git 仓库中。



<font color='#DA924A'>注意:</font>

  ●工作区的文件被修改了 ,但还没有放到暂存区,就是已修改状态。
  ●如果文件已修改并放入暂存区，就属于已暂存状态。
  ●如果Git 仓库中保存着特定版本的文件，就属于已提交状态。

## 基本的Git工作流程:

1. 在工作区中修改文件。
2. 将你想要下次提交的更改进行暂存。
3. 提交更新，找到暂存区的文件，将快照永久性存储到Git仓库。



## 检查文件的状态

使用 git status 命令查看文件处于什么状态。

git status  -s 来精简的显示文件状态   <font color='#DA924A'>未跟踪的文件（Untracked files）</font> 前面有红色的 <font color='#D26B6B'>？？</font>标记。

<font color='#DA924A'>已暂存(Staged)</font>  绿色的文件名。

<font color='#D26B6B'>clear 清空当前的窗口  更好的观察命令</font>



## 跟踪新文件

git add  命令开始跟踪一个文件，git add index.html   加文件名。

此时再运行git status命令，会看到new file : index.html文件在<font color='#DA924A'>Changes to be committed</font>  这行的下面，说明已被
跟踪，并处于<font color='#DA924A'>已暂存(Staged)</font>  状态。



## 提交更新

现在暂存区中有一个index.html文件等待被提交到Git仓库中进行保存。可以执行 <font color='#DA924A'>git commit</font> 命令进行提交,
其中  <font color='#DA924A'>-m</font>  选项后面是本次的提交消息，用来对提交的内容做进一步的描述:
<font color='#DA924A'>git commit -m "新建了index .html文件”</font>

提交成功之后，再次检查文件的状态,得到提示如下:
<font color='#DA924A'>On branch master</font>
<font color='#DA924A'>nothing to commit, working tree clean</font>
证明工作区中所有的文件都处于“未修改”的状态，没有任何文件需要被提交。



## 对已提交的文件修改

index.html 文件已经被Git跟踪，并且工作区和Git仓库中的index.html文件内容保持一致。当



修改了工作区中index.html的内容之后，再次运行git status和git status -S命令,会看到如下的内容: 

$ git status
On branch master
<font color='#DA924A'>Changes not staged for commit:</font>
   (use "git add <file>..."to update what wi 11 be commi tted) 
   (usegit restore <file>..." to discard changes in working di rectory)
          <font color='#D26B6B'>  modified:index. html</font>
no changes added to commit (use "git add" and/or "git commit -a")

$ git status -S
<font color='#D26B6B'>M </font>index. html



文件  index.html  出现在  <font color='#DA924A'>Changes not staged for commit</font>  这行下面，说明已跟踪文件的内容发生了变化,但还没有放到暂存区。

<font color='#DA924A'>注意</font>:修改过的、没有放入暂存区的文件前面有<font color='#D26B6B'>红色的M</font>标记。



## 暂存已修改的文件

工作区中的index.html文件已被修改,如果要暂存这次修改，

<font color='#DA924A'>需要再次运行  gitadd  命令</font>,

这个命令是个多功能的命令，主要有如下3个功效:

1. 可以用它开始跟踪新文件。
2. 把已跟踪的、且已修改的文件放到暂存区。
3. 把有冲突的文件标记为已解决状态。



## 提交暂存的文件



再次运行 <font color='#DA924A'> git commit -m  ”初始化了index.html文件“</font>命令。



## 撤销对文件的修改

撤销对文件的修改指的是:把对工作区中对应文件的修改，还原成Git仓库中所保存的版本。

<font color='#DA924A'>操作的结果:</font><font color='#D26B6B'>所有的修改会丢失</font>，<font color='#D26B6B'>且无法恢复!危险性比较高，请慎重操作!</font>



使用<font color='#DA924A'>git checkout -- index.html</font>命令，撤销对index.html文件的修改



## 向暂存区一次性添加多个文件  <font color='#D26B6B'>git add .</font>



## 取消暂存的文件  git reset HEAD 要移除的文件名

<font color='#D26B6B'>git reset HEAD .</font>  移除所有暂存文件



## 跳过暂存区域

Git标准的工作流程是<font color='#DA924A'>工作区→暂存区→Git仓库</font>，但有时候这么做略显繁琐，此时可以跳过暂存区，直接将

工作区中的修改提交到Git仓库,这时候Git工作的流程简化为了<font color='#DA924A'>工作区→Git仓库</font>。

Git提供了一个跳过使用暂存区域的方式，只要在提交的时候，<font color='#DA924A'>给git commit加上-a选项</font>，Git 就会自动把

所有已经跟踪过的文件暂存起来一并提交, 从而跳过git add步骤:

<font color='#D26B6B'>git commit -a -m "描述信息"</font>



## 移除文件

<font color='#DA924A'>从Git仓库中移除文件的方式有两种:</font>

1. 从Git仓库和工作区中同时移除对应的文件。
2. 只从Git仓库中移除指定的文件,但保留工作区中对应的文件。

```py
1 #从Git仓库和工作区中同时移除index.html 文件
2 git rm -f index. html
3 #只从Git仓库中移除index.html, 但保留工作区中的index.html 文件
4 git rm --cached index. html 
```



## 忽略文件

一般我们总会有些文件无需纳入Git的管理，也不希望它们总出现在未跟踪文件列表。在这种情况下，我们可
<font color='#DA924A'>以创建一个名为 .gitignore 的配置文件，列出要忽略的文件的匹配模式。</font>
<font color='#D26B6B'>文件.gitignore的格式规范如下</font>:

1. 以  <font color='#DA924A'>#</font>  开头的是注释。
2. 以 <font color='#DA924A'> / </font> 结尾的是目录 （任何目录）。
3. 以 <font color='#DA924A'> / </font> 开头防止递归 （当前目录）。
4. 以  <font color='#DA924A'>!  </font>开头表示取反。
5. 可以使用  <font color='#DA924A'>glob </font> 模式进行文件和文件夹的匹配  (glob 指简化了的正则表达式)。



### glob模式

所谓的glob模式是指简化了的正则表达式:

1. 星号 <font color='#DA924A'>*</font> 匹配零个或多个任意字符。
2. <font color='#DA924A'>[abc]</font> 匹配任何-一个列在方括号中的字符( 此案例匹配一个a或匹配-一个b或匹配一一个c)。
3. 问号 <font color='#DA924A'>? </font>只匹配-一个任意字符。
4. 在方括号 中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配(比如 <font color='#DA924A'>[0-9]</font> 表示匹配所有0到9的数字)。
5. 两个星号 <font color='#DA924A'> */ *</font> 表示匹配任意中间目录(比如a/**/z可以匹配a/z、a/b/z 或a/b/c/z等)。

```python
#忽略index.html
index.html
#忽略所有的.a文件
*.a

#但跟踪所有的lib.a, 即便你在前面忽略了.a文件
!lib.a

#只忽略当前目录下的TODO文件，而不忽略subdir/T0D0
/TODO

#忽略任何目录下名为build的文件夹
build/

#忽略doc/notes. txt, 但不忽略doc/ server /arch. txt
doc/*. txt

#忽略doc/ 目录及其所有子目录下的.pdf文件
doc/**/* . pdf
```



## 查看提交历史

如果希望回顾项目的提交历史，可以使用<font color='#DA924A'>git log</font>这个简单且有效的命令。
```python
#按时间先后顺序列出所有的提交历史，最近的提交排在最上面
git log     #冒号后按回车继续显示提交信息  --------------------- 按  q  退出---------------------------

#只展示最新的两条提交历史， 数字可以按需进行填写
git log -2

#在一行上展示最近两条提交历史的信息
git log -2 --pretty=oneline

#在一行上展示最近两条提交历史的信息，并自定义输出的格式
# %h提交的简写哈希值  %an作者名字  %ar作者修订日期，按多久以前的方式显示  %s提交说明
git log -2 --pretty=format:"%h |%an | %ar| %s"
```



## 回退到指定的版本

```python
#在一行上展示所有的提交历史
git log --pretty=oneline 

#使用git reset --hard命令，根据指定的提交ID回退到指定版本
git reset --hard <CommitID>

#在旧版本中使用git reflog --pretty=oneline 命令，查看命令操作的历史
git reflog --pretty=oneline

 #再次根据最新的提交ID,跳转到最新的版本
 git reset --hard <CommitID>

```



----



# 本地分支操作

在进行多人协作开发的时候，为了防止互相干扰,提高协同开发的体验，建议每个开发者都基于分支进行项目

功能的开发。







## main主分支

在初始化本地Git仓库的时候，Git <font color='#DA924A'>默认</font>已经帮我们创建了-一个名字叫做master的分支。通常我们把这个

<font color='#DA924A'>main分支</font>叫做<font color='#DA924A'>主分支</font>。



在实际工作中，master主分支的作用是:<font color='#DA924A'>用来保存和记录整个项目已完成的功能代码</font>。

因此，<font color='#DA924A'>不允许</font>直接在master分支上修改代码，因为这样做的<font color='#D26B6B'>风险太高</font>，容易导致整个项目崩溃。







## 功能分支

由于不能直接在main分支上进行功能的开发，所以就有了<font color='#DA924A'>功能分支</font>的概念。

功能分支指的是专门用来开发新功能的分支，它是临时从main主分支.上分叉出来的，当新功能开发且测试

完毕后，最终需要合并到main主分支上。







## 查看分支

```
git branch 查看当前Git仓库的所有分支    
```

分支名字前的 * 号表示<font color='#D26B6B'>当前所处的分支</font>。







## 创建新分支

<font color='#D26B6B'>基于当前分支创建新分支。</font>

```
git branch 分支名称
```

<font color='#DA924A'>执行完创建分支当前所处的还是 main 主分支。</font>







## 切换分支

<font color='#DA924A'>切换到指定的分支上开发。</font>

```
git checkout 以存在分支名字
```







## 分支的快速创建和切换

<font color='#DA924A'>创建并切换到新分支上</font>

```
#-b表示创建一个新分支
# checkout 表示快速切换到 新创建的分支上
git checkout -b 创建的分支名称
```







## 合并分支

功能分支的代码开发测试完毕之后，可以使用如下的命令,将完成后的代码合并到main主分支上:

```
# 1.切换到main 分支
git checkout main

# 2.在main分支上运行git merge 命令，将login分支的代码合并到main分支
git merge login 
```

<font color='#DA924A'>合并分支时的注意点:</font>
假设要把C分支的代码合并到A分支,则必须先切换到A分支上，再运行gitmerge命令，来合并C分支!







## 删除分支

当把功能分支的代码合并到main主分支上以后，

想删除已经合并的分支（删除的是分支 ，不是合并在主分支上的功能）

<font color='#DA924A'>需要切换到其他的分支上</font>

就可以使用如下的命令,删除对应的功能分支:

```
git branch -d 分支名称
```

<font color='#DA924A'>如果当前分支没有合并会报错</font>

<font color='#D26B6B'>可以强制删除 git  branch -D 分支名</font>









## 遇到冲突时的分支合并

如果在两个不同的分支中，对同一个文件进行了不同的修改，

Git 就没法干净的合并它们。

此时，我们需要打开这些包含冲突的文件然后<font color='#DA924A'>手动解决冲突</font>。



```python
#假设:在把reg分支合并到main分支期间，代码发生了冲突
git checkout main
git merge reg

#打开包含 冲突的文件，手动解决冲突之后， 再执行如下的命令
gitadd.
gitcommit-m"解决了分支合并冲突的问题”
```

<font color='#D26B6B'>手动解决</font>

打开出现冲突的文件   冲突代码上有四个按钮 <font color='#DA924A'> 采用当前修改   |   采用传入的修改   |   保留双方的修改   |   比较变更</font>

绿色代码块是当前修改                   蓝色是传入修改





## 将本地分支推送到远程仓库

如果是第一次将本地分支推送到远程仓库,需要运行如下的命令:

```python
#-U表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带-U参数
 git push -u 远程仓库的别名默认origin  本地分支名称  远程分支名称

#实际案例:
 git push -u origin payment:pay
#如果希望远程分支的名称和本地分支名称保持-致，可以对命令进行简化:
 git push -U origin payment 
```

GitHub中在 当前Git项目中  查看 main 下拉菜单 可查看分支

<font color='#D26B6B'>注意</font>:第一次推送分支需要带-u参数,此后可以直接使用git push推送代码到远程分支  （当前仓库几经包含了推送的分支的时候 直接使用 git push origin payment:pay）。







## 查看远程仓库的所有分支列表

```
git remote show 远程仓库名
```









## 跟踪分支

跟踪分支指的是:从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下:
```python
 #从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
 git checkout 远程分支的名称
 #示例:
 git checkout pay

 #从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
 git checkout -b 本地分支名称  远程仓库名称/远程分支名称
#示例:
 git checkout -b payment origin/pay
```









## 拉取远程分支的最新的代码

可以使用如下的命令,把远程分支最新的代码下载到本地对应的分支中:
```python
#从远程仓库，拉取当前分支最新的代码，保持当前分支的代码和远程分支代码一致
git pull
```









## 删除远程分支

可以使用如下的命令，删除远程仓库中指定的分支:
```python
#删除远程仓库中，指定名称的远程分支
git push远程仓库名称--delete 远程分支名称

#示例:
git push origin --delete pay
```































# 开源许可协议

开源并不意味着完全没有限制，为了限制使用者的使用范围和保护作者的权利，每个开源项目都应该遵守<font color='#DA924A'>开源</font>
<font color='#DA924A'>许可协议( Open Source License )。</font>

<font color='#DA924A'>常见的5种开源许可协议</font>

1. BSD ( Berkeley Software Distribution)
2. Apache Licence 2.0
3. <font color='#D26B6B'>GPL </font>( GNU General Public License )

​           ●具有传染性的一 种开源协议， 不允许修改后和衍生的代码做为闭源的商业软件发布和销售
​           ●使用GPL的最著名的软件项目是: Linux

4. LGPL ( GNU Lesser General Public License )

5. <font color='#D26B6B'>MIT</font> ( Massachusetts Institute of Technology, MIT )

​            ●是目 前限制最少的协议,唯-的条件: 在修改后的代码或者发行包中，必须包含原作者的许可信息
​            ●使用 MIT的软件项目有: jquery、 Node.js



# GItHub新建远程仓库

1. 点击右上角加号  点击 New reposi'tory
2. 输入  新建仓库名字 （最好不使用中文）
3. Description  （描述）
4. 勾选 public（公共） private（私有）



# 远程仓库的两种访问方式

Github.上的远程仓库，有两种访问方式，分别是HTTPS和SSH。它们的区别是:

1. <font color='#DA924A'>HTTPS:</font> 零配置;但是每次访问仓库时，需要重复输入Github的账号和密码才能访问成功
2. <font color='#DA924A'>SSH</font>:需要进行额外的配置;但是配置成功后，每次访问仓库时，不需重复输入Github的账号和密码

 创建完仓库后推荐选择  SSH 访问方式。



# 提交本地代码流程

## <font color='#DA924A'>HTTPS访问方式</font>

1. <font color='#D26B6B'>本地如果没有现有的  Git  仓库 应将文件提交到  Git  仓库。</font>
2. <font color='#D26B6B'>如果本地存在  Git  仓库  可以将本地仓库  Git  与远程仓库关联  ， 并把远程仓库命名 origin。</font> 
3. <font color='#D26B6B'>将本地仓库  Git  的内容推送到 远程仓库 origin。</font>

<font color='#DA924A'>将官方推出的代码 在 Git 终端输入 等待传输。</font>

```
git remote add origin https://github.com/WuZhiKe1/demo.git
git branch -M main
git push -u origin main
```



<font color='#DA924A'>再次提交修改后的文件  输入：</font>

<font color='#D26B6B'>git push</font>



## SSH key方式访问



SSH key的<font color='#DA924A'>作用</font>:实现本地仓库和Github之间免登录的加密数据传输。
SSH key的<font color='#DA924A'>好处</font>:免登录身份认证、数据加密传输。
SSH key由两部分<font color='#DA924A'>组成</font>：

1. id_ rsa (私钥文件,存放于客户端的电脑中即可)
2. id_ _rsa.pub (公钥文件，需要配置到Github中)

### <font color='#DA924A'>生成SSH key</font>

1. 打开Git Bash   终端
2. 粘贴如下的命令,并将email@outlook.com替换为注册Github账号时填写的邮箱: 
   <font color='#D26B6B'>ssh-keygen -t rsa -b 4096 -C "email@outlook.com"</font>。
3. 连续敲击3次回车，即可在C:\Users\用户名文件夹\.ssh目录中生成id_ rsa 和id_ rsa.pub 两个文件。



### <font color='#DA924A'>配置SSH key</font>

1. 使用记事本打开 <font color='#DA924A'> id_ _rsa.pub </文件,复制里面的文本内容。
2. 在浏览器中登录Github,<font color='#DA924A'>点击头像-> Settings -> SSH and GPG Keys -> New SSH key</font>。
3. 将<font color='#DA924A'>id_ rsa.pub</font>文件中的内容,<font color='#DA924A'>粘贴到Key对应的文本框中</font>。
4. 在Title文本框中任意填写-一个名称，来标识这个Key从何而来。





### <font color='#DA924A'>检测Github的SSHkey是否配置成功</font>

1. 打开Git Bash,输入如下的命令并回车执行:
   ssh -T git@github.com

2. .上述的命令执行成功后，可能会看到如下的提示消息:

```
The authenticity of host ' github.com (IP ADDRESS)' can't be established .
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1 IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)?
```

输入yes之后，如果能看到类似于下面的提示消息  看到用户名，证明SSH key已经配置成功了:

```
Hi username! You've successfully authenticated, but GitHub does not
provide shell access .
```





1. 创建仓库
2. 更该访问方式为 SSH
3. 依次在  git 终端运行

```
git remote add origin git@github.com:WuZhiKe1/project-demo2.git
git branch -M main
git push -u origin main
```

后续修改 运行

<font color='#D26B6B'>git push</font>





# 将远程仓库克隆到本地

```
git clone 远程仓库地址
```

<font color='#DA924A'>点击Code  选择访问方式 HTTPS SSH   然后复制地址</font>



# 更改远征仓库地址

 ```js
 git remote set-url origin git@github.com:WuZhiKe1/Admain.git
 ```







