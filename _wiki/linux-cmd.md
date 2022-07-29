---
layout: wiki
title: Linux 常用命令
cate1: Linux
cate2: Command
categories: Linux
description: Linux 常用命令。
keywords: Linux, command
---

# 帮助

### man:fire:

man 是 manual 的缩写

man 帮助用法演示:

```shell
man ls
```

man 也是一条命令，分为 9 章，可使用 man 命令获得 man 的帮助

查看 man 命令的第 7 章:

```shell
man 7 man 
```

命令帮助:

```shell
man 1 passwd 
```

配置文件帮助（/etc/passwd）:

```shell
man 5 passwd
```

查看全部帮助（不知道是命令还是配置文件，适用于相似查找）

```shell
man -a passwd
```

### help

shell（命令解释器）自带的命令称为内部命令，其他的是外部命令

如何区分内外部命令？

type 命令

```shell
type cd
```

内部命令使用help帮助:

```shell
help cd
```

外部命令使用 命令 --help 帮助:

```shell
ls --help
```

### whatis

命令简短介绍

```shell
whatis cp
```

### info

info帮助比help更详细，作为help的补充

```shell
info ls
```

### apropos

检索命令关键字

例如：不记得tcpdump命令的全名：

```shell
apropos tcp
#等价于
man -k tcp
```

# 文件和目录

## 删除和创建

### touch

创建空文件

```shell
touch file1.txt             #创建空文件
touch file2.txt file2.doc   #创建两个空文件
touch "program files"       #文件名含空格,但非常不建议文件或目录名中包含空格
```

### mkdir:fire:

创建文件夹

```shell
mkdir dir
mkdir dir1 dir2
mkdir -p dir   #递归创建，强烈建议脚本中使用此选项
```

### rm:fire:

删除文件或目录

| 选项 | 含义     |
| ---- | -------- |
| -r   | 删除目录 |
| -f   | 强制执行 |

```shell
rm -rf /root/test/      #强制删除/root/test/目录
rm file                 #删除文件file
```

### rmdir

删除空目录，非空目录使用 `rm -r` 删除

```shell
rmdir dir
```

### mv:fire:

移动 & 重命名 目录或文件

```shell
mv [源目录或文件] [目标目录或文件]
mv file1 file2    #将文件 file1 重命名为 file2
mv dir1 dir2      #将目录 dir1 重命名为 dir2（当前目录下不存在 dir2 目录）
mv file dir       #将文件 file 移动到 dir 目录内
mv dir dir1       #将目录 dir 移动到 dir1 目录内 （当前目录下存在 dir1 目录）
```

### cp:fire:

复制

| 选项     | 含义                               |
| -------- | ---------------------------------- |
| -r 或 -R | 递归复制目录及其子目录内的所有内容 |
| -p       | 保留权限、属主和修改时间           |
| -v       | 显示复制过程                       |
| -a       | 等同于-dpR                         |
| -d       | 复制符号连接，而不是指向的文件     |

```shell
cp file file.bak    #创建 file 的一个副本到当前目录下，名字为 file.bak
cp file dir         #将 file 复制一份到 dir 目录内
cp -r dir1 dir2     #目录 dir1 复制到 dir2 目录内
```

### ln

链接命令

```shell
ln -s [源文件或目录] [目标文件或目录] 创建软链接 
ln [源文件] [目标文件] 创建硬链接 
```

软连接：相当于【快捷方式】

硬链接：类似于复制，同步更新，i节点和源文件相同；通过i节点识别，不能跨分区，不能针对目录使用

## 目录操作

### ls

列出目录中的内容

| 选项        | 含义            |
| ----------- | --------------- |
| -h          | 人性化显示大小  |
| -a          | 显示隐藏文件    |
| -d          | 目录属性        |
| -i          | inode i节点信息 |
| -l（小写L） | 详细信息        |
| -1          | 一列显示        |
| -s          | 显示大小        |
| -r          | 逆序显示        |
| -t          | 按时间顺序显示  |
| -R          | 递归显示        |

```shell
ls -lh         #列出当前目录下的详细信息，并人性化显示大小
ls -a          #显示当前目录下的隐藏文件
```

### cd

切换目录

```shell
cd .         #切换到当前目录
cd ..        #切换到上级目录
cd ~         #切换到用户家目录
cd -         #切换到原来的目录
cd /root     #切换到 /root 目录下
```

### pwd

显示当前目录绝对路径

### tree

树状结构显示目录

``` shell
tree -L 1   #仅显示当前目录下的一级子目录
tree -d     #仅显示目录
```

### du

显示目录大小

```shell
du -sh /root         #显示当前目录大小
```

显示当前目录绝对路径

## 文件操作

## 查找

## 文件权限

## 压缩/解压缩

# 文本处理

## 查找文本内容

## 查看文本内容

## 文本处理

# 磁盘和文件系统

## 磁盘

## 文件系统

# 系统管理和资源监控

## 系统管理

## 资源监控

# 进程管理

## 进程查看

## 进程管理



# 用户和用户组管理

## 用户

## 用户组

## 用户信息

# 网络工具

## 网络路由

## 数据传输

## 网络诊断

# 软件包管理

# 其他命令
