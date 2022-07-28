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

### Python版本选择：

Python3是未来

Python发行版： Anaconda （包含大量库）

### Python编程利器：

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

元组存储数据<span style='color:red'>不可变更</span>，而列表可以变更。

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

<span style='color:red'>注意：中文GB2312编码一个中文字符占两个字节的指针，seek偏移按字节计算</span>

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
<span style='color:red'>NameError: name 'j' is not defined</span>

##### 语法错误：
<span style='color:red'>SyntaxError: invalid syntax</span>

##### 序列或元组超出范围：
例：

```python
a='123'
print(a[3])
```

<span style='color:red'>IndexError: string index out of range</span>

##### 字典键值错误：

例：

```python
d = {'a':2, 'c':3}
print(d['b'])
```

<span style='color:red'>KeyError: 'b'</span>

##### 输入类型错误：

例：

```python
year = int(input('input year:'))
```

<span style='color:red'>ValueError: invalid literal for int() with base 10: 'iji'</span>

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

<span style="color:red;">AttributeError: 'int' object has no attribute 'append'</span>

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

#### <span style='color:red'>文件操作最终要关闭文件</span>

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

# 函数、模块

## 函数的定义和常用操作

### 统计小说人物出现次数案例

使用Python对小说内容进行分析，统计出主角的出现次数

```python
f = open('name.txt')
data = f.read()
print(data.split('|'))
# 读取兵器的名称
f2 = open('weapon.txt')
# data2 = f2.read()
i = 1
for line in f2.readlines():
	if i % 2 == 1:
		# strip()把\n换行符删除
		print(line.strip('\n'))
	i +=1
# GB18030的编码比GB2312多，使用GB2312打开会有部分编码不支持
f3 = open('sanguo.txt', encoding='GB18030')
# replace做字符替换，将换行符替换掉
print(f3.read(),replace('\n',''))
```

### 函数

函数是对程序逻辑进行结构化的一种编程方法

函数的定义:

``` python
def 函数名称():
	代码
    return 需要返回的内容
```

函数的调用:

```python
函数名称()
```

函数名称以字母或下划线开头，中间为数字、字母和下划线

例：

```python
import re
def find_main_charecters( charecter_name ):
	with open('sanguo.txt', encoding='GB18030') as f:
		data = f.read().replace('\n', '')
		name_num = re.findall(charecter_name, data)
		# print('主角 %s 出现 %s 次数' %(hero,len(name_num)))
	return charecter_name, len(name_num)
# 读取人物的信息
name_dict = {}
with open('name.txt', encoding='GB18030') as f:
	for line in f:
		names = line.split('|')
		for n in names:
			name, name_num = find_main_charecters(n)
			name_dict[n] = name_num
# 读取武器信息
weapon_dict = {}
with open('weapon.txt', encoding='GB18030') as f:
	i = 1
	for line in f:
		if i%2 == 1:
			weapon_name, weapon_number = find_main_charecters(line.strip())
			weapon_dict[weapon_name] = weapon_number
		i += 1
# 字典排序
name_sorted = sorted(name_dict.items(), key=lambda item: item[1], reverse=True)
print(name_sorted[0:10])
weapon_sorted = sorted(weapon_dict.items(), key=lambda item: item[1],reverse=True)
print(weapon_sorted[0:10])
```

## 函数的可变长参数

函数调用默认按顺序传参，如果不按顺序传参则使用关键字参数

例：

```python
print('abc', end='\n\n')
print('123')
```

例：

```python
def func (a, b, c):
	print('a= %s' %a)
	print('b= %s' %b)
	print('c= %s' %c)

func(1, c=4, b=3)
```

### 可变长函数

例：

```python
# 取得参数的个数
def howlong(first, *other):
	print(1 + len(other))
howlong(123, 456, 789)
```

## 函数的变量作用域

### 函数内和函数外同名变量

例：

```python
var1 = 123
def func():
	# var1 = 456
	print(var1)
func()
```

输出：

```python
123
```

例：

```python
var1 = 123
def func():
	var1 = 456
	print(var1)
func()
print(var1)
```

输出：

```python
456
123
```

### 在函数内使用全局变量使用关键字global

例：

```python
var1 = 123
def func():
	global var1
	var = 456
	print(var1)
func()
print(var1)
```

输出：

```python
456
456
```

## 函数的迭代器与生成器

### 迭代器

用于循环操作列表

例：

```python
# 循环输出列表
list1 = [1, 2, 3]
it = iter(list1)
print(next(it))
print(next(it))
print(next(it))
print(next(it)) #except
```

