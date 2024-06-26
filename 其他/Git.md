## Git基本概念
### 1. Git历史
Git 是最流行的分布式版本控制系统(Distributed Version Control System, 简称 DVCS)。它由Linus Torvalds创建,当时非常需要一个快速、高效和大规模分布式的源代码管理系统, 用于管理 Linux 源代码。
由于 Linus 对几乎所有现有的源代码管理系统抱有强烈的反感, 因此他决定编写自己的源代码管理系列。2005年4月, Git就诞生了。到了2005年7月, 维护工作就交给了Junio Hamano, 自此他就一直在维护这个项目。
虽然最初只用于 Linux 内核, 但 Git 项目迅速传播, 并很快被用于管理许多其他 Linux 项目。现在, 几乎所有的软件开发, 尤其是在开源世界中, 都是通过 Git 进行的。
### 2. 版本控制系统
版本控制是指对软件开发过程中各种程序代码、配置文件及说明文档等文件变更的管理, 是软件配置管理的核心思想之一。版本控制技术是团队协作开发的桥梁, 助力于多人协作同步进行大型项目开发。软件版本控制系统的核心任务就是查阅项目历史操作记录、实现协同开发。
常见的版本控制主要有两种: **集中式版本控制**和**分布式版本控制**
(1) 集中式版本控制
集中式版本控制系统: 版本库是集中存放在中央服务器的。工作时, 每个人都要先从中央服务器获取最新的版本。完成之后, 再把自己添加/修改的内容提交到中央服务器。所有文件和历史数据都存储在中央服务器上。SVN 是最流行的集中式版本控制系统之一。
集中式版本控制系统的缺点就是必须联网才能使用, 如果使用局域网还好, 速度会比较快。而如果是使用互联网, 网速慢的话, 就可能需要等待很长时间。除此之外, 如果中央服务器出现故障, 那么版本控制将不可用。如果中心数据库损坏, 若数据未备份, 数据就会丢失。
![[../Image/Pasted image 20240229221238.png]]

(2) 分布式版本控制
分布式版本控制系统: 每台终端都可以保存版本库, 版本库可以不同, 可以对每个版本库进行修改, 修改完成后可以集中进行更新。虽然它没有中心服务器, 但可以有一个备份服务器, 它的功能有点类似于 SVN 的中央服务器, 但它的作用仅是方便交换修改, 而不像 SVN 那样还要负责源代码的管理。Git 是最流行的分布式版本控制系统之一。
和集中式版本控制系统相比, 分布式版本控制系统的安全性要高很多, 因为每个人电脑里都有完整的版本库, 某一个人的电脑损坏不会影响到协作的其他人。
![[../Image/Pasted image 20240229221550.png]]
(3) SVN VS Git
Git相较于SVN:
- **提交速度更快**

	因为在SVN中需要更频繁地提交到中央存储库, 所以网络流量会减慢每个人的速度。而使用Git, 主要在本地存储库上工作, 只需每隔一段时间才提交到中央存储库。
- **没有单点故障**

	使用 SVN, 如果中央存储库出现故障, 则在修复存储库之前, 其他开发人员无法提交他们的代码。使用 Git, 每个开发人员都有自己的存储库, 因此中央存储库是否损坏并不重要。开发人员可以继续在本地提交代码, 直到中央存储库被修复, 然后就可以推送他们的更改;
- **可以离线操作**

	与SVN不同, Git可以离线工作, 即使网络失去连接, 也可以继续工作而不会丢失功能
![[../image/Pasted image 20240229222548.png]]
	
### 3. Git安装
在Git官网下载、安装即可: https://git-scm.com/download
![[../Image/Pasted image 20240229223459.png]]
安装完成后, 可以使用以下命令查看Git是否安装成功:
```bash
git --version
```
如果安装成功, 终端会打印安装的Git的版本
```bash
[root@localhost ~]# git --version
git version 1.8.3.1
```
### 4. Git初始化
要给项目初始化一个Git仓库, 可以在终端中打开项目目录, 执行以下命令即可
```bash
git init
```
初始化之后, 就会创建一个名为.git的新子文件夹, 其中包含Git将用于跟踪项目更改的多个文件和更多的子目录
```bash
[root@localhost LearnPython]# cd ./.git/
[root@localhost .git]# ls
branches  config  description  HEAD  hooks  info  objects  refs
```
在使用Git进行代码管理时, 不希望一些文件出现在跟踪的列表中, 比如node_modules文件。在这种情况下, 可以在项目的根目录中创建一个名为.gitignore的文件, 在该文件中列出要忽略的文件和文件夹, 例如:
```
# 所有以.md结尾的文件  
*.md  
  
# lib.a不能被忽略  
!lib.a  
  
# node_modules和.vscode文件被忽略  
node_modules  
.vscode  
  
# build目录下的文件被忽略  
build/  
  
# doc目录下的.txt文件被忽略  
doc/*.txt  
  
# doc目录下多层目录的所有以.pdf结尾的文件被忽略  
doc/**/*.pdf
```
> 注意：以 # 符号开头的行是注释。

