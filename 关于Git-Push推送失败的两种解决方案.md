---
title: 关于Git Push推送失败的两种解决方案
date: 2017-05-21 06:50:44
tags: 高效工具
---

> Git的理念和使用都需要长期的经验和无尽的坑来填，否则你无法体会到它的强大！最近远程创建了含有Readme的仓库(以后在github上创建仓库时候我再也不添加README了), 本地初始化并添加了远程仓库后, push却失败了, 出现提示：

<!-- more -->

$ git push origin dev
```
To https://git.oschina.net/erchoc/laradock.git

 ! [rejected]        dev -> dev (fetch first)

error: failed to push some refs to 'https://git.oschina.net/erchoc/laradock.git'

hint: Updates were rejected because the remote contains work that you do

hint: not have locally. This is usually caused by another repository pushing

hint: to the same ref. You may want to first integrate the remote changes

hint: (e.g., 'git pull ...') before pushing again.

hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

- 问题(Non-fast-forward)出现的原因是: git仓库中已有一部分代码, 它不允许你直接把你的代码覆盖上去。于是你有2个选择方式:

```
1. 强推，即利用强覆盖方式用你本地的代码替代git仓库内的内容:

git push -f

2. 先把git的东西fetch到你本地然后merge后再push

    - git fetch
    - git merge

这2句命令等价于

git pull

有时候remote有多个版本分支库，git pull需要指定开发版本的分支：

git pull origin master
```

- 可是, 有时候还会出现问题:

```
上面出现的 [branch "master"]是需要明确(.git/config)如下的内容

[branch "master"]

    remote = origin

    merge = refs/heads/master
```

- 这等于在告诉git2件事:

```
1，当你处于master branch, 默认的remote就是origin。

2，当你在master branch上使用git pull时，却没有指定remote和branch。

那么git就会采用默认的remote（也就是origin）来merge在master branch上所有的改变。
```

- 如果不想或者不会编辑config文件的话，可以在bush上输入如下命令行：

```
$ git config branch.master.remote origin

$ git config branch.master.merge refs/heads/master
```

- 之后再重新git pull下。最后git push你的代码吧。

```