输出：

```python
1
2
3
>>>出错
```

### 生成器

例：

```python
# range循环输出，range（起始，终止，步长）
for i in range(10, 20, 2):
	print(i)
```

<span style='color:red'>步长无法使用小数</span>

#### 使用生成器构建函数

例：

```python
def frange(start, stop, step):
	x = start
	while x < stop:
		yield x
		# yield生成器，每次返回数值并记录位置，下次调用再继续
		x += step
for i in frange(10, 20, 0.5):
	print(i)
```

## lambda表达式

例：

```python
def true():return True
lambda : True
```

例：

``` python
def add(x, y):return x + y
lambda x, y : x + y
```

例：

```python
lambda x:x<= (month, day)
```

等效于:arrow_down:

```python
def func1(x):
	return x <= (month, day)
```

例：

```python
lambda item:item[1]
```

等效于:arrow_down:

```python
def func2(item):
	return item[1]
adict = {'a':'aa','b':'bb'}
for i in adict.items():
	print(func2(i))
```

输出：

```python
'aa'
'bb'
```

返回字典的值

lambda可以简化简单的函数处理

## python内建函数

### filter()

filter(函数，迭代器)

例：

```python
a = [1,2,4,5,6,7,8]
print(list(filter(lambda x:x>2, a)))
```

输出a列表中大于2的元素

### map()

map(函数，可变长参数)

例：

```python
a = [1,2,3,4]
print(list(map(lambda x:x+1, a)))
```

输出：

```py
[2, 3, 4, 5]
```

a列表每个元素+1



例：

```python
a = [1,2,3,4]
b = [3,4,5,6]
print(list(map(lambda x,y:x+y, a,b)))
```

输出：

```python
[4, 6, 8, 10]
```

a和b的对应元素相加

### reduce()

导入reduce模块

```python
from functools import reduce
reduce(函数，序列[, 初始值])
```

把序列和初始值按照函数方式运算

例：

```python
print(reduce(lambda x,y: x+y, [2,3,4], 1))
```

输出：

```python
10
```

初始值1+序列第一个值2的结果作为x接着与序列第二个值相加再与第三个值相加，即（（（1+2）+3）+4）

### zip()

```python
for i in zip((1,2,3), (4,5,6)):
	print(i)
```

输出：

```python
(1, 4)
(2, 5)
(3, 6)
```

可迭代函数，即帮助中有`__iter__`字段可使用for循环

例：

```python
dicta = {'a':'aa','b':'bb'}
dictb = zip(dicta.values(),dicta.keys())
print(dict(dictb))
```

输出：

```python
{'aa': 'a', 'bb': 'b'}
```

实现字典key和数值对调

### help()  显示帮助

```python
help(zip)
```

## 闭包的定义

函数嵌套，内部函数引用外部函数的变量称为闭包

例：

```python
def func():
	a = 1
	b = 2
	return a + b
def sum(a):
	def add(b):
		return a+b
	return add     #返回函数名
# add 函数名称或函数引用
# sdd() 函数调用
num1 = func()
num2 = sum(2)
print(type(num1))
# 返回类型为函数
print(type(num2))
print(num2(4))
```

输出：

```python
<class 'int'>
<class 'function'>
6
```

计数器，例：

```python
# 使用闭包定义计数器，每调用一次加1，可传递初值，空则从0开始计数
def counter(FIRST=0):
	cnt =[FIRST] 
	def add_one():
		cnt[0] += 1
		return cnt[0]
	return add_one
# 分开计数
num5 = counter(5)
num10 = counter(10)
print(num5())
print(num5())
print(num5())
print(num10())
print(num10())
```

输出：

```python
6
7
8
11
12
```

## 闭包的使用

```python
# a * x + b = y, 数学计算，调用一次固定a和b，下次仅传x
def a_line(a,b):
	def arg_y(x):
		return a*x+b
	return arg_y

# 使用lambda进一步简化
def b_line(a,b):
	return lambda x: a*x+b
    
# a=3,b=5
# x=10 y=?
# 可使用多条直线函数
line1 = a_line(3,5)
line2 = a_line(5,10)
print(line1(10))
print(line1(20))
print(line2(5))
```

输出：

```python
35
65
35
```

## 装饰器的定义

### time库的使用

```python
import time
# 显示1970年1月1日至今的秒数
print(time.time())
# 延时3秒
time.sleep(3)
```

### 计算运行时间：

