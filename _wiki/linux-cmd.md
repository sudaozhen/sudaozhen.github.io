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

### ls:fire:

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

### cd:fire:

切换目录

```shell
cd .         #切换到当前目录
cd ..        #切换到上级目录
cd ~         #切换到用户家目录
cd -         #切换到原来的目录
cd /root     #切换到 /root 目录下
```

### pwd:fire:

显示当前目录绝对路径

### tree

树状结构显示目录

``` shell
tree -L 1   #仅显示当前目录下的一级子目录
tree -d     #仅显示目录
```

### du:fire:

显示目录大小

```shell
du -sh /root         #显示当前目录大小
```

## 文件操作

### stat

显示文件的 inode 内容

```shell
stat file1
```

### rename

重命名

rename 源字符串 目标字符串 文件

```shell
# 将 name1.txt 重名名为 name.txt
rename name1.txt name.txt name1.txt
```

支持的通配符

| 通配符 | 含义                           |
| ------ | ------------------------------ |
| ?      | 可替代单个字符                 |
| *      | 可替代多个字符                 |
| [char] | 可替代char集合中的任意单个字符 |

假设当前文件夹中有name1，name2 ..., name9, name10, ..., name299

```shell
rename name name0 name?     
# 将 name1 到 name9 重命名为 name01 到 name09，即将匹配到的字串（name加任意1个字符）中的name替换为name0

rename name name0 name??    
# 将 name01 到 name99 重命名为 name001 到 name099，即将匹配到的字串（name加任意2个字符）中的name替换为name0

rename name name0 name*     
# 将 name001 到 name299 重命名为 name0001 到 name0299，即将匹配到的字串（以name开头）中的name替换为name0

rename name0 name name0[12]*   
# 将 name0100 到 name0299 重命名为 name100 到 name299，即将匹配到的字串（以name0，后一个字符为1或2开头）中的name0替换为name
```

正则表达式（Perl 版）（查看方法：rename -V ；util-linux 为非 Perl 版）

```shell
prename "s/AA/aa/" *
# 把文件名中的AA替换成aa

prename "s/.html/.php/" *
# 把 .html 后缀的改成 .php 后缀

prename "s/$/.txt/" *
# 把所有的文件名都改成以 .txt 结尾

prename "s/.txt//" *
# 把所有以 .txt 结尾的文件名的 .txt 去掉
```

### basename

获取文件名

```shell
basename /root/test.txt      # 提取文件名
test.txt

basename -s .txt /root/test.txt  #提取文件名并去掉后缀
test
```

### dirname

获取路径名

```shell
dirname /root/test.txt
/root
```

### file:fire:

查看文件类型

```shell
file aaa.txt
```

### md5sum:fire:

计算文件 md5 值

```shell 
md5sum file     # 计算 md5 校验值

echo "8fddaad2cac641f6abd3f79cd6ad6da5 file" | md5sum -c       # 校验 md5 值
```

### sha256sum

计算文件 sha256 值

```shell
sha256sum file     # 计算 sha256 校验值

echo "d0cada789ec90f5a65f2bcdbacb369ddb114a0e3f18648f4be27f3c987d94606 file" | sha256sum -c         # 校验 sha256 值
```

## 查找

### find:fire:

文件搜索

find [搜索路径] [匹配条件]

| 参数    | 含义                                                         |
| ------- | ------------------------------------------------------------ |
| -cmin   | 文件属性改变，单位分钟                                       |
| -amin   | 访问时间改变，单位分钟                                       |
| -mmin   | 文件内容变化时间，单位分钟                                   |
| -ctime  | 文件属性改变，单位天                                         |
| -atime  | 访问时间改变，单位天                                         |
| -mtime  | 文件内容变化时间，单位天                                     |
| -type   | 基于文件类型；f 文件，d 目录，l 软连接；                     |
| -inum   | 根据i节点查找                                                |
| -iname  | 文件名忽略大小写                                             |
| -size   | 根据大小查找，默认单位为1个数据块（0.5KB）；支持k（KiB），M（MiB），G（GiB） |
| -user   | 查找所属用户                                                 |
| -regex  | 正则表达式                                                   |
| -iregex | 忽略大小写的正则表达式                                       |
| -perm   | 查找权限                                                     |
| -a      | 两个条件同数满足                                             |
| -o      | 满足一个即可                                                 |
| -exec   | 找到文件后执行后续操作                                       |
| -ok     | 找到文件后执行后续操作，但需确认                             |

