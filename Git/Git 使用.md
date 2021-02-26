
## git 介绍及安装
`git` 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

 查看 `git` 版本 `git --version`

- [安装文档](https://www.jianshu.com/p/33108325fc87)
- [菜鸟教程](https://www.runoob.com/git/git-tutorial.html)
- [参考文档1](https://mp.weixin.qq.com/s/oGDzalW3BF57Jg1NpNIfkw)
- [参考文档2](https://mp.weixin.qq.com/s/DjpzC-XWm7M8b4B-SujopQ)
  

## git 常用指令
```
克隆远程仓库的内容到本地
git clone git@github.com:nohosts/nohost.git 

获取远程分支master并merge到当前分支
git pull origin master 

查看全部分支（远程+本地）
git branch-a

新建bugFix，并切换到到此分支。（如果分支已存在则去掉-b即可）
git checkout-b bugFix

查看当前~~~~版本状态（是否修改）
git status 

增加当前子目录~~~~下所有文件更改至暂存区
git add. 

提交暂存区的修改至本地的版本库, 修改备注为xxx
git commit-m'xxx' 

将本地版本推送到远程分支
git push 

增加v1.0的tag到某个提交上
git tag v1.0 


合并testBranch分支至当前分支
git merge testBranch 

暂存本地的当前修改，将本地代码重置为HEAD状态。（如果需要取出修改，命令后加一个pop即可）
git stash 

显示提交日志（如果想每个提交信息显示在一行，可以加上--pretty=oneline）
git log 

显示某个提交的详细内容
git show 

将当前版本重置为HEAD
git reset--hard HEAD 
```

## git 操作流程
  
![git 操作流程](https://static01.imgkr.com/temp/b7a89aae9c2a42b7958acf0510fadabc.jpg)

## .git 的文件夹
  - `hooks`  目录包含客户端和服务端的钩子脚本
  - `info`   包含一个全局排查文件 
  - `logs`   保存日志信息   
  - `objects` 目录存储所有数据内容
  - `refs`    目录存储指向数据(分支)的提交对象的指针
  - `config`  文件包含项目特有的配置选项 
  - `description`  用来显示对仓库的描述信息 
  - `HEAD`  文件指示目前检出的分支
  - `index`  文件保存暂存区信息

## git 配置

- **查看**
  > `git config --xxx --list`
  
  xxx 可选参数
    - `local`  查看 Repository 配置
    - `global` 查看 全局配置
    - `system` 查看 系统配置

- **修改**
  > `git config --xxx user.name "姓名"`
  >
  > `git config --xxx user.email "邮箱"`
  
  xxx 可选参数
    - `local`  修改 Repository 配置
    - `global` 修改 全局配置
    - `system` 修改 系统配置

- **删除**
  > `git config --xxx --unset user.name`
  >
  > `git config --xxx --unset user.email`
  
  xxx 可选参数
    - `local`  删除 Repository 配置
    - `global` 删除 全局配置
    - `system` 删除 系统配置


## git 创建仓库

- 初始化仓库

  > `git init`

- 克隆远程仓库

  > `git clone xxxxx`
  
## 关联远程仓库
- 初始化仓库 后 关联 远程仓库

  > `git remote add <name> <git-repo-url>`
  >
  > `git remote add origin https://github.com/xxxxxx`

## add 添加到暂存区

- 添加一个或多个文件到暂存区 

  > `git add [file1] [file2] ...`
  
- 添加指定目录到暂存区，包括子目录

  > `git add [dir]`
  
- 添加当前目录下的所有文件到暂存区      
  > `git add .` 等价于 `git add -A`
 
## branch 分支

- 查看本地分支

  > `git branch`
  
- 查看远程分支

  > `git branch -r`
  
- 查看本地和远程分支 

  > `git branch -a`

- 创建分支 

  > `git branch <branch-name> `
  
- 创建并切换至此分支 

  > `git checkout -b <branch-name>`

- 删除分支 

  > `git branch -d <branch-name>`

- 当前分支与指定分支合并 

  > `git merge <branch-name>`

- 查看哪些分支已经合并到当前分支 

  > `git branch --merged`

- 查看哪些分支没有合并到当前分支 

  > `git branch --no-merged`

- 查看各个分支最后一个提交对象的信息

  > `git branch -v`
  
- 删除远程分支

  > `git push origin -d <branch-name>`
  
- 重命名分支
  
  > `git branch -m <oldbranch-name> <newbranch-name>`
  
- 拉取远程分支并创建本地分支
  
  > `git checkout -b 本地分支名x origin/远程分支名x`


## commit 提交

- 将暂存区的文件提交到本地仓库并添加提交说明 

  > `git commit -m "本次提交的说明"`
  

## status 

- 查看工作区和暂存区的状态

  > `git status`
  

## push 推送 

- 推送至远程仓库

  > `git push`
  

 
  
  
