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
| -c   | 显示匹配的行数                 |
| -A   | 显示匹配行之后的内容行数       |
| -B   | 显示匹配行之前的内容行数       |
| -C   | 显示匹配行之前和之后的内容行数 |
| -q   | 不显示任何信息                 |
| -a   | 不要忽略二进制数据             |
| -o   | 只显示匹配到的字符             |

```shell
grep 111 file         # 匹配 file 中包含 111 的行
grep -i ac file       # 匹配 file 中包含 ac、AC、Ac、aC 的行，忽略大小写
grep -v aa file       # 匹配 file 中不包含 aa 的行
grep -E "aa|bb" file  # 匹配 file 中包含 aa 或 bb 的行
grep -A 2 aa file     # 匹配 file 中包含 aa 的行及其后2行（不含aa所在行）
```

## 查看文本内容

### cat:fire:

显示文本

| 选项 | 含义     |
| ---- | -------- |
| -n   | 显示行号 |

```shell
cat filename
```

### more

分页显示文本

| 按键      | 含义     |
| --------- | -------- |
| 空格 或 f | 向下翻页 |
| 回车      | 换行     |
| q         | 退出     |

```shell
more filename
```

### less:fire:

显示文本

| 按键      | 含义                 |
| --------- | -------------------- |
| 空格 或 f | 向下翻页             |
| b         | 向上翻页             |
| k 或 ↑    | 向上一行             |
| j 或 ↓    | 向下一行             |
| /string   | 向下搜索 string 字符 |
| ?string   | 向上搜索 string 字符 |
| q         | 退出                 |

```shell
less filename
```

### head

查看文本开头

```shell
head -n 7 filename   # 查看 filename 的前7行
```

### tail:fire:

查看文件结尾

| 参数 | 含义                             |
| ---- | -------------------------------- |
| -n   | 查看文本后几行                   |
| -f   | 动态显示文本，适用于实时查看日志 |

```shell
tail -fn 6 filename   # 实时显示 filename 最后6行
```

### tac

倒叙显示文本

```shell
tac filename    # 倒叙显示filename
```

## 文本处理

### cut:fire:

字段提取

| 选项 | 含义                           |
| ---- | ------------------------------ |
| -f   | 提取列号                       |
| -d   | 指定分隔符，不指定默认为制表符 |
| -c   | 按字符提取                     |

准备以下文本 filename(456 和 abc 之间为制表符)：

```shell
123 = 456		abc
```

```shell
cut -f 2 filename    # 使用默认制表符作为分隔符，提取 filename 的第2列
结果：abc

cut -f 1 -d "=" filename   # 使用"="作为分隔符，提取 filename 的第1列
结果：123

cut -c 1-5 filename        # 提取 filename 的第1到5个字符
结果：123 =
```

### sed:fire:

对数据流进行 选取、替换、删除、新增

#### sed的基本工作方式是：

- 将文件以行为单位读到内存（模式空间）
- 使用sed的每个脚本对该行进行操作
- 处理完成后输出该行

#### sed语法

```shell
sed [选项] '[动作]' 文件名
```

| 选项 | 含义                                                         |
| ---- | ------------------------------------------------------------ |
| -n   | 一般会把所有数据都输出到屏幕，如果加入此选择，则只会把经过sed处理的行输出到屏幕 |
| -e   | 允许对输入数据应用多条sed命令编辑                            |
| -i   | 用sed的修改结果直接修改读取数据的文件，而不由屏幕输出        |
| -r   | 支持扩展正则表达式                                           |

