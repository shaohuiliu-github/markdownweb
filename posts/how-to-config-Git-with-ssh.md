**Shaohui Liu**

**[Home](../index.html)    [Posts](../posts.html)    [Timeline](../timeline.html)    [Research](../research.html)**

---

### 如何用Git上传代码到Github

### 1 新建代码库

在github上选择右上角“+”，“New repository”，输入仓库名例如“markdownweb”

### 2 添加ssh公钥

将本地代码上传到github，需要配置ssh key。

1. 下载并安装Git。安装之后在终端输入git version，显示版本号即为安装成功（Windows系统用Git bash终端）。

2. 设置Git基本信息，终端输入以下命令：

   `$git config --global user.name "your github name"`

   `$git config --global user.email "your github login email" `

3. 在本地创建ssh key：

   `$ssh-keygen -t rsa -C "your github login email"`

   输入之后回要求输入路径和密码，建议不输入直接回车。之后会在“～/”文件夹下生成“.ssh”文件夹，执行以下命令：

   `$cat ~/.ssh/id_rsa.pub`

   复制出现的内容，例如“ssh-rsa XXXXXX email.com”。（注：如果之前有本地配置过ssh，记得去“config”文件夹里查看新生成的是哪个ssh，`$ls -l`可以查看文件夹生成时间）

4. 将本地ssh添加到Github：

   在Github上选择“Settings”，“SSH and GPG keys”，“New SSH key”，将上一步所复制的内容添加。

5. 验证是否添加成功：

   在终端(Mac/Linux)或者Git bash(Windows)中输入：`$ssh -T git@github.com`，按照提示输入（**注：这里很容易疏忽把回车当作yes输入导致出错**）

   若最终显示：“You've sucessfully...”，则表示连接成功。

### 3 本地仓库传到github

本地文件夹自己创建/从连接到的github上拷贝下来。在本地修改文件之后，存到缓存区并添加commit，之后上传到github。

1. 进入本地文件夹，并在终端或者Git bash中输入：`$git init`
2. 连接本地和github上的仓库：`$git remote add origin [your github repository ssh link]`，其中[your github repository ssh link]替换为ssh链接，例如：`git@github.com:shaohuiliu-github/markdownweb.git`
3. 拉取github仓库到本地：`$git pull origin main`，根据分支名字是main还是master进行替换。
4. 修改本地文件
5. 添加本地文件到缓存区：`$git add .`，有.表示添加文件夹中所有文件，也可add后加文件名。
6. 为文件添加注释：`$git commit -m "first push"`，引号内到为注释
7. 提交文件到github中：`$git push origin main`，等待提交完成即可

注：当git add 单一文件出现warning时，在命令行输入`$git config --global core.autocrlf false`来禁止自动转换即可

### 4 代码总结

后续在相同文件夹中上传的话，执行：

```bash
$git add filename
$git commit -m "xxxx"
$git push origin main
```

后续要删除的话，执行：

```bash
$git pull origin main #拉取远程仓库
$git rm -r --cached filename #delete file
$git commit -m "xxxx"
$git push origin main
```

即后续在本地文件夹例如“markdownweb”里面，执行add、commit、push即可
