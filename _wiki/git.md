---
layout: wiki
title: Git
cate1: Tools
cate2: Version Control
categories: Git
description: Git 常用操作记录。
keywords: Git, 版本控制
---

## git 安装

[https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git](https://git-scm.com/book/zh/v2/起步-安装-Git)

## 常用命令

| 功能                                                | 命令                                                       | 示例 |
| --------------------------------------------------- | ---------------------------------------------------------- | ---- |
| 配置用户名（当前用户所有仓库）                      | git config --global user.name 'your_name'                  |      |
| 配置邮箱（当前用户所有仓库）                        | git config --global user.email 'your_email@domain.com'     |      |
| 创建仓库                                            | git init                                                   |      |
| 查看状态                                            | git status                                                 |      |
| 添加文件到暂存区                                    | git add file1 [file2 ... ]                                 |      |
| 添加被监控文件到暂存区                              | git add -u                                                 |      |
| 提交到本地仓库                                      | git commit -m "msg"                                        |      |
| 查看日志                                            | git log                                                    |      |
| 单行显示                                            | git log --oneline                                          |      |
| 单行显示最近4次提交                                 | git log -n4 --oneline                                      |      |
| 图形显示所有提交                                    | git log --all --graph                                      |      |
| 图形单行显示所有                                    | git log --all --graph --oneline                            |      |
| 查看历史日志                                        | git reflog                                                 |      |
| 重命名                                              | git mv old_name new_name                                   |      |
| 图形界面显示                                        | gitk --all                                                 |      |
| 创建基于某个commit或分支的新分支并切换到新分支      | git checkout -b 新分支名 commit号或现有分支名              |      |
| 创建基于旧分支的新分支                              | git branch -m 旧分支名 新分支名                            |      |
| 比较工作区和暂存区所有文件的差异                    | git diff                                                   |      |
| 比较工作区和暂存区的指定文件（file1 [file2]）的差异 | git diff -- file1 [file2]                                  |      |
| 比较当前提交和上次提交的不同，^等同于~1             | git diff HEAD HEAD^                                        |      |
| 比较当前提交和上上次提交的不同，^^等同于~2          | git diff HEAD HEAD^^                                       |      |
| 比较指定两个提交的不同                              | git diff 415c5c8 3d4731d                                   |      |
| 比较暂存区和HEAD的文件差异                          | git diff --cached                                          |      |
| 比较两个分支的差异                                  | git diff 分支1(或commit_ID) 分支2(或commit_ID)             |      |
| 较两个分支指定文件的差异                            | git diff 分支1(或commit_ID) 分支2(或commit_ID) -- filename |      |
| 显示所有分支（包含远程）                            | git branch -av                                             |      |
| 删除分支                                            | git branch -d 分支名                                       |      |
| 强制删除分支                                        | git branch -D 分支名                                       |      |
| 修改最近一次commit信息                              | git commit --amend                                         |      |
| 交互式变基                                          | git rebase -i                                              |      |
| 暂存区所有文件恢复成HEAD                            | git reset HEAD                                             |      |
| 暂存区部分文件恢复成HEAD                            | git reset HEAD -- filename filename2 …                     |      |
| 工作区和暂存区都恢复成指定commit_ID **（危险）**    | git reset --hard commit_ID                                 |      |
| 工作区恢复成暂存区                                  | git checkout -- filename                                   |      |
| 删除文件                                            | git rm filename                                            |      |
|                                                     |                                                            |      |

### 修改老旧commit信息

git rebase -i 要修改的前一个commit_ID 

rebase ---- 交互式变基（仅限本地仓库）

- ​		pick ：不更改
- ​		reword ：修改信息

操作步骤：

1. git rebase -i 要修改的前一个commit_ID
2. 将需要修改 message 的 commit 前的 pick 改为 reword 并保存；
3. 在接下来的文件中修改 message 信息并保存。

### 把连续的多个commit整理成1个

git rebase -i 前一个commitID    (即8f30d42的前一个commitID)

squash：合并到下一个commit  （即合并到9c6861f）

![](\images\wiki\git\image1.png)

操作步骤：

1. git rebase -i feab180
2. 修改8f30d42、27d2f81、415c5c8这几个commit前的pick为squash（简写s），即将8f30d42、27d2f81、415c5c8、9c6861f这四个commit合并为一个，保存退出
3. 增加commit信息，保存退出

### 把间隔的几个commit整理成1个

1. git rebase -i 前一个commitID
2. 添加需要合进的commit并在其前面写pick
3. 调整顺序，将需要合并测commit放到合进的commit下方
4. 将需要合入的commit的pick改为squash（简写s），保存退出
5. 增加commit信息，保存退出

![](\images\wiki\git\image2.png)

### 加塞任务

情景描述：工作区已做修改，但不具备提交的状态，此时临时要求解决bug（更改其他分支）。

git stash    把工作区保存到堆栈

git stash apply    恢复之前状态，不清空堆栈

git stash list   显示堆栈列表

git stash pop  恢复之前的状态，清空堆栈

操作步骤：

1. git stash   把工作区保存到堆栈
2. 切换到其他分支，或创建 bug fix 分支
3. 解决bug，并提交
4. git stash pop   恢复之前的状态，清空堆栈

### 指定不需要git管理的文件

常用忽略语法 https://github.com/github/gitignore

文件名只能是 .gitignore

此文件放在git仓库根目录

### git仓库备份

| 常用协议                     | 语法格式                                                     | 说明                     |
| ---------------------------- | ------------------------------------------------------------ | ------------------------ |
| 本地协议(1)                  | /path/to/repo.git                                            | 哑协议                   |
| 本地协议(2)                  | [file:///path/to/repo.git](file://path/to/repo.git)          | 智能协议                 |
| http/https协议  （用户密码） | http://git-server.com:port/path/to/repo.git  https://git-server.com:port/path/to/repo.git | 平时接触到的都是智能协议 |
| ssh协议  （公私钥）          | user@git-server.com:path/to/repo.git                         | 工作中最常用的智能协议   |

 

哑协议与智能协议的区别

直观区别：哑协议传输进度不可见；智能协议传输可见。

传输速度：智能协议比哑协议传输速度快。

 

备份特点：

![](\images\wiki\git\image3.png)

采用克隆的方式备份git仓库

- 新建备份文件夹；

- 并切换到该文件夹，原仓库为/path/gittest/

- git clone --bare /path/gittest/.git ya.git

- git clone --bare [file:///path/gittest/.git](file://path/gittest/.git) zhineng.git

- --bare 不含工作区的裸仓库

同步到远端

- git remote -v    显示远端仓库

- git remote add zhineng [file:///path/backup/gittest.git](file://path/backup/gittest.git) 添加远端仓库

- git push zhineng   本地推送到远端