| 动作           | 含义                                                         |
| -------------- | ------------------------------------------------------------ |
| a              | 追加，在当前行后添加一行或多行。添加多行时，除最后一行外，每行末尾需要用“\”代表数据未完结。 |
| c              | 行替换，用c后面的字符串替换原数据行，替换多行时，除最后一行外，每行末尾需用“\”代表数据未完结。 |
| i              | 插入，在当期行前插入一行或多行。插入多行时，除最后一行外，每行末尾需要用“\”代表数据未完结。 |
| d              | 删除，d指令后的语句不会被执行                                |
| p              | 打印，输出指定的行。与-n配合只输出匹配行                     |
| s              | 字串替换，用一个字符串替换另外一个字符串。格式为“行范围s/旧字串/新字串/g”(和vim中的替换格式类似)。 |
| g              | 全局替换，用于替换所有出现的次数                             |
| 's/old/new/2'  | 替换第2次匹配                                                |
| w path/to/file | 替换的行输出到文件，sed -n 's/old/new/w /tmp/a.txt'          |
| =              | 打印行号                                                     |
| r              | 读取文件                                                     |
| w              | 写文件                                                       |
| n              | 读下一行命令，一般只处理偶数行，跳过奇数行                   |
| q              | 退出，sed 10q filename #读取10行退出                         |

```shell
sed -i '/string/d' filename    # 删除string所在行
sed -i 's/string/d' filename   # 删除string字串
sed -i '/string/a\new_string_line' filename  # 在filename中查找string在其后插入new_string_line字符行
sed '/ab/a ccc' filename       # 在ab字串后增加ccc新行
sed '/ab/c ccc' filename       # 替换ab字串所在行为ccc
sed '/ab/r bfile' afile        # afile中查找到ab字串后在其后插入bfile文件中的内容

sed -i 's/:$//g' filename    # 去除“:”结尾的“:”
sed -i 's/\r//g' filename    # 去除\r回车符，用于CRLF转换成LF格式

# 多次替换
sed -e 's/old/new/' -e 's/old/new/' filename …
sed -e 's/old/new/;s/old/new/' filename …

sed 's/正则表达式/new/' filename
sed -r 's/扩展正则表达式/new/' filename

# 同时匹配两个正则需使用()
sed -r 's/(aa)|(bb)/!/' filename

# 分组回调功能，“\1”表示回调第1组
echo axyzb | sed -r 's/(a.*b)/\1:\1/'
# 输出：axyzb:axyzb

# "/"与匹配内容冲突可以使用其他符号，原/分隔符使用!或@
sed 's!/!new!' filename
```

#### 寻址

默认对每行进行操作，增加寻址后对匹配的行进行操作

```shell
/正则表达式/s/old/new/g
行号范围/s/old/new/g
```

行号可以是具体的行，也可以是最后一行$符号

可以使用两个寻址符号，也可以混合使用行号和正则地址

#### 分组

寻址可以匹配多条命令

```shell
/regular/{s/old/new/;s/old/new/ }
```

#### 脚本文件

可以将选项保存为文件，使用-f 加载脚本文件

```shell
sed -f sedscript filename
```

#### sed的多行模式

xml或json配置文件为多行出现

| 多行模式处理命令 | 含义                                     |
| ---------------- | ---------------------------------------- |
| N                | 将下一行加入到模式空间                   |
| D                | 删除模式空间中的第一个字符到第一个换行符 |
| P                | 打印模式空间中的第一个字符到第一个换行符 |

##### 两行合并为一行处理

```shell
sed "N;s/a/b/g" # 两行合并成一行读取处理
```

示例文件

```
hel
lo
```

```shell
sed 'N;s/hel\nlo/!!!/' filename    # 双行读取匹配，注意换行符"\n"
sed 'N;s/hel.lo/!!!/' filename     # 也可使用正则"."
```

示例文件

```
hell
o bash hel
lo bash
```

```shell
sed 'N;s/\n//;s/hello bash/hello sed\n/;P;D' filename
# 读取下一行（2行一处理），先将\n替换为空，hello bash替换为hello

# sed\n，循环处理
sed 'N;N;s/\n//;s/hello bash/hello sed\n/;P;D' filename
# 3行一处理
```

#### 保持空间

保持空间也是多行的一种操作方式

将内容暂存在保持空间，便于做多行处理

| 保持空间命令 | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| h            | 将模式空间内容覆盖到保持空间（默认保存空间内有换行符，首次使用h将换行符覆盖） |
| H            | 将模式空间内容追加到保持空间                                 |
| g            | 将保持空间内容覆盖到模式空间                                 |

