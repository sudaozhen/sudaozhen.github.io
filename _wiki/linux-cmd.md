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

man是manual的缩写

man帮助用法演示:

```shell
man ls
```

man也是一条命令，分为9章，可使用man命令获得man的帮助

查看man命令的第7章:

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

### mkdir

### rm

### rmdir

### mv

### cp

### ln

## 目录操作

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
