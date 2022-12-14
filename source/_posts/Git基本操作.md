---
title: Git基本操作
date: 2022-12-14 20:08:34
tags:
    - Git
    - 编程工具
categories: 编程技巧
cover: /assets/img/cover/7.webp
---

# Git 基本操作

## 1. cherry-pick

[git cherry-pick 教程](https://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)

``` bash
# 将指定的提交应用于其他分支
git cherry-pick <commitHash>

# A B均为commit的hash值，转移A-B不包括A的提交
git cherry-pick A..B

# A B均为commit的hash值，转移A-B不的提交
git cherry-pick A^..B 
```

## 2. 合并几个提交

[Git 合并多个 commit](https://segmentfault.com/a/1190000007748862)

``` bash
# 从HEAD版本开始往过去数3个版本
git rebase -i HEAD~3

# 执行完上述步骤后，会弹出文本编辑器，将除第一行的pick全都改成squash或者s，保存

# 执行完上一步后，修改冲突（如果有的话），修改提交信息
```

## 3. 删除远程分支

``` bash
# 删除本地分支
git branch -d <localBranchName>

# 删除远程分支
git push origin --delete <remoteBranchName>
```

## 4. 添加远程仓库并首次推送

``` bash
# 添加远程仓库
git remote add origin git@ip:diretory/project.git
# 查看远程仓库
git remote -v
# 修改远程仓库
git remote set-url origin <new git>
# 首次推送
git push -u origin main
```
