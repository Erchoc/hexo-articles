---
title: Git在项目开发中的使用
date: 2017-05-09 16:08:31
tags: 高效工具
---

> Git不是github!Git不是github!Git不是github!重要的事情说三遍。Github和osc码云,gitlab,coding.net一样只是个放代码的远程仓库；怎么把这些代码放上去，怎么管理？这些平台都使用了Git这种超级流行的分布式管理技术。

> 我甚至建议开发者放弃传统的使用FTP上传代码到服务器的方式，项目代码反正你也要备份，放在托管平台多好，99%不会丢失数据，还方便迭代和版本回溯呢，又利于团队协作。FTP就让不懂代码的客户使用吧，也许他们要改改图片上传.av呢。阅读全文查看所有人都能学会的git简单使用方式。

<!-- more -->

- 开始一个项目有两种方式。第一种，到github创建项目仓库，本地clone下来。下面介绍第二种：

```
- 初始化本地仓库，生成.git配置文件夹 git init

- 查看当前暂存区代码状态 git status

- 将全部代码纳入本地仓库 git add -A

- 再次查看代码暂存区状态 git status

- 配置用户信息,用于区分代码维护者
    - git config --global user.name "Erchoc"
    - git config --global user.email "erchoc@qq.com"

- 查看git全部配置信息 git config -l

- 代码提交到本地仓库 git commit -m "初次提交,初始化项目"

- 修改过的代码直接丢进本地仓库 git commit -am “自动执行了add操作”

- 添加远程仓库地址
  git remote add origin https://github.com/Erchoc/laraos.git

- 添加多个远程仓库要加`set-url --add`参数
  git remote set-url --add origin https://git.oschina.net/erchoc/laraos.git

- 代码推送到远程dev分支 git push origin dev
```

- 码云图说Git基本使用：

![图片来自简书](http://upload-images.jianshu.io/upload_images/3995745-31b3b1de595b412f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

- 由于小叮共享书项目而接触到分支管理概念，以下为更新内容。

```
git clone到master分支到本地后，我们可以使用git branch查看本地分支。

创建并切换到本地的开发分支：git checkout -b develop master。

部分开发完毕，切换回master分支：git checkout master。

合并develop分支：git merge --no-ff develop，使用这个参数正常合并，否则默认使用快进世合并。

删除develop分支git branch -d develop
```