##### 倒序输出

```shell
sed -n '1h;1!G;$!x;$p'    # 1!G不对第一行处理
sed -n '1!G;h;$p'
sed -n '1!G;h;$!d'
```

### awk:fire:

#### awk脚本的流程控制

- 输入数据前历程   BEGIN{}

- 主输入循环  {}

- 所有文件读取完成例程  END{}

#### 记录和字段

- 每行称作awk的记录
- 使用空格、制表符分隔开的单次称作字段
- 也可以自己指定分割的字段

#### 字段的引用

awk中使用$1 $2 … $n 表示每一个字段，$0为整行

```shell
awk '{ print $1,$2,$3}' filename
```

awk 可以使用 -F 选项改变字段分隔符

```shell
awk -F ',' '{ print $1,$2,$3}' filename
```

分隔符可以使用正则表达式

例：

```shell
awk -F "'" '/^menu/{ print x++,$2 }' /boot/grub2/grub.cfg
# 打印以 menu 开头的第二列
```

结果：

```shell
0 CentOS Linux (5.1.11) 7 (Core)
1 CentOS Linux (3.10.0-1160.el7.x86_64) 7 (Core)
2 CentOS Linux (0-rescue-2362688d55a948b0a2829c283eab17e9) 7 (Core)
```

#### awk的表达式

##### 赋值操作符

###### = 是最常用的赋值操作符

```shell
var1 = "name"
var2 = "hello" "world"
var3 = $1
```

###### 其他赋值操作符


| 操作符 | 含义                 |
| ------ | -------------------- |
| ++     | 变量自加1            |
| --     | 变量自减1            |
| +=     | 将加的结果赋给变量   |
| -=     | 将减的结果赋给变量   |
| *=     | 将乘的结果赋给变量   |
| /=     | 将除的结果赋给变量   |
| %=     | 将取余的结果赋给变量 |
| ^=     | 将取幂的结果赋给变量 |
| **=    | 将取幂的结果赋给变量 |

##### 算数操作符

| 操作符 | 含义 |
| ------ | ---- |
| +      | 加   |
| -      | 减   |
| *      | 乘   |
| /      | 除   |
| %      | 取余 |
| ^      | 幂   |

##### 系统变量

- FS 和 OFS 字段分隔符，FS表示输入文件以什么分隔符判断，OFS 表示输出的字段分隔符

```shell
head -5 /etc/passwd | awk 'BEGIN{FS=":";OFS=","}{print $1,$2}'
# 读入分隔符使用":"，输出分隔符使用","
```

- RS 记录分隔符，默认为换行符

```shell
head -5 /etc/passwd | awk 'BEGIN{RS=":"}{print $0}'
# 以“:”作为一条记录的分隔符
```

- NR 和 FNR 行数；处理多文件时，FNR跟随文件，NR则为总行数；

- NF 字段数量，最后一个字段内容可以用 $NF 取出

##### 关系操作符

| 操作符 | 含义             |
| ------ | ---------------- |
| <      | 小于             |
| >      | 大于             |
| <=     | 小于等于         |
| >=     | 大于等于         |
| ==     | 等于             |
| !=     | 不等于           |
| ~      | 匹配正则表达式   |
| !~     | 不匹配正则表达式 |

##### 布尔操作符

| 操作符 | 含义   |
| ------ | ------ |
| &&     | 逻辑与 |
| \|\|   | 逻辑或 |
| ！     | 逻辑非 |

#### awk条件判断语句

条件语句使用if开头，根据表达式的结果来判断执行哪条语句

```shell
if (表达式)
	awk语句1
[else
	awk语句2
]
```

如果有多个语句需要执行可以使用{}将多个语句扩起来

```shell
awk '{if($2>=80) {print $1; print $2} }' filename
```

#### awk循坏语句

##### while 循坏

```shell
while(表达式)
	awk 语句1
```

##### do 循环

```shell
do{
	awk 语句1
}while(表达式)
```