```shell
find /etc -name init       #查找文件名为init
find /etc -name *init*     #查找文件包含init
find /etc -type d -name rc*   #查找/etc下 rc开头的文件夹
find /etc -iname init      #查找文件init（忽略大小写）
find /etc -size +204800    #查找大于100MB的文件，默认单位为数据块，1数据块=0.5KB
find /etc -size +10M       #查找大于10MB的文件
find /etc -user abc        #查找属于abc用户的文件
find /etc -cmin -5         #查找5分钟内修改过属性的文件，+5表示超过5分钟
find / -perm -0777         #查找权限为777的文件
find /etc -name inittab -exec ls -l {} \;   #将找到的文件执行 ls -l 操作
find -inum 2629483 -exec rm {} \;    #根据i节点来删除文件，适用于特殊文件名
find / -perm -4000 -o -perm -2000    #查找系统中具有UID权限的文件
```

### which

查找命令路径，是否有别名

```shell
which rm
```

### whereis

查找命令路径，及帮助文档

```shell
whereis ls
```

### locate

基于索引的搜索，速度比 find 快，但实时性不如 find

locate [文件名]

| 选项 | 含义       |
| ---- | ---------- |
| -i   | 忽略大小写 |

```shell
locate file  # 全盘搜索 file
updatedb     # 更新索引
```

/tmp 不在索引范围内

## 文件权限

### chown:fire:

| 用法                             | 含义                             |
| -------------------------------- | -------------------------------- |
| chown [用户] [文件或目录]        | 改变所有者，只有root可以改所有人 |
| chown [:组名] [文件或目录]       | 改变所属组                       |
| chown [用户名:组名] [文件或目录] | 同时改变所属组和所有者           |

 ```shell
 chown test file1        # 将 file1 的所属者改为 test
 chown :test file1       # 将 file1 的所属组改为 test
 chown test:test file1   # 将 file1 的所属者改为 test，所属组改为 test
 ```

### chgrp

改变所属组

```shell
chgrp test file1        # 将 file1 的所属组改为 test
```

### chmod:fire:

修改文件或目录权限

chmod [{ugoa}{+-=}{rwx}] [文件或目录]

| 选项 | 含义                                                  |
| ---- | ----------------------------------------------------- |
| u    | 所有者                                                |
| g    | 所属组                                                |
| o    | 其他人                                                |
| a    | 所有                                                  |
| +    | 增加                                                  |
| -    | 移除                                                  |
| =    | 指定                                                  |
| r    | 读（4），可以查看文件内容，列出目录中的内容           |
| w    | 写（2），可以修改文件内容，可以在目录中创建、删除文件 |
| x    | 执行（1），可以执行文件，可以进入目录                 |
| -R   | 递归修改                                              |

```shell
chmod g+w,o-r filename    # 将 filename 所属组增加写权限，其他人去掉读权限
chmod u+x filename        # 将 filename 所有者增加执行权限
chmod 644 filename        # 将 filename 权限指定为：所有者可读写，所属组和其他人为只读，但所有人都不可执行

chmod u+s filename        # 将 filename 增加 SUID 权限，即执行该文件权限变为root
chmod u-s filename        # 将 filename 去掉 SUID 权限

chmod g+s filename        # 将 filename 增加 SGID 权限，即执行该文件时权限变为该文件的所属组
chmod g+s dirname         # 将 dirname 增加 SGID 权限，即其他用户在此目录创建的文件属组为该目录的属组
chmod g-s filename        # 将 filename 去掉 SGID 权限

chmod o+t dirname         # 将 dirname 增加 SBIT 粘着位权限，即用户对该目录下的所有文件都有写权限，但只能删除此目录下自己创建的文件，而无法删除其他用户创建的文件。
chmod o-t dirname         # 将 dirname 去掉 SBIT 粘着位权限
```

### chattr 

设置文件系统属性

chattr [+-=] [选项] 文件或目录名

| 选项      | 含义                                             |
| --------- | ------------------------------------------------ |
| +         | 增加权限                                         |
| -         | 删除权限                                         |
| =         | 等于某权限                                       |
| i（文件） | 不允许对文件进行删除、改名，也不能添加和修改数据 |
| i（目录） | 只能修改目录下文件的数据，但不允许建立和删除文件 |
| a（文件） | 只能在文件中增加数据，但是不能删除也不能修改数据 |
| a（目录） | 只允许在目录中建立和修改文件，但是不允许删除     |

```shell
chattr +i filename     # 对 filename 增加i权限
```

### lsattr

查看文件系统属性

lsattr 选项 文件名

| 选项 | 含义                                               |
| ---- | -------------------------------------------------- |
| -a   | 显示所有文件和目录，含隐藏文件                     |
| -d   | 若目标是目录，仅列出目录本身的属性，而不是子文件的 |

```shell
lsattr filename     # 显示 filename 的文件系统属性
```

### setfacl

设置文件 ACL 权限

setfacl [选项] [文件或目录名]

| 选项 | 含义              |
| ---- | ----------------- |
| -m   | 设定ACL权限       |
| -x   | 删除指定的ACL权限 |
| -b   | 删除所有的ACL权限 |
| -d   | 设定默认ACL权限   |
| -k   | 删除默认ACL权限   |
| -R   | 递归设定ACL权限   |

