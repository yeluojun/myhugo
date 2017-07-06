---
title: "工作中使用到的git的命令集合-持续更新"
date: 2016-09-01T19:21:33+08:00
tags: ["git"]
categories: ["git"]
---

## 工作中用到的git命令集合

<!--more-->

>
配置部分：
>
    git config --global user.name "yeluojun" ; 设置全局用户名
    git config --global user.email "635143970@qq.com" ; 设置全局邮箱
    git config -l  ; 查看所有配置
----
>    
clone 部分：
>   
    git clone <路径> ； clone项目
    git clone -b <分支> <路径> ; clone特定分支

----
>
git add and rm :
>
    git add <file/dir> ; 将文件(夹)提交到本地暂存区
    git add . ; 将所有有修改过的文件（包括添加，删除，修改）提交到本地暂存区
----
>
    git rm <file/dir>  ; 从版本库中删除文件   
    git rm <file/dir> --cached ; 从版本库中删除文件，但不删除文件
----
>  
    git show  ; 查看最近一次提交的内容  
    git status ; 查看工作区状态  
----
>
checkout部分：
>  
    git checkout branch ; 切换分支  
    git checkout -b branch ; 新建一个分支并切换到该分区  
    git checkout -- <文件> ; 撤销对某个文件的修改  
    git checkout -- . ; 撤销所有未提交的修改
----    
>
分支管理：
>  
    git branch ; 查看所有分支  
    git branch -a ; 查看所有分支(包括远程分支)  
    git branch <分支名> ; 新建一个分支   
    git branch -d <分支名> ; 删除分支（未合并该分支到当前分支会报错）  
    git branch -D <分支名> ; 强制删除分支(无法删除当前所在的分支)
----
>    
拉取/提交更新：
>
    git pull origin <分支名> ; 拉取远程更新  
    git push origin <分支名> ; 提交到远程
    git push origin :<分支名> ; 删除远程分支
----
>
版本回滚：
>
    git log ; 查看commit信息
    git reset  --hard ; 恢复最近一次提交过的状态
    git reset  --hard  e96a05d37b9c8d0d02aec488ed9ec629c18b2396 ; 回复某个commit的版本
----
>
远程仓库管理:
>
    git remote ; 列出所有的远程仓库
    git remote -v ；列出所有远程仓库及其地址
    git remote add origin <地址> ; 添加远程仓库地址， origin为仓库名称，可以是其他名称比如 "a", "b" ...,
    git remote rm origin ; 删除名为“origin” 的远程仓库
    git remote set-url origin <地址> ； 修改名为“origin”的远程仓库的地址
----
>
 git fetch 相关：
>
    git pull origin dev 相当于：
    git fetch origin dev
    git merge origin/dev
>    
    git fetch -p ; 删除远程已经删除但本地还存在的分支，并拉取所有远程分支

>
    拉去其它分支的更新，合并到自己的分支：
    git fetch origin <分支名>
    git rebase origin/<分支名>
----
>
合并分支：
>
    git merge <分支名>; 合并分支

----
----

> 暂时用过的基本就这些，持续更新ing...
