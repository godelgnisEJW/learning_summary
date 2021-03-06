# Git 

## Git基本概念

+ 版本控制系统把程序员所完成并提交（commit）的任何修改都记录下来
+ 直接访问式版本控制系统需要登录版本库所在服务器，才能访问版本库
+ 集中式版本库可以通过网络访问版本库，但是所有的操作必须连接网络，包括查询查询历史修改记录等
+ 分布式版本控制系统不会遇到网络带来的问题，每个人都有自己的本地库，历史修改都存储在本地的版本库中，提交代码也不需要联网，要将修改同步到主版本库，只需要通过Git的“Push”操作推送到主版本库即可。
+ Git记录和跟踪版本库中组成文件的各部分内容，而其他众多版本库控制工具则是以文件为单位存储，Git为文件中的字符和代码行添加一系列元数据，比如文件名，文件属性等，这样就能够降低版本库存储历史版本所需的磁盘空间，另外也使得函数或类在文件中的移动和拷贝更加便捷。
+ 版本库是版本控制系统用来存储所有历史数据的地方
+ 工作目录树是版本库的一个“断面视图”，它包括了开发该项目所需要的全部文件，包括源代码文件、构建文件、单元测试文件等。
+ 版本库会记录所有的commit，本地推送到公共版本库，使用push命令，本地从公共版本库取改动，使用fetch命令，合并操作使用merge命令，fetch和merge可以合并成一个操作，即pull命令。
+ 里程碑标志着项目的进程，使用标签能够记录下版本库在特定历史时刻的“断面视图”。标签以一个简单的名称（标签名）来标记版本库历史中某个特定的点，比如对外正式发布的版本，比如修复一个缺陷后打个标签
+ 分支可以用来做实验性的工作，如果有价值可以合并到主分支（Master Branch），也称为主干（trunk），没有价值的话，可以悄无声息地删除它，分支在本地和远程版本库都可以创建。
+ 合并操作地思路与程序员手工处理地思路是一致的，如果不同的变化发生在不同文件，那么可以自动合并，如果修改了同一处地方，那么会发生冲突，这时候需要手动处理冲突进行合并。
+ 合并跟踪（merge tracking）记录跟踪哪些提交已经合并在一起了

## Git设置

### 查看Git版本

```shell
git version
```

### 基本设置

```shell
#设置全局变量，使用 --global
#设置用户名
git config --global user.name "godlegnis"
#设置用户邮箱
git config --global user.email "2275433755@qq.com"
#使用不同颜色显示Git命令的输出
git config --global color.ui "always"
#查看所有的全局变量
git config --global --list
```

### 获取帮助信息

````shell
#查看所有可选的命令
git help
#查看具体的命令的使用方法
git help <command>
````

## 创建项目

### 初始化项目

```shell
#该命令会生成一个.git目录，存储版本库的全部元数据
git init
```

+ 在项目中创建文件，然后将文件添加到版本库的索引，再提交

```shell
#创建文件
touch test.html
#向版本库添加索引
git add test.html
#提交到本地版本库
git commit -m "创建了一个html文件"
```

+ 修改文件，查看文件状态

```shell
#更改文件之后查看项目状态
git status
#添加修改，如果要添加所有的修改到缓存区，可以使用git add .
git add test.html
#创建提交记录，如果用了`git commit -a`则会提交全部的修改
git commit -m "更改了文件"
#查看提交的相关信息
git log
#限制查看的日志条数
git log -2
```

> Git中有三个可以存放代码的地方：工作目录树，暂存区（staging area），版本库。工作目录树中的修改会被检测到，但是不能确定如何处理它们。如果要提交到版本库，必要暂存修改，然后在提交到版本库中。
>
> `git add` 命令可以添加新的文件，也可以添加新的修改到缓存区。
>
> `git commit`可以提交修改到版本库。

### 理解并使用分支


```shell
#分支命令 `git branch <新分支名称>  <父分支名称>`
git branch RB_1.0 master
#切换分支
git checkout RB_1.0
#删除分支
git branch -d 分支名
#强制删除分支
git branch -D 分支名
#列出所有的分支
git branch
```

### 处理发布，打标签


```shell
#给RB_1.0的末梢打上标签
git tag 1.0 RB_1.0
#查看所有的标签
git tag
```

### 归档处理

```shell
git archive --format=tar --prefix=mysite-1.0 1.0/ |gzip > mysite-1.0.tar.gz
git archive --format=zip --prefix=mysite-1.0 1.0/ > mysite_1.0.zip
```

> `--format`指明要产生tar格式的输出
>
> `--prefix`指明包中所有东西都放到mysite-1.0/ 目录下
>
> `1.0`指明要归档的标签名称

+ 通过打标签，可以使Git与现有开发流程交互协作，Git的归档命令则有助于创建项目源代码的发布包

### 克隆远程版本库

```shell
#克隆整个项目
git clone git://github.com/tswceegood/mysite.gitt mysite-remote
```

> `git clone`命令有两个参数，远程版本库的位置和存放该版本库的本地目录。第二个参数可选。

## Git基础

### 添加文件到暂存区