##### for 循环

```shell
for(初始值; 循环判断条件; 累加)
	awk 语句1
```

例：

```shell
awk '{sum=0; for(c=2;c<=NF;c++) sum+=$c; print sum/(NF-1)}' filename
# 计算第2列到最后一列的平均数
```

##### 影响控制的其他语句

- break
- continue

#### awk 数组

##### 数组的定义

数组：一组有某种关联的数据（变量），通过下标依次访问

```shell
数组名[下标]=值
```

下标可以使用数字也可以使用字符串

##### 数组的遍历

```shell
for(变量 in 数组名)
	使用 数组名[变量] 的方式依次对每个数组的元素进行操作
```

##### 删除数组

```shell
delete 数组[下标]
```

```shell
awk '{ sum=0; for(c=2;c<=NF;c++) sum+=$c; avg[$1]=sum/(NF-1)}END{ for(user in avg) sum2+=avg[user] ;print sum2/NR}' filename
```

```shell
awk -f script.awk filename  # awk使用脚本文件处理filename
```

##### 命令行参数数组

- ARGC  awk 参数数量
- ARGV  awk 参数数组

##### 数组综合应用处理脚本

处理数据文件<kpi.txt>:

```markdown
user1 70 72 74 76 74 72
user2 80 82 84 82 80 78
user3 60 61 62 63 64 65
user4 90 89 88 87 86 85
user5 45 60 63 62 61 50
```

awk脚本文件<result.awk>:

```shell
{
sum = 0
for(c = 2; c <= NF; c++)
    sum += $c
avg[$1] = sum / ( NF - 1 )

if( avg[$1] >= 80 )
    letter = "S"
else if( avg[$1] >= 70 )
    letter = "A"
else if( avg[$1] >= 60 )
    letter = "B"
else
    letter = "C"

letter_all[letter]++
print $1,avg[$1],letter

}
END{
for( user in avg )
    sum_all += avg[user]

avg_all = sum_all / NR
print "average all:" avg_all

for( user in avg )
    if( avg[user] > avg_all )
        above++
    else
        below++

print "above",above
print "below",below
print "S:",letter_all["S"]
print "A:",letter_all["A"]
print "B:",letter_all["B"]
print "C:",letter_all["C"]
}
```

执行：

```shell
awk -f result.awk kpi.txt
```

结果：

```shell
user1 73 A
user2 81 S
user3 62.5 B
user4 87.5 S
user5 56.8333 C
average all:72.1667
above 3
below 2
S: 2
A: 1
B: 1
C: 1
```

#### awk 函数

##### 算数函数

| 函数    | 含义                        |
| ------- | --------------------------- |
| sin()   | 正弦函数                    |
| cos()   | 余弦函数                    |
| int()   | 取整                        |
| rand()  | 基于种子的伪随机数 ,范围0~1 |
| srand() | 重新获取种子，两者配合使用  |

```shell
awk 'BEGIN{pi=3.14; print int(pi) }'  # 取整，结果：3

awk 'BEGIN{srand();print rand()}'     # 生成随机数
```

##### 字符函数

| 函数             | 含义                                        |
| ---------------- | ------------------------------------------- |
| gsub( r,s )      | 在整个 $0 中用 s 替代 r                     |
| gsub( r,s,t )    | 在整个 t 中用 s 替代 r                      |
| index( s,t )     | 返回 s 中 字符串t 的第一位置                |
| length( s )      | 返回 s 长度                                 |
| match( s,r )     | 测试 s 是否包含匹配r的字符串                |
| split( s,a,sep ) | 在 sep 上将 s 分成序列 a                    |
| sub( r,s,t )     | 用 t 中最左边最长的子串代替 s               |
| substr( s,p,n )  | 返回 字符串s 中从 p 开始长度为 n 的后缀部分 |

##### 自定义函数

```shell
function 函数名(参数){
	awk语句
	return awk变量
}
```

例：

```shell
awk 'function a(str){ return str str} BEGIN{ print a("b")}'
```

### wc:fire:

