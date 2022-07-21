# Git简介

是一个分布式版本管理工具

追踪目录（文件夹）和文件的修改历史



# 基础命令

* 设置全局用户

    ~~~powershell
    git config --global user.name "用户名"
    git config --global user.email "电子邮件"
    ~~~

* `git init`建立仓库,在指定的目录文件夹下执行该命令，将建立该文件夹的仓库

* `git add`将文件添加到暂存区

    * `.`添加当前目录下的所有文件
    * `[file1] [file2]`添加指定文件
    * `[dir]`添加指定目录包括子目录

* `git commit -m "提交描述"`将暂存区文件提交到仓库
* `git log`查看仓库提交记录
* `git diff <filename>`查看差异
* `git reset --hard <head>`恢复到指定版本
    * head^上个版本
    * head^^上上个版本
    * head~n 往上n个版本

* `git reflog`查看历史操作记录

# 远程仓库

* `git remote add <name> <url>`添加远程数据库

    * name:远程数据库在本地的别名
    * url:远程数据库的url

* `git push <repository> <refspec> `推送本地仓库到远程仓库

    克隆的数据库目录执行推送时，您可以省略数据库和分支名称。

    * repository:要推送的远程仓库
    * refspec：要推送的分支

* `git clone <repository><directory>`复制远程仓库到本地

    * `repository`要复制到远程仓库
    * `directory`复制仓库的文件夹

* `git pull <repository><refspec>`将远程仓库的最新版本拉去到本地

在执行pull之后，进行下一次push之前，如果其他人进行了推送内容到远程数据库的话，那么你的push将被拒绝。



# 分支























