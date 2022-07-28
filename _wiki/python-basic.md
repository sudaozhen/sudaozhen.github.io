---
layout: wiki
title: Python 基础
cate1: Program language
cate2: Python
categories: Python
description: Python 基础知识。
keywords: Python, code, program 
---

# Python 介绍与安装

## Python 的发展历史与版本

![](D:\test\sudaozhen.github.io\images\wiki\python\image1.png)

Python版本选择：

Python3是未来

Python发行版： Anaconda （包含大量库）

Python编程利器：

Python官方文档

[https://www.python.org/doc](https://www.python.org/doc)

iPython

[https://www.ipython.org](https://www.ipython.org)

jupyter notbook 网页编程

[http://jupyyer-notebook.readthedocs.io/en/latest/](http://jupyyer-notebook.readthedocs.io/en/latest/)

sublime text 专业编辑器

[https://www.sublimetext.com](https://www.sublimetext.com)

PyCharm Python IDE

[https://www.jetbrains.com/pycharm/](https://www.jetbrains.com/pycharm/)

Pip

[https://pip.pypa.io/en/stable/installing/](https://pip.pypa.io/en/stable/installing/)

## Python的安装

### python解释器下载：

[www.python.org](http://www.python.org)

推荐下载3.x版本

### python IDE下载：

https://www.jetbrains.com/pycharm/      推荐下载社区版

或使用vscode

vscode + Python插件 + Pylance插件 + Code Runner插件

### 运行python：

#### 命令行输入:

python3

#### 退出：（英文括号）

exit()

#### Python文件命名

xxx.py

## Python程序的书写规则

\#开头是注释

import  导入模块

缩进（4个空格） 来区分同一语句块

# 变量、数字、序列、映射和集合

## 基础数据类型

### 基本数据类型

#### 数据类型

- 整形（int）      8

- 浮点型（float）   8.8

- 字符串（str）    “8” “Python”

- 布尔型（bool）   True、False


#### type()：显示数据类型

- type(8)

- type('8')

- type(True)


### 数据类型转换：

| 函数名 | 含义         | 用法                                         |
| ------ | ------------ | -------------------------------------------- |
| int()  | 转换为整型   | int('8')                                     |
| str()  | 转换为字符串 | str(123)                                     |
| bool() | 转换为布尔值 | bool(123)；bool值：非0 为 True，0 为 False。 |

## 变量的定义和常用操作

### 网络带宽计算器案例

![](D:\test\sudaozhen.github.io\images\wiki\python\image2.png)

### 变量

![](D:\test\sudaozhen.github.io\images\wiki\python\image3.png)

```python
bandwidth = 100
ratio = 8
print(bandwidth/ratio)
```

### 变量的命名

- 临时变量使用单字符
- 其余变量要有意义
- 驼峰命名 bandWidth
- BandWidth
- band_width

定义：

- 以字母和下划线开头，中间可以包括下划线、字母和数字
- 下划线开头用于特殊含义

## 序列的概念

### 计算生肖和星座案例

![](D:\test\sudaozhen.github.io\images\wiki\python\image4.png)

### 序列

序列是指它的成员都是有序排列，并且可以通过下标偏移访问到它的一个或几个成员，字符串、列表、元组三种类型都属于序列

字符串："abcd"

列表：[0,"abcd"]

元组：("abc","def")

### 编写思想：

1. 考虑面对什么样的问题？
2. 生活中用什么样的方式去解决？
3. 编程的用什么思路去解决？
4. 编写相应代码并测试。

单引号和双引号没有区别，双引号里使用单引号。

``` python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
print(chinese_zodiac[0])    #0开始
print(chinese_zodiac[0:4])  #0到3，4的前一个
print(chinese_zodiac[-1])   #负数表示倒数，-1倒数第一个
```

## 字符串的定义和使用

```python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
# print(chinese_zodiac[0])    #0开始
# print(chinese_zodiac[0:4])  #0到3，4的前一个
# print(chinese_zodiac[-1])   #负数表示倒数，-1倒数第一个
year =2022
# print (year % 12)
print (chinese_zodiac[year % 12 - 4])
```

## 字符串的常用操作

### 序列的基本操作

#### 成员关系 操作符

（in、not in）

对象 [not] in 序列

```python
print ('马' not in chinese_zodiac)
```

False

#### 连接 操作符

（+）

序列 + 序列

```python
print ('马' + '龙' + chinese_zodiac)
```
#### 重复 操作符

（*）

序列 * 整数

```python
print('马' * 3)
print(chinese_zodiac * 3)
```

#### 切片操作符

序列[0:整数]

## 元组的定义和常用操作

元组大小比较

```python
(4) < (6)
```

True

```python
(1,20) < (1,11)  #当成120和111比较
```

False

元组存储数据不可变更，而列表可以变更。

```python
filter()  #取元组中大于或小于某变量的元素

a = (1,2,3,6,7,8)
b=4
filter(lambda x:x < b , a)   #取出a中小于b的元素
list (filter(lambda x:x < b , a))  #取出a中小于b的元素并显示出来
len (list (filter(lambda x:x < b , a)))  #取出a中小于b的元素并显示个数
```

```python
zodiac_name = (u'魔羯座',u'水瓶座',u'双鱼座',u'白羊座',u'金牛座',u'双子座',
               u'巨蟹座',u'狮子座',u'处女座',u'天秤座',u'天蝎座',u'射手座',)
zodiac_days = ((1,20), (2,19), (3,21), (4,21), (5,21), (6,22), 
                (7,23), (8,23), (9,23), (10,23), (11,23), (12,23))
(month, day) = (2, 15)  #定义日期
#取出小于等于指定日期的元组
zodiac_day = filter(lambda x: x <= (month, day), zodiac_days)  
#将取出的元组转换成列表并计算个数然后对12取余
zodiac_len = len(list(zodiac_day)) % 12
#打印取余后的结果所对应的元组下标
print(zodiac_name[zodiac_len])
```

# 条件和循环

## 条件语句

条件语句：if

if语句包含：关键字，判断条件表达式，判断为真时的代码块

​		if表达式:

​				代码块

例：

```python
x = 'abc'
if x == 'abc' :
      print('x 的值和 abc 相等')
```

if语句还可以和else、elif（else-if）语句组合成更复杂的判断

```python
if表达式：
	代码块
elif表达式：
	代码块
else：
	代码块
```

例：

```python
x = 'abcd'
if x == 'abc' :
    print('x 的值和 abc 相等')
else:
    print('x 的值和 abc 不相等')
```

例：

```python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
#输入的是字符串用int()将其转化为整型

year = int(input('请用户输入出生年份'))  
if (chinese_zodiac[year % 12 - 4]) == '虎':
	print('虎年运势。。。')
```

## for循环

### 循环语句

#### while语句

```python
while表达式：
	代码块
```

#### for语句

```python
for 迭代变量 in 可迭代对象：
	代码块
```

例：

```python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
for cz in chinese_zodiac:
	print(cz)
for i in range(1,13):
	print(i)
```

#### 遍历元组

例：

```python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
for year in range(2000,2023):
	print('%s 年的生肖是 %s' %(year, chinese_zodiac[year % 12 - 4]))
```

## while循环

例：

```python
num = 5
while True:
	print('a')
	num = num + 1
    
    if num > 10:
		break
```

例：

```python
import time
num = 5
while True:
	num = num + 1
    
	if num == 10:
		continue
	print(num)
	time.sleep(1)
```

## for循环语句中的if嵌套

```python
# u代表Unicode编码
zodiac_name = (u'魔羯座',u'水瓶座',u'双鱼座',u'白羊座',u'金牛座',u'双子座',
               u'巨蟹座',u'狮子座',u'处女座',u'天秤座',u'天蝎座',u'射手座',)
zodiac_days = ((1,20), (2,19), (3,21), (4,21), (5,21), (6,22), 
                (7,23), (8,23), (9,23), (10,23), (11,23), (12,23))
# 用户输入月份和日期
int_month = int(input('请输入月份：'))
int_day = int(input('请输入日期：'))
for zd_num in range(len(zodiac_days)):
	if zodiac_days[zd_num] >= (int_month, int_month):
		print(zodiac_name[zd_num])
		break
	elif int_month == 12 and int_day > 23 :
		print(zodiac_name[0])
		break
print (type(int_month))
```

## while循环语句中的if嵌套

```python
# u代表Unicode编码
zodiac_name = (u'魔羯座',u'水瓶座',u'双鱼座',u'白羊座',u'金牛座',u'双子座',
               u'巨蟹座',u'狮子座',u'处女座',u'天秤座',u'天蝎座',u'射手座',)
zodiac_days = ((1,20), (2,19), (3,21), (4,21), (5,21), (6,22), 
                (7,23), (8,23), (9,23), (10,23), (11,23), (12,23))
# 用户输入月份和日期
int_month = int(input('请输入月份：'))
int_day = int(input('请输入日期：'))

n = 0
while zodiac_days[n] < (int_month,int_day):
	if int_month == 12 and int_day > 23 :
		break
	n +=1
print(zodiac_name[n])
```

## 字典的定义和常用操作

映射的类型：字典

字典包含哈希值和指向的对象

```python
{"哈希值":"对象"}
{'length':180, 'width':80}
```

例：

```python
dict1 = {}
print(type(dict1))
dict2 = {'x':1 , 'y':2 }
dict2['z'] = 3
print(dict2)
```

通过字典的形式统计用户输入的生肖和星座数量

例：

```python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
zodiac_name = (u'魔羯座',u'水瓶座',u'双鱼座',u'白羊座',u'金牛座',u'双子座',
               u'巨蟹座',u'狮子座',u'处女座',u'天秤座',u'天蝎座',u'射手座',)
zodiac_days = ((1,20), (2,19), (3,21), (4,21), (5,21), (6,22), 
                (7,23), (8,23), (9,23), (10,23), (11,23), (12,23))
cz_num = {}
for i in chinese_zodiac:
	cz_num[i] = 0
z_num = {}
for i in zodiac_name:
	z_num[i] = 0
while True:
	# 用户输入月份和日期
	year = int(input('请用户输入出生年份'))   
	int_month = int(input('请输入月份：'))
	int_day = int(input('请输入日期：'))
	n = 0
	while zodiac_days[n] < (int_month,int_day):
		if int_month == 12 and int_day > 23 :
			break
		n +=1
	print(zodiac_name[n])
	print('%s 年的生肖是 %s' %(year, chinese_zodiac[year % 12 - 4]))
	cz_num[chinese_zodiac[year % 12 - 4]] += 1
	z_num[zodiac_name[n]] += 1
# 输出生肖和星座的统计信息
	for each_key in cz_num.keys():
		print('生肖 %s 有 %d 个' % (each_key,cz_num[each_key]))
    
	for each_key in z_num.keys():
		print('星座 %s 有 %d 个' % (each_key,z_num[each_key]))
```

## 列表推导式与字典推导式

列表推导式：

```python
# 从 1 到 10 所有偶数的平方
alist = []
for i in range(1,11):
	if (i % 2 == 0):
		alist.append( i*i )
print(alist)

blist = [i*i for i in range(1,11) if(i % 2) == 0]
print(blist)
```

字典推导式：

```python
z_num = {}
for i in zodiac_name:
	z_num[i] = 0

z_num = {i:0 for i in zodiac_name}
```

例：

```python
chinese_zodiac = '鼠牛虎兔龙蛇马羊猴鸡狗猪'
# u代表Unicode编码
zodiac_name = (u'魔羯座',u'水瓶座',u'双鱼座',u'白羊座',u'金牛座',u'双子座',
               u'巨蟹座',u'狮子座',u'处女座',u'天秤座',u'天蝎座',u'射手座',)
zodiac_days = ((1,20), (2,19), (3,21), (4,21), (5,21), (6,22), 
                (7,23), (8,23), (9,23), (10,23), (11,23), (12,23))
# cz_num = {}
# for i in chinese_zodiac:
#     cz_num[i] = 0
# z_num = {}
# for i in zodiac_name:
#     z_num[i] = 0
cz_num = {i:0 for i in chinese_zodiac}
z_num = {i:0 for i in zodiac_name}

while True:
	# 用户输入月份和日期
	year = int(input('请用户输入出生年份'))   
	int_month = int(input('请输入月份：'))
	int_day = int(input('请输入日期：'))
	n = 0
	while zodiac_days[n] < (int_month,int_day):
		if int_month == 12 and int_day > 23 :
			break
		n +=1
	print(zodiac_name[n])
	print('%s 年的生肖是 %s' %(year, chinese_zodiac[year % 12 - 4]))
	cz_num[chinese_zodiac[year % 12 - 4]] += 1
	z_num[zodiac_name[n]] += 1
# 输出生肖和星座的统计信息
	for each_key in cz_num.keys():
		print('生肖 %s 有 %d 个' % (each_key,cz_num[each_key]))
    
	for each_key in z_num.keys():
		print('星座 %s 有 %d 个' % (each_key,z_num[each_key]))
```

# 文件、输入输出、异常

## 文件的内建函数

### 文件操作案例

使用Python对文件进行基本的读写操作

文件内建函数和方法

- open()    打开文件
- read()     输入
- readline()  输入一行
- seek()     文件内移动
- write()    输出
- close()    关闭文件

#### 文件写入流程

open() => write() => close()   close才保存

例：

``` python
file1 = open('name.txt','w')
file1.write('诸葛亮')
file1.close()
```

#### 文件读取流程

open() => read() => close()

例：

```python
file2 = open('name.txt')
print(file2.read())
file2.close()
```

例：

```python
file3 = open('name.txt','a')
file3.write('刘备')
file3.close()
```

## 文件的常用操作

例：

```python
# 读取一行
file4 = open('name.txt')
print(file4.readline())
file4.close()
```

例：

```python
# 循环读取每行
file5 = open('name.txt')
for line in file5.readlines():
	print(line)
	print('=====')
file5.close()
```

### seek()移动当前文件指针

例：

```python
file6 = open('name.txt')
print('当前文件指针的位置 %s' %file6.tell())
print('当前读取到了一个字符，字符的内容是 %s' %file6.read(1))
print('当前文件指针的位置 %s' %file6.tell())
file6.seek(0)
print('我们进行了seek操作')
print('当前文件指针的位置 %s' %file6.tell())
print('当前读取到了一个字符，字符的内容是 %s' %file6.read(1))
print('当前文件指针的位置 %s' %file6.tell())
file6.close()
```

例：

```python
file6 = open('name.txt')
print('当前文件指针的位置 %s' %file6.tell())
print('当前读取到了一个字符，字符的内容是 %s' %file6.read(1))
print('当前文件指针的位置 %s' %file6.tell())
# 第一个参数代表偏移位置，第二个参数：0 表示从文件开头偏移， 1 表示从当前位置偏移，2 从文件结尾
file6.seek(6,0)
print('我们进行了seek操作')
print('当前文件指针的位置 %s' %file6.tell())
print('当前读取到了一个字符，字符的内容是 %s' %file6.read(1))
print('当前文件指针的位置 %s' %file6.tell())
file6.close()
```

**注意：中文GB2312编码一个中文字符占两个字节的指针，seek偏移按字节计算**

## 异常的检测和处理

### 异常

错误 不等于 异常

异常是在出现错误时采用正常控制以外的动作

异常处理的一般流程是：检测到错误，引发异常；对异常进行捕获的操作

```python
try:
	<监控异常>
except Exception[, reason]:
	<异常处理代码>
finally:
	<无论异常是否发生都执行>
```

#### 错误类型：

##### 变量未定义：
NameError: name 'j' is not defined
##### 语法错误：
SyntaxError: invalid syntax
##### 序列或元组超出范围：
例：

```python
a='123'
print(a[3])
```

IndexError: string index out of range

##### 字典键值错误：

例：

```python
d = {'a':2, 'c':3}
print(d['b'])
```

KeyError: 'b'

##### 输入类型错误：

例：

```python
year = int(input('input year:'))
```

ValueError: invalid literal for int() with base 10: 'iji'

异常处理代码：

```python
try:
	year = int(input('input year:'))
except ValueError:
print('年份要输入数字')
```

##### 属性错误：

例：

```python
a = 123
a.append()
```

AttributeError: 'int' object has no attribute 'append'

#### 异常处理的组合，通过元组组合

```python
except (ValueError, AttributeError, KeyError)
```

#### 打印出错信息

```python
try:
	print(1/0)
except ZeroDivisionError as e:
print('0 不能做除数 %s' %e)
```

#### 打印所有错误信息

```python
try:
	print(1/'a')
except Exception as e:
print(' %s' %e)
```

#### 自定义错误类型

```python
try:
	raise NameError('helloError')
except NameError:
print('my custom error')
```

#### **文件操作最终要关闭文件**

```python
try:
	a = open('a.txt')
except Exception as e:
	print(e)
finally:
	a.close()
```

## 文件操作案例总结

### 文件和输入输出

- 文件对象
- 内建函数

### 异常处理

- 异常产生
- 异常检测
- 异常处理