统计

```shell
wc filename     # 统计 filename 文件的行数、单词数、字节数
wc -l filename  # 统计 filename 文件的行数
```

### uniq

去除重复行

```shell
uniq filename   # 去除 filename 文件中重复的行
```

### diff 

比较两个文件的差异

```shell
diff -u 源文件名 修改后文件名       # 比较两个文件的不同，u选项（Unified），显示行号
diff -u 源文件名 修改后文件名 > filediff.patch   # 将不同存成patch补丁文件
```

### patch

打补丁

```shell
patch 源文件名 filediff.patch   # 应用补丁文件，将 源文件 变更为 修改后的文件
```

### split

拆分文件

split <参数> <要分割的文件> [输出文件名前缀]

| 参数 | 含义                                                         |
| ---- | ------------------------------------------------------------ |
| -b   | 指定每个分割文件的大小，单位有K、M、G、P等                   |
| -d   | 指定分割文件的后缀为数字                                     |
| -a   | 指定分割文件数字后缀的长度，如果是1，后缀为0,1,2…；如果是2，则为00,01,02…；默认是2 |
| -C   | 指定每行最大的字节数                                         |
| -l   | 指定每个文件最大的行数                                       |

```shell
split -b 100M -d -a 1 test.tar.gz test.tar.gz.    # 将 test.tar.gz 压缩包拆分成100MB大小的小包，输出命名为 test.tar.gz.1、test.tar.gz.2、test.tar.gz.3 ...
cat test.tar.gz.* | tar -zxv    # 将分卷压缩包解压
```

### paste

合并文件

```shell
paste file1 file2 file3    # 将file1、file2、file3 按列合并
paste -s file1 file2 file3    # 将file1、file2、file3 按行合并
```

### sort

排序

```shell
sort filename         # 将 filename 的内容正向排序
sort -r filename      # 将 filename 的内容反向排序
```

### join

文本按相同列名合并

测试文本：

file1:

```
aaa 123
bbb 456
```

file2:

```
aaa 88
bbb 99
```

```shell
join file1 file2   # 将file1 和 file2 按相同列名合并
```

结果：

```
aaa 123 88
bbb 456 99
```

### tr

转换或删除文件中的字符

```shell
cat file | tr a-z A-Z       # 将file中的字母全部转换成大写
```

# 磁盘和文件系统

## 磁盘

### df

文件系统查看命令

| 选项 | 含义                                                      |
| ---- | --------------------------------------------------------- |
| -a   | 显示所有的文件系统信息，包括特殊文件系统，如/proc. /sysfs |
| -h   | 使用习惯单位显示容量，如KB, MB或GB等                      |
| -T   | 显示文件系统类型                                          |
| -m   | 以MB为单位显示容量                                        |
| -k   | 以KB为单位显示容量，默认就是以KB为单位                    |

```shell
df -hT  # 显示当前系统分区使用情况及分区格式
```

### du

统计目录或文件大小

| 选项 | 含义                                                     |
| ---- | -------------------------------------------------------- |
| -a   | 显示每个子文件的磁盘占用量。默认只统计子目录的磁盘占用量 |
| -h   | 使用习惯单位显示磁盘占用量，如KB, MB或GB等               |
| -s   | 统计总占用量，而不列出子目录和子文件的占用量             |

```shell
du -sh /root  # 统计/root目录文件占用空间
```

### sync

清空缓存，将数据同步写入磁盘；一般卸载分区前使用。

### fdisk

分区（分区格式为MBR，2.1TB 以下的硬盘）

```shell
fdisk /dev/sdb   # 将/dev/sdb磁盘进行分区
```

