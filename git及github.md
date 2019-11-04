

# Git及Github的使用

> 本文讲述Git的基本概念及本地库基本使用方法等。

####  

**版本控制工具**：协同修改、数据备份、版本管理、权限控制、历史记录、分支管理。

---



#### Git的基本介绍

- 是一种采用文件系统快照对的方式，对每个版本的文件信息进行管理的工具，即版本控制工具。SVN则采用增量式管理的方式。

- 是一种分布式版本控制工具，而SVN则是集中式控制。

  > 1、分布式版本控制系统没有“中央服务器”，每个人的电脑都是一个完整的版本库，不用联网安全性相对于集中式版本控制系统要高很多。
  >
  > 2、分布式版本控制系统还拥有强大的分支管理能力，允许开发团队在工作过程中多条生产线同时推进任务，大大提高效率。

- 对团队外参与开发人员进行权限控制，对其代码进行审核。

---

#### Git命令行操作

##### 1.设置签名

分别在命令行中输入以下代码，进行user.name和user.email的设置

`git config --global user.name [user.name]`

`git config --global user.email [user.email]`

![gKoYGu.png](https://t1.picb.cc/uploads/2019/11/04/gKoYGu.png)

**--global** 是系统用户级别，信息保存在`：~/.gitconfig `文件中。

可以通过`$ cat ~/.gitconfig`命令查看。

![gKoTlF.png](https://t1.picb.cc/uploads/2019/11/04/gKoTlF.png)

##### 2.创建本地库

选择合适的地方，创建空目录并进入（可以不按照默认路径）。

```git
$mkdir gitwork
$cd gitwork
```

**可以输入`pwd`查看当前显示的目录**

##### 3.仓库初始化

`git init`

![gKozM1.png](https://t1.picb.cc/uploads/2019/11/04/gKozM1.png)

初始化成功，当前目录下多出了`.git`目录，不能随意修改或者删除。

可以使用`ls -ah`查看隐藏的`.git`

##### 4.状态查看

`git status`

![gKoLUJ.png](https://t1.picb.cc/uploads/2019/11/04/gKoLUJ.png)

当前为空库，所以no commits .分支为master.

##### 5.添加文件



> 1、想要添加文件，得先写一个文件。用`vim [filename]`写一个.txt文件，关于[vim](https://www.cnblogs.com/itech/archive/2009/04/17/1438439.html)的在此不做过多的探究，退出键为`ESC`,再输入`：wq`，文件便创建完成。
>
> 2、使用`git add [filename]`命令，将文件加到暂存区。

>![gKoRYt.png](https://t1.picb.cc/uploads/2019/11/04/gKoRYt.png)

> 可以发现，出现了warning语句。注意：
> warning: LF will be replaced by CRLF in app.wxss.
> The file will have its original line endings in your working directory.
> 原因是路径中存在 / 的符号转义问题，false就是不转换符号默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题.解决方法就是输入以下命令，接着按原计划走。

> `git config --global core.autocrlf false`

![gKoF4T.png](https://t1.picb.cc/uploads/2019/11/04/gKoF4T.png)

##### 6.提交文件

此时再次输入`git status`命令，可以查看仓库的状态，以加深对工作区，暂存区和本地库的理解。

![gKoBV6.png](https://t1.picb.cc/uploads/2019/11/04/gKoBV6.png)

> 一个新的文件被加入到暂存区，就是绿色部分所显示的。**将“新建、修改”的文件添加至暂存区**。

`git commit -m "message"[filename]`

![gKoPjM.png](https://t1.picb.cc/uploads/2019/11/04/gKoPjM.png)

> **将暂存区的内容提交至本地库。**

##### 7.历史记录

`git log`

![gKosf0.png](https://t1.picb.cc/uploads/2019/11/04/gKosf0.png)

> 当然，这里作为演示，只有一步行为。在实际的应用过程中，版本更新的频率是很高的，所以为了看着舒适清晰，可以采用以下命令：
>
> ```git
> git log --pretty=oneline 包含sha1哈希值，指针指向，以及commit内容
> git log --oneline  包含一小部分sha1哈希值，指针指向以及commit内容
> git reflog 包含一小部分哈希值，HEAD@{移动到当前版本需要的步数}以及commit内容
> ```

##### 8.前进后退

> 在提交了多次修改申请之后，界面变成如下：

> - 后退：`git reset --hard HEAD^` 表示后退一步

![gKoDFd.png](https://t1.picb.cc/uploads/2019/11/04/gKoDFd.png)

>   `提示：HEAD is now at f435d69 commit youfirst.txt`
>
> ​	`git reset --hard HEAD~n` 表示后退n步
>
> ​	`git reset --hard[index] `基于索引值
>
> - 前进：只能基于索引值，推荐使用。
>
> 前进或者后退，HEAD指针都在随着版本更新，在变化。

---

**reset三个参数的对比**

- --soft:仅仅在本地库中移动HEAD指针。

- --mixed：在本地库中移动HEAD指针。

   		重置暂存区。

- --hard：在本地库中移动HEAD指针。

  ​		重置暂存区。

  ​		重置工作区。

---

##### 9.删除文件

`前提`：删除前，文件存在的状态提交到了本地库。

`git reset --hard[指针位置]`

- 删除操作已经提交到了本地库：指针位置指向历史记录。
- 删除操作尚未提交到本地库：指针位置使用HEAD。

##### 10.比较文件差异

`1、git diff[filename]`:将**工作区**的文件和**暂存区**进行比较。

![gKoKVa.png](https://t1.picb.cc/uploads/2019/11/04/gKoKVa.png)

`2、git diff[本地库中的历史版本][文件名]`：**工作区**和**本地库**中的历史记录比较。

3、不带文件名比较多个文件。

---

