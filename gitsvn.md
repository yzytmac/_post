---
title: git-svn总结
date: 2019-02-25 15:15:07
tags: 版本控制
categories: git-svn教程
thumbnail: https://gitee.com/yzytmac/resource/raw/master/git.png
---
## 写在前面
个人喜欢用git,但工作中主要还是svn,如何使用git来控制svn的项目呢,有请主角git-svn登场
## 安装
在Linux中需要安装git, svn, git-svn
```bash
sudo apt install git subversion git-svn
```
在mac中只需安装git和svn,因为git中已经包含了git-svn
```bash
brew install git subversion
```
## 命令
```bash
# 拉取一个项目
git svn clone xxx [--username=xxx]

# 更新svn仓库的代码
git svn rebase

# 本地的一些操作增删改查,都是在git下完成
git log [--author=xxx] #查看(某人的)日志,用git svn log -v查看的更详细
git status #查看状态
git add * #添加所有修改
git commit -m "xx" #提交到git本地仓库
git reset --hard HEAD #恢复所有修改到本地最新版本
git reset HEAD file #丢弃暂存区的修改
git revert HEAD #取消上一次的提交
git branch new_branch_name #创建新分支
git checkout -b new_branch_name #创建并跳转到新分支
git branch -d branch_name #删除分支
git diff #显示工作去与暂存区的修改

# 提交svn仓库
git svn dcommit
```
## 常见问题
```bash
#当执行git svn rebase更新代码时可能会提示下面错误 
branches/xxx/.idea/misc.xml: needs update
update-index --refresh: command returned error: 1
#说明本地与服务端冲突了,只需执行下面操作即可解决
git update-index --refresh xxx/.idea/misc.xml
#或者执行下面命令,意思是假设本地文件没有改变
git update-index --assume-unchanged xxx/.idea/misc.xml

```
## 总结
与svn服务器有关的操作就用git svn命令开头,仅仅在本地的操作就用git开头
