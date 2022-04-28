# Git简介

版本控制工具应该具备的功能：

* 协同修改，多人并行不悖地修改服务器端地同意给文件
* 数据备份，保存每一个提交过的历史状态
* 版本管理，Git采用文件系统快照
* 权限控制
* 历史记录
* 分支管理



<img src="Git.assets/image-20220427164234212.png" alt="image-20220427164234212" style="zoom:50%;" />



## Git 和 代码托管中心

* 局域网环境下
  * GitLab 服务器
* 外网环境下
  * GitHub
  * 码云



本地库开发：

<img src="Git.assets/image-20220427164828870.png" alt="image-20220427164828870" style="zoom:50%;" />

远程库开发：

<img src="Git.assets/image-20220427165049497.png" alt="image-20220427165049497" style="zoom:50%;" />



# 基本操作

打开vim编辑器：`vim good.txt` 关闭时 esc 后输入 :wq

查询文件内容：`cat good.txt`

删除文件：`rm good.txt`



## Git命令行操作

### 初始化

`git init`

会生成一个隐藏文件夹，存放的是本地库相关的子目录和文件，使用 `ls -lA` 命令可以看到

![image-20220427170034494](Git.assets/image-20220427170034494.png)



### 设置签名

* 形式：
  * 用户名：Candy
  * Email 地址：zyy9803@foxmail.com
* 作用：取分不同开发人员的身份
* 辨析：这里设置的签名和登陆代码托管中心的账号、密码没有任何关系
* 命令：
  * 项目级别/仓库级别：仅在当前本地库范围内有效
    * `git config user.name candy`
    * `git config user.email zyy9803@foxmail.com`
    * 信息保存位置 `.git/config` 文件中，可以通过 `cat .git/cofig` 命令查询
  * 系统用户级别：登陆当前操作系统的用户范围
    * `git config --global user.name candy`
    * `git config --global user.email zyy9803@foxmail.com`
    * 信息保存位置 `~/.gitconfig` 文件中，可以通过 `cd ~` 进入~目录 `cat .git/cofig` 命令查询
  * 级别优先级：
    * 就近原则：项目级别 > 系统用户级别
    * 如果只有系统用户级别，就以系统用户级别为准
    * 不允许二者都没有



### 添加提交及查看状态

* 查看状态：`git status`

查看工作区、暂存区的状态

![image-20220427190804893](Git.assets/image-20220427190804893.png)

* 添加文件：`git add good.txt`

将工作区的新建和修改添加到暂存区

![image-20220427190844239](Git.assets/image-20220427190844239.png)

* 提交文件：`git commit good.txt`

将暂存区的内容提交到本地库

![image-20220427191325049](Git.assets/image-20220427191325049.png)

如果修改了文件，git可以追踪到，此时需要通过 `git add good.txt` 再次添加并 commit

commit时可以通过 `git commit -m "Message" good.txt` 添加修改消息，不用进入 vim 编辑器



### 查看历史记录

* 查看提交 `git log` 最完整

多屏显示控制方式：空格向下翻页  b向上翻页  q退出

![image-20220427192734911](Git.assets/image-20220427192734911.png)

* 在同一行显示：
  * `git log --pretty=oneline` 简洁一些
  * `git log --oneline` 更简洁
  * `git reflog` 在上一个基础上显示了 `HEAD@{移动到当前版本需要多少步}`



### 版本前进后退

git 通过 head 指针控制版本前进后退

* 通过索引值 `git reset --hard 局部索引值`，索引值通过 git log 查看

![image-20220427194558100](Git.assets/image-20220427194558100.png)

* 使用 ^ 符号：`git reset --hard HEAD^^^`只能后退，几个 ^ 后退几步
* 使用 ~ 符号：`git reset --hard HEAD~5`只能后退，后退 n 步

参数含义：

* --soft 参数：仅仅在本地库移动 head 指针
* --mixed 参数：在本地库移动 head 指针，重置暂存区
* --hard 参数：在本地库移动 head 指针，重置暂存区，重置工作区



### 比较文件差异

* `git diff 文件名`
  * 将工作区中的文件和暂存区进行比较
* `git diff 本地库中的历史版本 文件名 `
  * 将工作区中的文件和本地库历史记录进行比较
* 不带文件名则比较多个文件



## 分支

![image-20220427214719390](Git.assets/image-20220427214719390.png)

分支的好处：

* 同时并行推进多个功能的开发，提高开发效率
* 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可



### 基本命令

* 列出分支基本命令：

```
git branch
```

* 创建分支命令：

```
git branch (branchname)
```

* 切换分支命令:

```
git checkout (branchname)
```

当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

* 合并分支命令:

先切换到接受修改的分支，在此分支上进行合并

```
git merge 
```



### 冲突解决

当我们在不同分支中修改同一个文件，合并时会产生冲突

* 冲突的表现：

![image-20220428102233635](Git.assets/image-20220428102233635.png)

* 冲突的解决
  * 编辑文件，删除特殊符号，按下 ESC 后 dd 删除整行，进行修改
  * `git add [文件名]`
  * `git commit -m 日志` 



# Git 原理

Git 通过 SHA-1 哈希算法对文件进行运算，获得哈希值，进行文件验证

Git把数据看作是小型文件系统的一组快照。每次提交更新时Git都会对当前的全部文件制作一个快照并保存这个快照的索引。为了高效，如果文件没有修改，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件。所以Gt的工作方式可以称之为快照流。

<img src="Git.assets/image-20220428103631235.png" alt="image-20220428103631235" style="zoom:50%;" />

每一个文件都有一个哈希值，每一个文件树有一个哈希值，每一次提交有一个哈希值

![image-20220428104330854](Git.assets/image-20220428104330854.png)



Git 在进行分支管理创建新分支时，并没有将所有文件复制一份，而是创建一个指针指向某一个版本

* 比如新建一个testing分支，它和master共同指向同一个版本

<img src="Git.assets/image-20220428105357146.png" alt="image-20220428105357146" style="zoom: 33%;" />

* 当我们切换到 testing 分支上时，只是 HEAD 指针的指向发生了变化

<img src="Git.assets/image-20220428105520602.png" alt="image-20220428105520602" style="zoom:33%;" />

* 当对 testing 修改并提交后，生成新的版本

<img src="Git.assets/image-20220428105607640.png" alt="image-20220428105607640" style="zoom:33%;" />

* 此时再切换回 master，就是 HEAD 指针指向发生改变，HEAD 再次提交后就会产生新版本

<img src="Git.assets/image-20220428105700635.png" alt="image-20220428105700635" style="zoom:33%;" />



# Github 

首先在 github 中创建远程仓库

* `git remote -v` 查看远程地址别名
* `git remote add [远程地址别名] [远程地址]`

推送操作：

* `git push [远程地址别名] [分支名字]`

克隆操作：

* `git clone [远程库地址]`
* 自动做了下面三件事
  * 完整的把远程库下载到本地
  * 创建 origin 远程地址别名
  * 初始化本地库

拉取操作：

* `git fetch [远程库地址别名] [远程分支名]`
* `git merge [远程库地址别名/远程分支名]`

* `git pull [远程库地址别名] [远程分支名]` 相当于 fetch + merge，同时进行了下载资源和合并

解决冲突：

* 如果不是基于 Github 远程库最新版所做的修改，不能推送，必须先拉取
* 拉去下来后如果进入冲突状态，则按照分支冲突操作解决即可

 