可以在本地克隆Git存储库上的代码, 首先要找到Git存储库上的HTTPS或SSH的地址, 如下:
![[../Image/Pasted image 20240229224935.png]]
然后使用以下命令将远程仓库克隆到本地
```bash
git clone https://github.com/facebook/react.git
```

### Git结构和状态
从Git的角度来看, 可以在三个区域进行文件更改: 工作区, 暂存区和存储库
- **工作区**: 本地看得到的工作目录
- **暂存区** : 一般存放在`.git`录下的index文件(.git/index)中, 所以暂存区有时也叫索引(index), 暂存区是一个临时保存修改文件的地方
- **版本库**: 工作区有一隐藏的目录`.git`, 这个不算工作区, 而是Git的版本库, 版本库中存储了很多配置信息、日志信息和文件版本信息等
![[../Image/Pasted image 20240229232305.png]]
Git工作目录下的文件存在两种状态:
- Untracked: 未跟踪, 未被纳入版本控制, 即该文件没有被Git版本管理
- tracked: 已跟踪, 被纳入版本控制, 即该文件已被Git版本管理
其中**已跟踪状态**可以细分为以下三种状态:
- Unnodified: 未修改状态
- Modified: 修改状态
- Staged: 已暂存状态

可以通过运行以下命令来检测当前分支的状态
```bash
git status
```
此命令不会更改或更新任何内容。它会打印出哪些文件被修改、暂存或未跟踪。未跟踪的文件是尚未添加到 git 索引的文件, 而自上次提交以来已更改的文件将被视为已被git修改
## Git入门
### 1. 全局配置
当安装Git后首先要做的就是配置所有本地存储库中使用的用户信息。每次Git提交都会使用该用户信息。
config命令适用于不同的级别:
- **本地级别**: 所有配置都仅限于项目目录。默认情况下, 如果未通过任何配置, 则git config将在本地级别写入
- **全局级别**: 此配置特定于操作系统上的用户, 配置值位于用户的主目录中。
- **系统级别**: 这些配置放在系统的根路径下, 它跟踪操作系统上的所有用户和所有存储库
下面的配置均为写入系统级别:

1. **设置用户名**

可以使用以下命令设置使用Git时的用户名:
```bash
git config --global user.name "name"
```
可以使用以下命令查看设置的 `user.name`
```bash
git config user.name
```

2. **设置邮箱**

可以使用以下命令设置使用Git时的邮箱
```bash
git config --global user.email "email"
```
可以使用以下命令查看设置的`user.email`
```bash
git config user.email
```

3. **设置命令颜色**

除了上述两个基本的设置之外, 还可以设置命令的颜色, 以使输出具有更高的可读性:
```bash
git config --global color.ui auto
```

4. **查看所有配置**

通过上述的命令设置的信息会保存在本地的`.gitconfig`文件中, 可以使用以下命令查看所有配置信息
```bash
git config --list
```
如果在全局输入这个命令，就会显示全局的配置
如果在使用 Git 的项目中输入该命令, 除了会显示全局的配置之外, 还会显式本地仓库的一些配置信息

5. **设置别名**

git config命令为我们提供了一种创建别名的方法, 这种别名通常用于缩短现有的命令或者创建自定义命令。
```bash
git config --global alias.cm "commit -m"
```
为`commit -m`创建一个别名`cm`, 这样在提交暂存区文件时, 只需要输入以下命令即可:
```bash
git cm <message>
```

### 2. 分支操作
分支是源代码控制的核心概念, 它允许将工作分离到不同的分支中, 这样就可以自由地处理源代码, 而不会影响其他任何人的工作或主分支中的代码。
1.  查看分支

可以使用以下命令来查看当前所在分支以及该项目所有的分支情况
```bash
git branch
```
该命令可以列出项目所有的**本地分支**, 显示绿色的分支就是当前分支
可以使用以下命令来列出所有的远程分支
```bash
git branch -r
```
可以使用以下命令来查看所有的本地分支和远程分支
```bash
git branch -a
```

2. 创建分支

在计算机上只能访问本地分支, 在将分支推送到远程仓库之前, 需要先创建一个本地分支
可以使用以下命令来创建分支
```bash
git checkout <branch>
```
加上`-b`就可以在创建新分支之后, 直接切换到新创建的分支上
```bash
git checkout -b <branch>
```
如果想将新建的本地分支推送到远程仓库, 以在远程仓库添加这个分支。可以执行以下命令
```bash
git push -u origin <branch>
```

3. 删除分支

可以使用以下命令来删除本地分支
```bash
git branch -d <branch>
```
> 需要注意，在删除分支之前，要先切换到其他分支, 否则就会报错

有时Git会拒绝删除本地分支