```python
import time
# 显示1970年1月1日至今的秒数
#print(time.time())
# 延时3秒
def i_can_sleep():
    time.sleep(3)
start_time = time.time()
i_can_sleep()
stop_time = time.time()
print('函数运行了 %s 秒' %(stop_time - start_time))
```

输出：

```python
函数运行了 3.003718614578247 秒
```

### 使用装饰器

```python
import time
def timer(func):
	def wrapper():
		start_time = time.time()
		func()
		stop_time = time.time()
		print("运行时间是 %s 秒" % (stop_time - start_time))
	return wrapper

# 延时3秒
@timer #@语法塘，timer=>装饰函数，
def i_can_sleep():  #被装饰函数
	time.sleep(3)

i_can_sleep()
```

输出：

```python
运行时间是 3.0025811195373535 秒
```

## 装饰器的使用

### 不带参数的装饰器的伪代码：

```python
def wai(func):
    def nei():
        start ...
        func()
        stop ...
        [return ...]
    return nei
```

### 带参数的装饰器:

```python
# 带参修饰器
def new_tips(argv):
	def tips(func):
		def nei(a,b):
			# 修饰器参数，被修饰函数名
			print('start %s,function name %s' %(argv, func.__name__))
			func(a,b)
			print('stop %s' %argv)
		return nei
	return tips
@new_tips('add_module')
def add(a,b):
	print(a+b)
@new_tips('sub_module')
def sub(a,b):
	print(a-b)
sub(3,4)
add(5,2)
```

输出：

```python
start sub_module,function name sub
-1
stop sub_module
start add_module,function name add
7
stop add_module
```

## 上下文管理器

```python
fd = open('name.txt')
try:
    for line in fd:
        print(line)
finally:
    fd.close()
# with ... as 即上下文管理器，
# 出错后执行最终的类似以上写法的finally:来关闭文件
with open('name.txt') as f:
    for line in f:
        print(line)
```

## 模块的定义

### 模块

模块是在代码量变得相当大之后，为了将需要重复使用的有组织的代码段放在一起，这部分代码可以附加到现有的程序中，附加的过程叫做导入（import）

### 导入模块的一般写法

- import 模块名称
- form 模块名称 import 方法名

#### 导入模块并简化写法:

```python
import time as t
t.sleep()
```

#### 不推荐写法 ，省略模块名:

```python
from time import sleep
sleep()
```

### 编写模块：

模块文件名： mymod.py

```python
def print_me():
    print('me')
    
# print_me()
```

调用编写的模块文件：

```python
import mymod
mymod.print_me()
```

输出：

```python
me
```

## PEP8编码规范

### 遵循编码规范

