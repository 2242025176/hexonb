---
title: git基本命令
date: 2021-10-09
categories: git
tags: git  #标签
---


# git 基本命令

## 拷贝远程仓库代码

```git
git clone 链接
```

## 拉取最新代码

```
git pull
```

## 当当前项目有更改，需要进行提交

1.暂存更改 （添加目录下所有发生改变的文件）

```
git add .
```

2.添加注释信息

```
git commit -m '注释信息'
```

3.进行提交

```
git push
```

## 分支部分

1.将本地分支`wuhaidong`分支与主分支 `master`分支进行`合并`

```
先暂存所有更改-----在提交  最后在执行git命令

git checkout master  ---》进入到master分支

git merge wuhaidong   ---将wuhaidong分支和master分支进行合并

git push    --- 提交到远程仓库

git checkout wuhaidong  ----切换到本地分支
```

2.主分支`master`拉取`合并`到本地分支：

```
git checkout master    -- 进入master 分支

git pull   --拉取

git checkout wuhaidong   --切换回本地分支

git merge master    --- 合并
```

