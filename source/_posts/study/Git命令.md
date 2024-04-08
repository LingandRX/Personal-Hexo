---
title: Git命令
date: 2023-07-19 11:56:27
tags: 
    - git
categories:
    - [学习]
---

## 初始化仓库

``` shell
# 使当前目录初始化为git仓库，同时会生成一个.git隐藏的文件夹，或者重新初始化现有仓库
git init
# 指定一个目录成为git仓库，同时会生成一个.git隐藏的文件夹
git init newRepo
```

## 克隆远程仓库

```shell
# 克隆仓库
git clone <repo>
# 将仓库克隆到指定目录
git clone <repo> <directory>
```

## 基本操作

```shell
# 上传远程代码合并
git push

# 下载远程代码合并
git pull

# 将文件添加到暂存区
git add

# 查看仓库的当前状态,显示有变更的文件
git status

# 比较文件的不同,即暂存区和工作区的差异
git diff

# 将文件添加到暂存区
git commit

# 回退版本
git reset

# 将文件从暂存区和工作区删除
git rm

# 移动或者重命名工作区文件
git mv

# 切换分支
git checkout

# 查看提交日志
git log

# 查看指定文件的修改日志
git blame <file>

# 命令help
git <commond> help

# 合并分支，合并到当前分支
git merge [目标分支]
```