[https://peps.python.org/pep-0008/](https://peps.python.org/pep-0008/)

### 自动格式化软件安装

#### pyCharm

pip install autopep8

pyCharm添加pep8：

属性=>扩展工具=>添加=>pep8

使用：

右键=>扩展工具=>pep8

#### vscode

vscode 安装python插件 

右键=>格式化文档

# 面向对象编程

## 类与实例

```python
# 面向过程编程
user1 = {'name':'tom', 'hp':100}
user1 = {'name':'jerry', 'hp':80}
def print_role(rolename):
	print('name is %s, hp is %s' %(rolename['name'],rolename['hp']))
print_role(user1)

# 面向对象的编程
class Player():     # 定义一个类，类名以大写字母开头
	def __init__(self,name,hp):  # 实例化一个类后自动执行
		self.name = name
		self.hp= hp
	def print_role(self):   #定义一个方法
		print('%s: %s' %(self.name,self.hp))

user1 = Player('tom',100)  #类的实例化
user2 = Player('jerry',90)

user1.print_role()
user2.print_role()
```

输出：

```python
tom: 100 
jerry: 90
```

## 如何增加类的属性和方法

### 定义空类：

```python
class Monster():
	'定义怪物类'
	pass
```

### 增加类的属性和方法：

```python
class Player():     # 定义一个类
	def __init__(self, name, hp, occu):  # 实例化一个类后自动执行
		self.name = name  # 变量称作属性
		self.hp = hp
		self.occu = occu
    def print_role(self):  # 定义一个方法
		print('%s: %s %s' % (self.name, self.hp, self.occu))
	def update_name(self, newname):
		self.name = newname

user1 = Player('tom', 100, 'war')  # 类的实例化
user2 = Player('jerry', 90, 'master')

user1.print_role()
user2.print_role()

user1.update_name('willsen')
user1.print_role()
```

输出：

```python
tom: 100 war
jerry: 90 master
willsen: 100 war
```

可以通过赋值的方式修改name属性：

```python
user1.name = 'aaa'
user1.print_role()
```

### 类的封装：

```python
class Player():     # 定义一个类
    def __init__(self, name, hp, occu):  # 实例化一个类后自动执行
        self.__name = name  # 变量称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):  # 定义一个方法
        print('%s: %s %s' % (self.__name, self.hp, self.occu))
    def update_name(self, newname):
        self.__name = newname

user1 = Player('tom', 100, 'war')  # 类的实例化
user2 = Player('jerry', 90, 'master')

user1.print_role()
user2.print_role()

user1.update_name('willsen')
user1.print_role()

user1.__name = 'aaa'
user1.print_role()
```

输出：

```python
tom: 100 war
jerry: 90 master
willsen: 100 war
willsen: 100 war
```

<span style='color:red'>即无法通过赋值的方式修改name属性，只能通过update_name方法修改name</span>

## 类的继承

### 继承的概念

猫科动物（父类） -> 猫（子类）

### 定义子类

class 子类名(父类名):

```python
class Monster():  # 父类
    '定义怪物类'
    def __init__(self,hp=100):
        self.hp = hp
    def run(self):
        print('移动到某个位置')
    def whoami(self):
        print('我是怪物父类')

class Animals(Monster):   #子类
    '普通怪物'
    def __init__(self, hp=10):
        # 子类中重复父类的初始化
        super().__init__(hp)

class Boss(Monster):   #子类
    'Boss类怪物'
    def __init__(self, hp=1000):
        # 子类中重复父类的初始化
        super().__init__(hp)

    def whoami(self):  #重复方法会覆盖父类中的方法
        print('我是怪物我怕谁')

a1 = Monster(200)
print(a1.hp)
print(a1.run())
a2 = Animals(1)
print(a2.hp)
print(a2.run())
a3 = Boss(800)
a3.whoami()
```

输出：

```python
200
移动到某个位置
None
1
移动到某个位置
None
我是怪物我怕谁
```

```python
# 打印对象属于哪个类
print('a1的类型 %s' %type(a1))
print('a2的类型 %s' %type(a2))
print('a3的类型 %s' %type(a3))
# 判断对象a2是否属于Monster的子类，返回True、False
# 用于判断是否属于继承关系
print(isinstance(a2,Monster))
```

父类和子类都定义了同名方法，子类会覆盖父类的方法（多态）

元组、列表和字符串都是类，都继承于object父类

类是描述具有相同属性和方法的集合。

类的特性：

- 封装（无法访问的属性）；
- 继承（子类继承父类的属性和方法）；
- 多态（父类定义的方法，子类可以覆盖）。



类无法直接应用，必须实例化才能操作。

## 类的使用-自定义with语句

### with语句的正常调用：

```python
class Testwith():
    def __enter__(self):
        print('run')
    def __exit__(self,exc_type, exc_val, exc_tb):
        print('exit')
with Testwith():
print('Test is running')
```

输出：

```python
run
Test is running
exit
```

### with语句异常处理：

```python
class Testwith():
    def __enter__(self):
        print('run')
    def __exit__(self,exc_type, exc_val, exc_tb):
        if exc_tb is None:
            print('正常结束')
        else:
            print('has error %s' %exc_tb)
with Testwith():
    print('Test is running')
raise NameError('testNameError')
```

输出：

```python
run
Test is running
has error <traceback object at 0x000002D4E2F80840>
Traceback (most recent call last):
    File "with_test.py", line 26, in <module>
    raise NameError('testNameError')
NameError: testNameError
```

# 多线程编程

## 多线程编程的定义

### 启动5个进程

```python
import threading
import time
from threading import current_thread

def myThread(arg1, arg2):
    print(current_thread().name, 'start')
    print('%s %s' %(arg1, arg2))
    time.sleep(1)
    print(current_thread().name, 'stop')

for i in range(1, 6, 1):  # 循环5次
    # t1 = myThread(i, i+1)
    # 设置线程
    t1 = threading.Thread(target=myThread, args=(i, i+1))
    # 启动线程
    t1.start()
print(current_thread().name, 'end')
```

输出：

```python
Thread-1 (myThread) start
1 2
Thread-2 (myThread) start
2 3
Thread-3 (myThread) start
3 4
Thread-4 (myThread) start
4 5
Thread-5 (myThread) start
5 6
MainThread end
Thread-5 (myThread) stop
Thread-3 (myThread) stop
Thread-2 (myThread) stop
Thread-1 (myThread) stop
Thread-4 (myThread) stop
```

分别启动5个线程执行，最后主线程先结束，子线程后结束

### 重定义Thread类里的run，使子进程先结束

``` python
import threading
from threading import current_thread
# threading.Thread().run()
# 继承threading模块里的Thread类
class Mythread(threading.Thread):
    # 重定义run方法，覆盖Thread类里的run
    def run(self):
        print(current_thread().name, 'start')
        print('run')
        print(current_thread().name, 'stop')

t1 = Mythread()
t1.start()
t1.join()  # 等待线程结束

# 主线程结束
print(current_thread().name, 'end')
```

输出：

```python
Thread-1 start
run
Thread-1 stop
MainThread end
```

## 经典的生产者和消费者问题

水池不同粗细的水管进排水

程序产生数据，用户消耗数据

称为生产者和消费者问题

使用队列处理

### 队列简单使用

```python
>>>import queue
>>>q = queue.Queue()
>>>q.put(1)  # 把数据放入队列
>>>q.put(2)
>>>q.put(3)
>>>q.get()   #从队列中取出数据
1
>>>q.get()
2
>>>q.get()
3
```

### 生产者和消费者代码演示：

```py
from threading import Thread, current_thread
import time  # sleep
import random  # 随机数
from queue import Queue  # 队列
# 定义队列且长度为5
queue = Queue(5)

class ProducerThread(Thread):
    def run(self):
        name = current_thread().name
        nums = range(100)
        global queue
        while True:
            num = random.choice(nums)  # 生成随机数
            queue.put(num)  # 把随机数放入队列
            print('生产者 %s 生产了数据 %s' % (name, num))
            t = random.randint(1, 3)
            time.sleep(t)
            print('生产者 %s 睡眠了 %s 秒' % (name, t))

class ConsumerThread(Thread):
    def run(self):
        name = current_thread().name
        global queue
        while True:
            num = queue.get()  # 从队列里取数据
            queue.task_done()  # 线程等待和线程同步
            print('消费者 %s 消耗了数据 %s' % (name, num))
            t = random.randint(1, 5)
            time.sleep(t)
            print('消费者 %s 睡眠了 %s 秒' % (name, t))

# 1个生产者
p1 = ProducerThread(name='p1')
p1.start()
# 2个消费者
c1 = ConsumerThread(name='c1')
c1.start()
c2 = ConsumerThread(name='c2')
c2.start()
```

输出：

```python
生产者 p1 生产了数据 32
消费者 c1 消耗了数据 32
生产者 p1 睡眠了 1 秒
生产者 p1 生产了数据 94
消费者 c2 消耗了数据 94
消费者 c1 睡眠了 3 秒
消费者 c2 睡眠了 2 秒
生产者 p1 睡眠了 3 秒
生产者 p1 生产了数据 30
消费者 c1 消耗了数据 30
消费者 c1 睡眠了 2 秒
生产者 p1 睡眠了 3 秒
生产者 p1 生产了数据 5
消费者 c2 消耗了数据 5
消费者 c2 睡眠了 1 秒
生产者 p1 睡眠了 3 秒
```
3个生产者，2个消费者

```python
# 3个生产者
p1 = ProducerThread(name='p1')
p1.start()
p2 = ProducerThread(name='p2')
p2.start()
p3 = ProducerThread(name='p3')
p3.start()
# 2个消费者
c1 = ConsumerThread(name='c1')
c1.start()
c2 = ConsumerThread(name='c2')
c2.start()
```

输出：

```python
生产者 p1 生产了数据 67
生产者 p2 生产了数据 60
生产者 p3 生产了数据 54
消费者 c1 消耗了数据 67
消费者 c2 消耗了数据 60
消费者 c2 睡眠了 1 秒
消费者 c2 消耗了数据 54
生产者 p1 睡眠了 3 秒
生产者 p3 睡眠了 3 秒
生产者 p1 生产了数据 7
生产者 p3 生产了数据 57
生产者 p2 睡眠了 3 秒
生产者 p2 生产了数据 85
消费者 c2 睡眠了 3 秒
消费者 c2 消耗了数据 7
消费者 c1 睡眠了 5 秒
消费者 c1 消耗了数据 57
生产者 p3 睡眠了 2 秒
生产者 p3 生产了数据 50
生产者 p1 睡眠了 3 秒
消费者 c1 睡眠了 1 秒
生产者 p1 生产了数据 45
消费者 c1 消耗了数据 85
生产者 p2 睡眠了 3 秒
生产者 p2 生产了数据 67
```