设定用户 ACL 权限

setfacl -m u:用户名:权限 文件名或目录名

```shell
setfacl -m u:test:rx dir/      # 设置 test 用户只可查看 dir 目录内的文件，但不可删除、创建或修改目录内的文件
```

设定用户组 ACL 权限

setfacl -m g:组名:权限 文件名或目录名

```shell
setfacl -m g:test:rwx dir     # 设置 test 组对 dir 目录拥有全部权限
```

其他用法

```shell
setfacl -m m:rx 文件名或目录名      # 设置指定文件的最大有效权限
setfacl -x u:用户名 文件名或目录名   # 删除指定用户对指定文件或目录的全部 ACL 权限
setfacl -x g:组名 文件名或目录名     # 删除指定用户组对指定文件或目录的全部 ACL 权限
setfacl -b 文件名或目录名            # 删除指定文件或目录的所有 ACL 权限
setfacl -m u:用户名:权限 -R 目录名   # 设定指定目录下的所有文件的 ACL 权限
setfacl -m d:u:用户名:权限 目录名    # 设定指定目录的默认 ACL 权限，即该目录下后建的文件都遵循此权限，再此之前设置的权限不受影响
```

### getfacl

查看文件 ACL 权限

```shell
getfacl filename    # 查看 filename 的 ACL 权限
```

## 压缩 / 解压缩

### gzip

gzip -d xxx.gz    解压gz压缩包，默认删除源文件

gunzip xxx.gz    解压gz压缩包

gzip [文件] *.gz   压缩文件，只能压缩文件

```shell
gzip -d file.gz        # 解压 file.gz ,并删除 file.gz
gzip file file.gz      # 将 file 压缩为 file.gz, 并删除源文件 file
```

### tar:fire:

| 选项 | 含义              |
| ---- | ----------------- |
| -f   | 指定压缩文件名    |
| -c   | 创建打包          |
| -z   | 压缩（*.tar.gz）  |
| -v   | 显示详细信息      |
| -j   | 压缩（*.tar.bz2） |
| -C   | 解压路径          |

```shell
tar -cvf file.tar file    # 将 file 打包成 file.tar
tar -cvf dir.tar dir/     # 将 文件夹 dir 打包成 dir.tar
gzip file.tar file.tar.gz # 将 file.tar 压缩成 file.tar.gz
tar -czvf dir.tar.gz dir    # 将以上两步合并，打包并压缩 dir 目录
tar -czvf file.tar.gz file1 file2 file3 # 将多个文件打包并压缩成 file.tar.gz
tar -xzvf file.tar.gz     # 将 file.tar.gz 解压缩并解包
tar -xzvf file.tar.gz -C /root  # 将 file.tar.gz 解压缩并解包到 /root 目录下

tar -cjvf dir.tar.bz2 dir/  # 将 dir 打包压缩成 file.tar.bz2
tar -xjvf dir.tar.bz2       # 将 dir.tar.bz2 加压缩并解包

tar -xvf file.tar.xz        # 将 file.tar.xz 解压缩并解包
xz file.tar                 # 将 file.tar 包 压缩为 file.tar.xz，并删除 file.tar
```



### zip / unzip:fire:

zip -r *.zip [文件或目录]     压缩文件或目录为zip

unzip *.zip                解压zip文件

```shell
zip -r file.zip file    # 将 file 压缩成 file.zip
unzip file.zip          # 将 file.zip 解压缩 
```

### bzip2 / bunzip2

```shell
bzip2 file          # 将 file 压缩为 file.bz2, 并删除 file
bzip2 -k file       # 将 file 压缩为 file.bz2, 不删除 file
bunzip2 file.bz2    # 将 file.bz2 解压缩
```

# 文本处理

## 查找文本内容

### grep:fire:

查找文件内字符串

grep 选项 文件名

| 选项 | 含义                           |
| ---- | ------------------------------ |
| -i   | 忽略大小写                     |
| -v   | 排除字符串                     |
| -E   | 正则表达式                     |
| -n   | 显示源文件行数                 |
| -w   | 显示全匹配                     |
| -c   | 显示匹配的列数                 |
| -A   | 显示匹配行之后的内容行数       |
| -B   | 显示匹配行之前的内容行数       |
| -C   | 显示匹配行之前和之后的内容行数 |

```shell
grep 111 file         # 匹配 file 中包含 111 的行
grep -i ac file       # 匹配 file 中包含 ac、AC、Ac、aC 的行，忽略大小写
grep -v aa file       # 匹配 file 中不包含 aa 的行
grep -E "aa|bb" file  # 匹配 file 中包含 aa 或 bb 的行
grep -A 2 aa file     # 匹配 file 中包含 aa 的行及其后2行（不含aa所在行）
```

## 查看文本内容

### cat:fire:

### more

### less:fire:

### head

### tail:fire:

### tac

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