> `git add` 用来添加新文件和修改版本库中的已有文件的内容  
>
> `git add -i` 进入交互模式
>
> `git add -p`进入补丁模式

### 提交修改

> 跟踪空目录，临时解决方是在未来想跟踪的文件夹中添加一个空文件
>
> ---
>
> 三种提交方式：
>
> 1. 先用`git add xxx`暂存更改，再用 `git commit -m "第一种方式"`提交更改
> 2. `git commit -m "第二种方式" -a`，一次性提交所有的修改
> 3. `git commit -m "第三种方式" some-file`，提交指定的文件或文件列表，一般可以结合`git add -p` 暂存部分修改，然后在提交指定的文件或者文件列表
>
> ---
>
> 第一种方法是先缓存再提交，后两种方法是直接提交

### 查看修改内容

> 1. 查看文件状态，直接使用`git status `
>
> 2. 查看文件改动
>    + `git diff` 直接查看文件的更改
>    + `git diff --cached` 这个命令可以查看更改与版本库的区别，只有比较暂存的修改
>    + `git diff HEAD` 这个命令比较工作目录树（包括暂存和未暂存的修改）与版本库中的差别

### 管理文件

> `git mv <源文件名称> <新文件名称>`可以用来移动文件。Git会使用原来文件内容创建新文件，新文件将保留原文件的历史修改记录
>
> Git不复制文件，Git只关心文件内容，文件改动或者存在复制的行为，Git可以自动检测到它。
>
> 忽略文件的两种方式
>
> + 通过`.gitignore`文件中添加要忽略的文件或者文件规则，设置版本库级别的忽略
> + 在`.git/info/exclude`中添加忽略的文件或文件规则，设置本地级别的忽略规则

## 理解和使用分支

### 基本操作

+ 创建分支
+ 合并分支
+ 处理合并冲突
+ 删除分支
+ 重命名分支
+ 使用发布分支

> 试验性更改、增加新功能、Bug修复这几个场景适合创建分支

### 创建分支

#### 创建本地分支

```shell
#通过branch命令创建
git branch <新分支名称> <父分支名称>
#使用检出命令，一次性完成创建分支并检出该分支
git checkout -b <新分支名称> <父分支名称>
```

#### 创建远程分支

```shell
#创建远程分支，需要先创建并切换到本地分支，然后再将本地分支推送到远程仓库
git branch -b new_branch parent_branch
git push origin new_branch
```



### 合并分支

+ 直接合并，将一条分支的全部提交历史合并到另一条分支上

  ```shell
  #比如要合并一个分支到主分支，需要先检出到主分支
  #然后进行合并
  git checkout master
  git merge NB_1.0
  ```

+ 压合合并

  > 功能分支(Feature branch)，在已有分支上创建新的分支，用于开发新的功能或者修复Bug，通过一个压合提交将新分支上的更改合并回来。

  > 压合指的是Git将一条分支上的所有提交历史压合成一个提交，提交到另一条分支上。需慎重使用

  ```shell
  #压合提交语法
  git merge --squash <新分支名称>
  ```

+ 拣选合并

  > 从一个分支中的挑选一个提交合并到主分支中

  ```shell
  git cherry-pick 321d76f  #321d76f是提交名称
  ```

  > 从一个分支条挑选多个提交

  ```shell
  #该操作会将改动拣选并暂存，并不会立刻提交
  git cherry-pick -n 321d76f
  .............
  重复多次相同操作
  .............
  #不使用 `-m` 参数，Git会将拣选的所有提交的提交留言作为现在的提交留言 
  git commit
  ```

### 冲突处理

> 同一文件的同一文本块以不同的方式修改，并试图合并的时候，会发生冲突，需要人工处理。
>
> `<<<<<<<<<`表示本分支的内容，`>>>>>>>>`表示合并过来的分支的内容，`===========`用来分隔两个不同分支的内容。
>
> 通过`git mergetool`可以使用系统工具来解决冲突，解决之后要通过`git commit`提交

### 删除分支

#### 删除本地分支

```shell
#当分支中的内容没有合并到当前分支时，就会操作失败，需要使用`-D`参数，强制删除
git branch -d <branch-name>
git branch -D <branch-name>
```

#### 删除远程分支 

```shell
git push origin --delete BR_1.0
```



#### 分支重命名

> 分重命名语法
>
> `git branch -m <old-name> <new-name>`
>
> 使用参数`-M`将会强制覆盖已经存在的分支

## 查询Git历史

### 查看Git日志

```shell
#语法
git log
#查看版本之间代码差异
git log -p
#查看指定条数的日志
git log [-number]
#查看指定名称开始的日志
git log [-name]
```

### 指定查找范围

```shell
#查看最近5小时的提交
git log --since="5 hours"
#查看5小时之前的最后一个提交
git log --before="5 hours" -1
#类似的格式还有 --ince="24  hours" --since="1 minute" --before="2008-10.01"
#查看两个版本之家的提交
git log <old-verision-name>..<new-version-name>
#查询的日志以只显示名称（哈希值）的缩写和提交留言，与--prety=oneline同等效果
git log --pretty=format:"%h %s"
#显示18f822e前一个版本到最新版本之间的所有提交
git log 18f822e^..HEAD
#显示18f822e前10个版本到最新版本之间的所有提交
git log 18f822e~10..HEAD
```