| 命令 | 说明                                                       |
| ---- | ---------------------------------------------------------- |
| a    | 设置可引导标记                                             |
| b    | 编辑bsd磁盘标签                                            |
| c    | 设置DOS操作系统兼容标记                                    |
| d    | 删除一个分区                                               |
| l    | 显示已知的文件系统类型。82为Linux  sw叩分区，83为Linux分区 |
| m    | 显示帮助菜单                                               |
| n    | 新建分区                                                   |
| o    | 建立空白DOS分区表                                          |
| p    | 显示分区列表                                               |
| q    | 不保存退出                                                 |
| s    | 新建空白SUN磁盘标签                                        |
| t    | 改变一个分区的系统ID                                       |
| u    | 改变显示记录单位                                           |
| v    | 验证分区表                                                 |
| w    | 保存退出                                                   |
| x    | 附加功能(仅专家)                                           |

重新读取分区表信息

partprobe

```shell
fdisk -l   # 显示所有磁盘设备及分区
```

### parted

分区（分区格式为GPT）

```shell
parted -l   显示分区
parted /dev/sdb  把sdb进行分区
```

### mdadm

软RAID组建

| 选项         | 含义                 |
| ------------ | -------------------- |
| -n           | 设备数量             |
| -l           | raid级别             |
| -C           | 创建raid设备         |
| -S 或 --stop | 停止raid设备         |
| -D           | 显示raid设备详细信息 |
| --remove     | 删除RAID设备         |

```shell
mdadm -C /dev/md0 -a yes -l 1 -n 2 /dev/adb1 /dev/sdc1
# 将/dev/adb1 和 /dev/sdc1 创建为/dev/md0，级别为raid1

mdadm -D /dev/md0  # 查看/dev/md0 RAID设备详细信息
```

### lsblk

```shell
lsblk -f  # 显示UUID及分区结构
```

## 文件系统

### mount:fire:

挂载

| 选项 | 含义                                                         |
| ---- | ------------------------------------------------------------ |
| -l   | 查询系统中已挂载的设备并显示卷标名称                         |
| -a   | 依据配置文件 /etc/fstab 的内容，自动挂载                     |
| -t   | 文件系统类型，ext3、ext4、iso9660、vfat（FAT32）、fat（FAT16） |
| -L   | 卷标名                                                       |
| -o   | 特殊选项，见下表                                             |

| -o特殊选项    | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| atime/noatime | 更新访问时间/不更新访问时间。访问分区文件时，是否更新文件的访问时间，默认为更新 |
| async/sync    | 异步/同步，默认为异步                                        |
| auto/noauto   | 自动/手动，mount  -a命令执行时，是否会自动安装/etc/fstab文件内容挂载，默认为自动 |
| defaults      | 定义默认值，相当于rw，suid，dev，exec，auto，nouser，async这七个选项 ，<span style="color:red">可移动硬盘不推荐defaults，推荐使用"nodev，nofail"</span> |
| exec/noexec   | 执行/不执行，设定是否允许在文件系统中执行可执行文件，默认是exec允许 |
| remount       | 重新挂载已经挂载的文件系统，一般用于指定修改特殊权限         |
| rw/ro         | 读写/只读，文件系统挂载时，是否具有读写权限，默认是rw        |
| suid/nosuid   | 具有/不具有SUID权限，设定文件系统是否具有SUID和SGID的权限，默认是具有 |
| user/nouser   | 允许/不允许普通用户挂载，设定文件系统是否允许普通用户挂载，默认是不允许，只有roof可以挂载分区 |
| usrquota      | 写入代表文件系统支持用户磁盘配额，默认不支持                 |
| grpquota      | 写入代表文件系统支持组磁盘配额，默认不支持                   |
| dev/nodev     | 默认dev                                                      |
| nofail        | 如果设备故障也不影响引导启动，<span style="color:red">自动挂载推荐加上，若无此设备，系统启动不会卡住，推荐"defaults，nofail"</span> |

```shell
mount      # 查询系统中已挂载的设备
mount -l   # 查询系统中已挂载的设备并显示卷标名称
mount [-t 文件系统] [-L 卷标名] [-o 特殊选项] 设备文件名 挂载点

mount -o remount,noexec /home    # /home必须是单独的分区，重新挂载/home分区，并使用noexec权限

mount -t iso9660 /dev/cdrom /mnt/cdrom     # 挂载光盘
mount /dev/sr0 /mnt/cdrom        #挂载光盘

mount -o loop /root/rhel7.iso /media   # 挂载iso光盘文件
```

