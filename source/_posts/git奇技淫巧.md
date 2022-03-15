---
title: git奇技淫巧
date: 2021-04-29 16:04:42
tags:
---

# git commands
```
git init
git log
git branch
git checkout
git reset
git switch
git add
git commit
git status
```

# differences between commands

## git主要分解为三部分
+ working directory，index，repository。
+ 其中working directory为当前工作目录，通过git add *把文件添加到index进行追踪（但要注意此时并没有把文件修改commit到snapshot）。再通过git commit添加当前index中的内容到当前HEAD所指向的branch的commit当中，并下移一条

## 理解三大概念：commit, branch, HEAD
+ 每一个commit有一个hash的commit ID，可以通过指定branch当作指向某个具体commit ID的指针，而HEAD是有且只有一个的指向当前branch（正常模式）或commit（detach模式）的指针。
+ branch is only a pointer to a specific commit

## 把commit当作一条指向父节点的链表
这解释了为什么git checkout到某个指定的commit时只能看到更早时的commit，而不能看到不在此链上的commit。

## branch与tag的区别
branch会随着HEAD指向的commit而移动，而tag只会跟随某个指定commit不再移动

## reset与checkout的区别
checkout移动HEAD到指定commit但保持branch不变，而reset直接把当前HEAD指向的branch也移动到对应commit

## branch internals
+ The concept behind branching is that each snapshot can have more than one child. Applying a second change set to the same snapshot creates a new, separate stream of development. And if it is named, it is called a branch.
```
// 创建新branch并移动
git checkout -b <branch_name>
// 只创建不移动
git branch <branch_name> <commit_id>
```

# 技巧

## 还未git add之前恢复到原本的样子
```
// 恢复修改的文件
git checkout .
// 删除新添加的文件
git clean -df
```

## 把https上传改成git协议（ssh密钥）上传
```
git remote -v
git remote set-url origin git@github.com:someaccount/someproject.git
```
