### Github远程库与Git本地库连接

- 创建SSH Key
  - 用户主目录有`.ssh`->`id_rsa`和`id_rae.pub`->直接跳过
  - 若没有->`ssh-keygen -t rsa -C["邮件地址"]`->回车完事
  - 将`id_rsa.pub`里的内容复制粘贴到`Github`->`Account settings`->`SSH Keys`->`Add SSH Hey`

- 添加远程库

  - `本地Git仓库`-->`远程Github仓库`
  - 在Github上创建一个新的仓库->`Create repository`
  - `git remote add [别名][仓库地址] `->别名一般为origin 
  - `git remote -v`->可以查看当前所有远程地址别名
  - **这里讲的是用https方式上传，每次都会验证账号密码，会比较麻烦，可以参考下面解决方案。**

- 推送文件

  - `git push [别名][分支名]`

  - Github提交代码输入的用户名和密码：

    - 默认方式https: 账号：user.email

      ​		 密码：token

    - 解决方法->转换为SSH

      1.`git remote -v `查看是什么方式

      2.`git remote rm origin` 移除https方式换成ssh方式

      3.复制ssh地址。

      4.`git remote add origin [复制的地址]`

      5.`git remote -v`查看是否更改成功

      6.`git push origin master`重新提交

- 克隆文件

   - `git clone [远程地址]`
     - 把远程库下载到本地
     - 创建origin远程地址别名
     - 初始化本地库