### 查看版本之间的差异

```shell
#指定版本范围的方法与git log一致，差别是git diff输出的是最老和最新版本之间的差异
#查看指定版本的与当前版本之间的差异
git diff <version-name>
#统计版本之间的代码更改量
git diff --stat <version-name>
```

### 查明问责

> `git blame <file-name>`这条命令可以输出文件的更改信息，包括是谁更改了文件，什么时候更改了哪一个位置，以及提交留言
>
> `git blame -L [start,end] <file-name>`这个命令可以显示特定的开始行和结束行的修改情况
>
> `git blame -L [start] [+num|-num] <file-name>`有同等效果
>
> `git blame -L [start,end] <version-name> -- <file-name>`可以查看指定版本范围

### 跟踪内容

> 在 `git blame` 和 `git log` 的命令后面加上 `-C -C` 参数可以检测文件之间的复制情况 
>
> `git log -C -C -1 -p` 可以查看详细的变动

### 撤销修改

> 修改历史的操作只能在变更推入共享版本库之前进行修改，如果推入共享版本库之后再修改历史，其他人在同步时会遇到麻烦。
>
> 增补提交
>
> ```shell
> # -C 告诉Git复用指定提交的提交留言，而不是从头写一个。使用小写的 -c 会打开编辑器
> # 增补提交只能针对最后一个提交
> git commit -C HEAD -a --amend
> ```
>
> 反转提交
>
> ```shell
> #反转已经提交的改动，通过在版本库中创建一个“反向的”的新提交来抵消原来提交的改动
> #通常Git会提克提交反转结果，运行多个 git revert -n 命令，Git会暂存所有变更
> #使用反转提交需要指定提交名称
> git revert -n HEAD
> git revert -n 540ecb7
> #复位一个提交，Git暂存所有因复位带来的差异，但不提交它，好像默认是使用了 --soft
> git reset HEAD^ 
> #复位一个提交，--hard 选项会从版本库和工作目录中同时删除提交,需要慎重使用
> git reset --hard HEAD^
> #复位失败，还可以进行回滚
> #首先通过reflog查看HEAD记录
> git reflog
> #然后进行回滚
> git reset --hard <version-name>
> ```
>
> 小结：总的来说，回滚操作命令是有使用场景的，这个场景就是我们在写代码，然后已经将更改暂存到缓存区或者已经提交，那么，我们就可以通过回滚操作，将版本库的状态回滚到之前，通过 `--soft` 则是会使提交的更改重新回到暂存区，暂存区的更改回到未暂存的状态，而 --hard 则是会把这些更改全部删除。不过，即使是使用了 `--hard` 进行回滚，误删了之前提交的更改，也可以通过 `git reflog` 查看操作记录，然后再次回滚到正常状态。

### 重新改写历史记录

> 通过 `git rebase` 命令完成，但是这个功能不常用。
>
> 它可以对历史提交记录进行重新排序，将多个提交合并成一个提交，将一个大的提交分解成多个提交

## 与远程版本库协作

### Git 网络协议

+ Git 支持的网络协议包括 SSH协议，git自带的网络协议，以及HTTP/HTTPS协议
+ SSH协议链接以 `git@` 开头， git自带的网络协议的链接则以  `git://` 开头，HTTP/HTTPS协议的链接则以 `http://` 开头。

### 克隆远程版本库

```shell
git clone git://github.com/your/project/path.git
```

### 版本库同步

+ 远程分支

  ```shell
  #加上 -r 参数可以查看远程版本库的所有分支
  git branch -r
  #可以像检出本地普通分支那样检出远程分支，但是不应该修改分支，如果要修改，就应该先从远程分支创建一个本地分支，，然后再进行修改
  #创建本地分支的两种方法
  #1.直接创建分支
  git branch new-local origin/new
  #2.先检出到远程分支，再创建本地分支
  git checkout origin/new
  git switch -c new-local
  ```

+ 同步

  ```shell
  #fetch操作可以更新远程分支，但不会将远程分支上的修改合并到本地分支上
  git fetch
  #pull操作会完成两件事：取来，然后合并
  #origin 是默认的远程版本库别名，new则是要拖入的远程分支名
  git pull origin new
  ```

### 推入改动

> 推入操作是把本地改动推入到上有版本库，以实现共享。

```shell
#push命令会把更改推入默认的版本库origin中与当前分支相对应的远程分支中
git push
#加上 --dry-run 参数可以查看推入了哪些提交
git push --dry-run
#推入指定版本库的指定分支，<repository>可以是网络协议支持的任何URL
git push <repository> <refspec>
```

### 添加新的远程版本库

```shell
#语法：git remote add <name> <repo-url>
#origin是默认的版本库名称，可以用其他的别名代替
git remote add origin git://ourcompany.com/dev-erin.git 
#这个命令可以查看某个远程版本库的详细新消息
git remote show <name>
```