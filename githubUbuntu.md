---
title: 'GitHub on Ubuntu'
---

# git 的安装

```bash
sudo apt-get install git git-core git-gui git-doc git-svn git-cvs gitweb gitk git-email git-daemon-run git-el git-arch
```

可以通过命令 `ssh -T git@github.com` 检查是否可以连接到 GitHub.

*ssh*:  [secure shell, 安全外壳协议](http://en.wikipedia.org/wiki/Secure_Shell)

# 创建共用信息


## 注册

Go to <https://www.github.com>, create an account.

<!-- account: rhohz -->

## 设置 git 全局信息

```bash
git config --global user.name 'accounName'
git config --global user.email 'emalAddress'
```

<!-- accountName: rhohz;  emailAddress: rhozhanghz at gmail dot com -->

通过命令 `git config --list`　查询当前配置信息

## 生成 SSH key

检查~/.ssh目录下是否有id_rsa（私钥）和id_rsa.pub（公钥）文件，如果有，则备份出来，删除原文件，再执行如下语句, 否则直接执行如下语句：

```bash
    ssh-keygen -t rsa -C "emailAddress"
```

三次回车生成秘钥，第一次回车指定密钥存放路径，默认为`~/.ssh`. 后两次回车确认密钥地密码，默认为空。

> strike Enter directly when asked ''Enter file in which to save the key''

> Enter passphrase (empty for no passphrase):

> Enter same passphrase again: 

## 设置github上的公钥

将id_rsa.pub文件中的字符串复制到 clipboard，以备后用。

```bash
   sudo apt-get install xclip
   xclip -sel clip < ~/.ssh/id_rsa.pub
```

登陆 github ->  "Account Setting"  ->  "SSH Keys"  -> "Add SSH Key"

- Title处填写该公钥的描述，如：ssh key for rho's dell desktop

- 在Key处，Ctrl + v, 将我们刚才复制到clipboard上的内容黏贴到该处。

- 每台电脑都需要一个SSH Key，但不是每个项目都需要一个SSH Key

通过命令 ` ssh -T git@github.com` 测试设置是否成功

当看到如下提示，说明添加成功：

> Hi rhozhang! You've successfully authenticated, but GitHub does
> not provide shell access.

# 在 github 上创建项目

- 在github账户中选择创建一个新的 repositories ，输入项目名称和描述，以及设置是否公开，是否需要添加 README 等等。创建完项目后，
该项目会有一个 http 地址和一个 SSH 地址，其中SSH 地址格式为：git@github.com:Account_Name/Repository_Title.git，该地址就是项目地址。

# 项目同步

## 从本地直接创建

- 进入项目所在目录，执行命令 `git init` 以创建一个仓库。

- 执行命令 git add . 选择需要添加到仓库中的文件。其中 “.” 表示将当前目录中的所有文件添加进仓库，如果想指定具体文件，则将 “.” 替换为具体文件名即可。

- 执行命令 `git commit -m 'description'` 提交add指定的文件到仓库。

- 执行命令 `git remote add origin git@github.com:Account_Name/Repository_Title.git` 建立本地仓库与远程github项目的链接

## 从 github 服务器已有的项目创建

### 克隆

若 github 的账户名为 *rhohz*，项目仓库（repository）名为：*tools.git*，你希望克隆后的路径为：*~/rhoKlive/tools*

```bash
cd rhoKlive
git clone https://github.com/rhohz/tools.git
```

### Commit and Push

本地产生一些文件后，提交给github：

```bash
   git add .    //往暂存区域添加已添加和修改的文件, 不处理删除的文件, --no-ignore-removal 则处理删除文件
   git status   //比较本地数据目录与暂存区域的变化
   git commit -m "add files" //提到代码到本地数据目录，并添加提交说明
```

可能你和其他人改的是同一个文件，这样形成了冲突。我们需要在提交之后再获取一下代码，就会提示代码冲突的文件，我们需要做的就是处理这些冲突，并再次提交：

```bash
   git pull     //更新代码, 根据提示修改冲突文件中的代码
   git add .
   git commit -m "commit directions"
```

做完以上步骤，把本地数据目录的版本库的数据同步到GitHub服务器上去，这样你的同事才能够看到你作出的修改：

```bash
git push -u origin master
```

# Miscellaneous: [Remove a Repository](https://help.github.com/articles/deleting-a-repository)

In GitHub

- navigate to the repository you want to delete;

- in the repository action bar, click **settings**;

- under danger zone, click *delete this repository*;

- read the warnings. To verify that you are deleting the correct repository, type the name of the repository you want to delete.

- click *I understand the consequences, delete this repository*.

# 参考文献

- <http://www.linuxidc.com/Linux/2012-06/62168p2.htm>

- <http://justcoding.iteye.com/blog/1829698>

- <http://www.pythoner.com/263.html>
