---
title: "Github协作的建议"
date: 2021-03-25T14:47:17+08:00
draft: false
---

# 功能驱动

需求是开发的起点，先有需求再有功能分支或者补丁分支。完成开发后，该分支就合并到主分支，然后被删除。

# 持续集成

频繁地（一天多次）将代码集成到主分支。

# 分支管理

合理且优雅的分支管理策略可以使得版本库的演进保持简洁，主干清晰，各个分支各司其职、井井有条。

## 主分支Master

首代码库应该有一个、且仅有一个主分支。所有提供给用户使用的正式版本，都在这个主分支上发布。Github主分支的名字，默认叫做Master。它是自动建立的，版本库初始化以后，默认就是在主分支在进行开发。

## 开发分支Develop

主分支只用来分布重大版本，日常开发应该在另一条分支上完成。我们把开发用的分支，叫做Develop。如果想正式对外发布，就在Master分支上，对Develop分支进行"合并"（merge）。

Git创建Develop分支的命令：

```bash
git checkout -b develop master
```

将Develop分支发布到Master分支的命令：

```bash
# 切换到Master分支
git checkout master
# 对Develop分支进行合并
git merge --no-ff develop
```

这里稍微解释一下，上一条命令的--no-ff参数是什么意思。默认情况下，Git执行"快进式合并"（fast-farward merge），会直接将Master分支指向Develop分支。使用--no-ff参数后，会执行正常合并，在Master分支上生成一个新节点。为了保证版本演进的清晰，我们希望采用这种做法。

## 临时性分支

前面讲到版本库的两条主要分支：Master和Develop。前者用于正式发布，后者用于日常开发。其实，常设分支只需要这两条就够了，不需要其他了。但是，除了常设分支以外，还有一些临时性分支，用于应对一些特定目的的版本开发。临时性分支主要有三种：

- 功能（feature）分支
- 预发布（release）分支
- 修补bug（fixbug）分支

这三种分支都属于临时性需要，使用完以后，应该删除，使得代码库的常设分支始终只有Master和Develop。

## 功能分支

接下来，一个个来看这三种"临时性分支"。

第一种是功能分支，它是为了开发某种特定功能，从Develop分支上面分出来的。开发完成后，要再并入Develop。功能分支的名字，可以采用feature-*的形式命名。

创建一个功能分支：

```bash
git checkout -b feature-x develop
```

开发完成后，将功能分支合并到develop分支：

```bash
git checkout develop

git merge --no-ff feature-x
```

删除feature分支：

```bash
git branch -d feature-x
```

## 预发布分支

第二种是预发布分支，它是指发布正式版本之前（即合并到Master分支之前），我们可能需要有一个预发布的版本进行测试。

预发布分支是从Develop分支上面分出来的，预发布结束以后，必须合并进Develop和Master分支。它的命名，可以采用release-*的形式。

创建一个预发布分支：

```bash
git checkout -b release-1.2 develop
```

确认没有问题后，合并到master分支：

```bash
git checkout master
git merge --no-ff release-1.2
# 对合并生成的新节点，做一个标签
git tag -a 1.2
```

再合并到develop分支：

```bash
git checkout develop
git merge --no-ff release-1.2
```

最后，删除预发布分支：

```bash
git branch -d release-1.2
```

## 修补bug分支

最后一种是修补bug分支。软件正式发布以后，难免会出现bug。这时就需要创建一个分支，进行bug修补。

修补bug分支是从Master分支上面分出来的。修补结束以后，再合并进Master和Develop分支。它的命名，可以采用fixbug-*的形式。

创建一个修补bug分支：

```bash
git checkout -b fixbug-0.1 master
```

修补结束后，合并到master分支：

```bash
git checkout master
git merge --no-ff fixbug-0.1
git tag -a 0.1.1
```

再合并到develop分支：

```bash
git checkout develop
git merge --no-ff fixbug-0.1
```

再合并到develop分支：

```bash
git branch -d fixbug-0.1
```

# 使用流程

合理且优雅的Git使用流程，是非常重要的，否则，每个人都提交一堆杂乱无章的commit，项目很快就会变得难以协调和维护。

## 第一步：新建分支

首先，每次开发新功能，都应该新建一个单独的分支

```bash
# 获取主干最新代码
git checkout master
git pull
# 新建一个开发分支myfeature
git checkout -b myfeature
```

## 第二步：提交分支commit

分支修改后，就可以提交commit了。

```bash
git add --all
git status
git commit --verbose
```

## 第三步：撰写提交信息

提交commit时，必须给出完整扼要的提交信息，下面是一个范本。

```
Present-tense summary under 50 characters

* More information about commit (under 72 characters).
* More information about commit (under 72 characters).

http://project.management-system.com/ticket/123
```

第一行是不超过50个字的提要，然后空一行，罗列出改动原因、主要变动、以及需要注意的问题。最后，提供对应的网址（比如Bug ticket）。

## 第四步：与主干同步

分支的开发过程中，要经常与主干保持同步。

```bash
git fetch origin
git rebase origin/master
```

## 第五步：合并commit

分支开发完成后，很可能有一堆commit，但是合并到主干的时候，往往希望只有一个（或最多两三个）commit，这样不仅清晰，也容易管理。

那么，怎样才能将多个commit合并呢？这就要用到 git rebase 命令。

```bash
git rebase -i origin/master
```

git rebase命令的i参数表示互动（interactive），这时git会打开一个互动界面，进行下一步操作。

推送到远程仓库

## 第六步：发出Pull Request

合并commit后，就可以推送当前分支到远程仓库了。

```bash
git push --force origin myfeature
```

git push命令要加上force参数，因为rebase以后，分支历史改变了，跟远程分支不一定兼容，有可能要强行推送。

## 第七步：发出Pull Request

提交到远程仓库以后，就可以发出 Pull Request 到master分支，然后请求别人进行代码review，确认可以合并到master。

# 参考

[1] "Git 工作流程 - 阮一峰的网络日志". [Ruanyifeng.Com](http://ruanyifeng.com/), 2020, [http://www.ruanyifeng.com/blog/2015/12/git-workflow.html](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html). Accessed 9 Dec 2020. 

[2] "持续集成是什么？ - 阮一峰的网络日志". [Ruanyifeng.Com](http://ruanyifeng.com/), 2020, [https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html](https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html). Accessed 9 Dec 2020.

[3] "Git分支管理策略 - 阮一峰的网络日志". [Ruanyifeng.Com](http://ruanyifeng.com/), 2020, [http://www.ruanyifeng.com/blog/2012/07/git.html](http://www.ruanyifeng.com/blog/2012/07/git.html). Accessed 9 Dec 2020.

[4] "Git 使用规范流程 - 阮一峰的网络日志". [Ruanyifeng.Com](http://ruanyifeng.com/), 2020, [http://www.ruanyifeng.com/blog/2015/08/git-use-process.html](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html). Accessed 9 Dec 2020.