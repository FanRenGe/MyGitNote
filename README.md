# MyGitNote

> 参考网站 [Git教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

> windows下安装 msysgit 参考：<http://blog.chinaunix.net/uid-25806493-id-3319781.html>

## 一、 安装Git

在window系统下安装Git 需要安装 msysgit ，从 <https://git-for-windows.github.io> 下载最新的安装程序。  
安装完成后，在开始菜单里找到 **“Git”->“Git Bash”** ，蹦出一个类似命令行窗口的东西，就说明Git安装成功！  
安装完成后，还需要最后一步设置，在命令行输入：
``` shell
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 二、创建SSH Key

在用户主目录下,一般在 C:\Users\你的用户名\\.ssh）(mac: /Users/用户/.ssh）看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
``` shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有 id_rsa 和 id_rsa.pub 两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
将ssh文件夹中的公钥（ id_rsa.pub）添加到GitHub管理平台中，在GitHub的个人账户的设置中找到

    SSH and GPG kyes -- SSH keys -- Add new 
    
title随便起一个，将公钥（ id_rsa.pub）文件中内容复制粘贴到key中，然后点击Ass SSH key就好啦
测试一下配置是否成功，在Git Bush命令框（就是刚才配置账号和邮箱的命令框）中继续输入以下命令，回车
 ``` shell
$ ssh -T git@github.com
```
要是看见下面的这句话就说明配置好啦
``` shell
Hi <yourname>! You've successfully authenticated, but GitHub does not provide shell access.
```
## 三、常用命令

``` shell
$ git init    #初始化一个Git，及把当前目录变成Git可以管理的仓库
    Initialized empty Git repository in /Users/michael/learngit/.git/

$ git add <file name>  #把文件添加到仓库

$ git add .    #把当前目录下所有文件添加到仓库

$ git commit -m "commit message"   #把文件提交到仓库，-m后面输入的是本次提交的说明，不能为空

$ git status    #查看工作区状态

$ git diff      #查看修改的内容

$ git diff HEAD -- <file name>   #查看工作区和版本库里面最新版本的区别 

$ git log --pretty=oneline     #查看历史提交日志 ,参数--pretty=oneline 每条日志按一行显示

$ git reset --hard HEAD^       #回退到上一个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

$ git reset --hard 3628164     #回退到指定的版本， 可以是之前的也可以是之后的

$ git reflog                   #查看命令历史

$ git checkout -- readme.txt   #丢弃工作区的修改。意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或git add时的状态。

$ git reset HEAD readme.txt    #把暂存区的修改撤销掉（unstage），重新放回工作区，git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。 

$ git rm test.txt              #删除文件，执行该命令后需要 执行commit

$ git remote add origin git@github.com:michaelliao/learngit.git  #在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

$ git push -u origin master    #把本地库的所有内容推送到远程库上，由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

$ git push origin master       #第一次推送之后，即使用改命令即可。如果要推送其他分支，比如dev，就改成：$ git push origin dev


################################
…or create a new repository on the command line

echo "# Dictation" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:FanRenGe/Dictation.git   # 通过 命令在 github上新建项目
git push -u origin master

…or push an existing repository from the command line

git remote add origin git@github.com:FanRenGe/Dictation.git
git push -u origin master
##########################################


$ git clone git@github.com:michaelliao/gitskills.git   #从远程库克隆到本地库

$ git branch                   #查看分支

$ git branch <name>            #创建分支

$ git checkout <name>          #切换分支

$ git checkout -b <name>       #创建+切换分支

$ git merge <name>             #合并某分支到当前分支

$ git branch -d <name>         #删除分支

$ git branch -D <name>         #强行删除，如果要丢弃一个没有被合并的分支可以使用该命令

$ git log --graph --pretty=oneline --abbrev-commit  #查看分支合并图

$ git merge --no-ff -m "merge with no-ff" dev   #--no-ff参数，表示禁用Fast forward，因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

$ git stash  #可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

$ git stash list #查看藏匿列表

$ git stash apply #恢复藏匿，但是恢复后，stash内容并不删除

$ git stash drop    #删除藏匿

$ git stash pop     #回复藏匿的同时把其删掉

$ git remote -v     #查看远程库信息， -v 详细信息

$ git checkout -b dev origin/dev    #创建远程origin的dev分支到本地

$ git pull            #把当前分支的最新的提交抓下来

$ git branch --set-upstream dev origin/dev   #如果git pull失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接，之后在 pull

$ git tag <name>       #用于新建一个标签，默认为HEAD，也可以指定一个commit id；

$ git tag -a <tagname> -m "blablabla..."    #指定标签信息

$ git tag -s <tagname> -m "blablabla..."     #用PGP签名标签,-s用私钥签名一个标签,签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错,请参考GnuPG帮助文档配置Key。

$ git tag                                    #查看所有标签

$ git show <tagname>                         #查看标签信息

$ git tag -d v0.1                            #删除标签

$ git push origin v1.0                       #推送某个标签到远程

$ git push origin --tags                     #一次性推送全部尚未推送到远程的本地标签  

$ git push origin :refs/tags/v0.9            #删除一个远程库的标签，如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除，再执行此命令

$ git config --global color.ui true      #Git会适当地显示不同的颜色

$ git config --global alias.co checkout  #设置命令的别名（简写）
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
$ git config --global alias.unstage 'reset HEAD'
$ git config --global alias.last 'log -1'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

如果想在本地忽略某个文件的话执行这个命令:

$ git update-index --assume-unchanged <file>

如果想重新同步这个文件的话执行这个命令.

$ git update-index --no-assume-unchanged <file>
```

## 四、自定义Git

忽略特殊文件: <https://github.com/github/gitignore/blob/master/VisualStudio.gitignore>

多人协作的工作模式通常是这样：

    首先，可以试图用git push origin branch-name推送自己的修改；

    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

    如果合并有冲突，则解决冲突，并在本地提交；

    没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。