### umount:fire:

卸载

```shell
umount 设备文件名或挂载点
umount /mnt/cdrom    # 卸载，挂载点
umount /dev/sde1     # 卸载，设备名
```

### eject

弹出光驱

### dd

| 选项  | 含义                           |
| ----- | ------------------------------ |
| if    | 输入                           |
| of    | 输出                           |
| ibs   | 一次读入字节数                 |
| obs   | 一次输出字节数                 |
| bs    | 同时设置读入/输出的块大小      |
| cbs   | 一次转换字节数                 |
| skip  | 从输入文件开头跳过块数         |
| seek  | 从输出文件开头跳过块数后再复制 |
| count | 仅复制块数                     |

```shell
dd if=/dev/zero bs=4M count=10 of=/afile  
# 生成全0文件/afile，大小为40MB

dd if=/dev/zero bs=4M count=10 seek=20 of=/bfile  
# 生成全0文件/bfile，ls显示120MB，du显示40MB，“seek=20”代表跳过 4MBx20

dd if=/dev/sda of=mbr.bin bs=512 count=1  # 备份sda的mbr
dd if=/dev/sda of=/dev/sdb     # 将/dev/sda整盘备份到/dev/sdb
dd if=/dev/sda of=/root/image  # 将/dev/sda整盘备份到/root/image文件中
dd if=/root/image of=/dev/sda  # 将备份的/root/image文件恢复到/dev/sda中
dd if=/dev/sdb | gzip > /root/image.gz    # 将/dev/sdb的数据压缩并备份到/root/image.gz中
gzip -dc /root/image.gz | dd of=/dev/sdb  # 将/root/image.gz解压并还原到/dev/sdb中
dd if=/dev/urandom of=/dev/sda1  # 利用随机数填充/dev/sda1
dd if=/dev/mem of=/root/mem.bin bs=1024   # 复制内存中的数据到/root/mem.bin,大小为1kB
dd if=/dev/cdrom of=/root/cd.iso  # 备份光盘内容到/root/cd.iso 
```

### mkfs

格式化分区

```shell
mkfs -t ext4 /dev/sdb1   # 格式化/dev/sdb1分区为ext4
mkfs.ext4 /dev/sdb1      # 格式化/dev/sdb1分区为ext4
mkfs.ntfs /dev/sdb1      # 格式化/dev/sdb1分区为ntfs
```

### fsck

文件系统修复

| 选项 | 含义                                             |
| ---- | ------------------------------------------------ |
| -a   | 不用显示用户提示，自动修复文件系统               |
| -y   | 自动修复。和-a作用一致，不过有些文件系统只支持-y |

```shell
fsck -y /dev/sda1   # 自动修复/dev/sda1分区，需要先卸载分区
```

### swap交换分区

#### mkswap

格式化swap文件

```shell
mkswap /swapfile    # swap文件
mkswap /dev/sdb6    # swap分区
```

#### swapon

加入swap

```shell
swapon /swapfile    # swap文件
swapon /dev/sdb6    # swap分区
```

#### swapoff

取消swap分区

```shell
swapoff /dev/sdb6    # swap文件
swapoff /dev/sdb6    # swap分区
```

### LVM管理

#### pvcreate

创建物理卷

```shell
pvcreate /dev/sd[b,c,d]1
```

#### pvs

查看物理卷

#### vgcreate

创建卷组

```shell
vgcreate vg1 /dev/sdb1 /dev/sdc1
```

#### lvcreate

创建逻辑卷

```shell
lvcreate -L 100M -n lv1 vg1
```

#### lvs

查看逻辑卷

#### vgextend

扩充卷组

```shell
vgextend centos /dev/sdd1
```

#### lvextend

扩充逻辑卷

```shell
lvextend -L +100G /dev/centos/root
```

#### xfs_growfs

扩充文件系统

```shell
xfs_growfs /dev/centos/root
```

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

hexdump
