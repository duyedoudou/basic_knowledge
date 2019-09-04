### Python常用功能：

#####  把列表按空格输出：

```Python
a = [1,2,3]
c = [str(i) for i in a]
print(c)
print(' '.join(c))
```

```
['1', '2', '3']
1 2 3
```
##### 打印列表中某个元素的下标：

```Python
a = [2,3,'f',99,'tttr']
print(a.index('f'))
```

```
2
```

##### 输入存进二维列表：

```python
arr = []
for i in range(4):
    arr.append(list(map(int,input().split())))
print(arr)
```

```Python
1 2 3 4
2 3 4 2
2 1 3 4
1 5 4 6
[[1, 2, 3, 4], [2, 3, 4, 2], [2, 1, 3, 4], [1, 5, 4, 6]]
```
##### input输入的是字符串，转化成列表：

```Python
# 功能：input输入的是字符串，转化成列表。
# split()   默认空格,换行\n,制表符\t分割
#map(square, [1,2,3,4,5])   # 计算列表各个元素的平方  square是函数名
line = input()
l = list(map(int, line.split()))
print(l,type(l))
```

```
2 3 4 5
[2, 3, 4, 5] <class 'list'>
```

##### 生成二维列表：

![image-20190826101002053](/Users/mac/Library/Application Support/typora-user-images/image-20190826101002053.png)

##### 对字典按value值排序：！！sorted之后字典变成了元组组成的列表。

```Python
#知识点：sorted函数。sorted()的参数，链接很详细。
# ！！sorted之后字典变成了元组组成的列表。
#https://www.runoob.com/python/python-func-sorted.html
dicc = {9149: 0, 9150: 26, 9151: 24, 9158: 24, 9153: 25}
dicc2 = sorted(dicc.items(),key=lambda m:m[1])  # 按value排序
dicc3 = sorted(dicc.items(),key=lambda m:m[0])  # 按key排序
print(dicc2,type(dicc2))
print(dicc3,type(dicc3))
```

```
[(9149, 0), (9151, 24), (9158, 24), (9153, 25), (9150, 26)] <class 'list'>
[(9149, 0), (9150, 26), (9151, 24), (9153, 25), (9158, 24)] <class 'list'>
```

##### 内置的十进制转二进制：

```Python
a = bin(15)
print(a,type(a))  # 输出字符串形式
```

```
0b1111 <class 'str'>
```

##### 判断数字是奇数还偶数：

```
# n&1用来判断n是否为偶数。与运算：全1才出1

# 如果是偶数，n&1返回0；否则返回1，为奇数。
```

##### 统计列表中不同元素的个数:

```python 
#知识点Counter函数

import collections
numbers = [2,2,2,3,4,6,6,7,5]
c = collections.Counter(numbers)
print(c,type(c))
c = dict(c)          # 转换成字典格式
print(c,type(c))
c2 = sorted(c.items(),key = lambda m:m[0])
print(c2)
```

```
Counter({2: 3, 6: 2, 3: 1, 4: 1, 7: 1, 5: 1}) <class 'collections.Counter'>
{2: 3, 3: 1, 4: 1, 6: 2, 7: 1, 5: 1} <class 'dict'>
[(2, 3), (3, 1), (4, 1), (5, 1), (6, 2), (7, 1)]
```

##### 字符串修改。字符串是不可变量，无法直接修改：

```Python
# 思路二：使用replace()函数
a = 'we are happy.'
a= a.replace(' ','%20')
print(a)
```

```
we%20are%20happy.
```

```Python
#思路1：先把字符串转成列表，修改后，再拼接回去

# 知识点：join（）
#下边函数的功能是将字符串中的空格改成’%20‘
a = 'we are happy.'
b = list(a)
print(b)
for i in range(len(b)) :
    if b[i] == ' ':
        b[i] = '%20'
print(b)
a = '--'.join(b)
print(a)
```

```
['w', 'e', ' ', 'a', 'r', 'e', ' ', 'h', 'a', 'p', 'p', 'y', '.']
['w', 'e', '%20', 'a', 'r', 'e', '%20', 'h', 'a', 'p', 'p', 'y', '.']
w--e--%20--a--r--e--%20--h--a--p--p--y--.
```



##### 巧用sum函数给列表降维：

```Python
# 语法：sum(iterable[, start]) ，sum() 函数的第一个参数是可迭代对象，如列表、元组或集合等，
# 第二个参数是起始值，默认为 0 。其用途是以 start 值为基础，再与可迭代对象的所有元素相“加”。
# newlist = sum(oldlist,[])
# 执行效果是 oldlist 中的子列表逐一与第二个参数相加，而列表的加法相当于 extend 操作，
# 所以最终结果是由 [] 扩充成的列表。即，空列表变成了含有oldlist中所有子元素的一维列表。
# 这里有两个关键点：sum() 函数允许带两个参数，且第二个参数才是起点。
v = [[True, True, True, True], 
     [False, False, False, False], 
     [False, False, False, False], 
     [False, False, False, False], 
     [False, False, False, False]]
print(sum(v,[]))  
print(sum(sum(v,[])))  # 打印有多少个True
```

```
[True, True, True, True, False, False, False, False, False, False, False, False, False, False, False, False, False, False, False, False]
4
```

##### 合并多个数组为元组列表:

```python 
#知识点：zip函数，合并后，元素个数和最短的列表一致。
cc = [200,600,100,180,300,450]
vv = [6,10,3,4,5,8]
bb = [33,555,3,1,4,5]
nn = zip(cc,vv,bb)
for i in nn:
    print(i)
```

```
(200, 6, 33)
(600, 10, 555)
(100, 3, 3)
(180, 4, 1)
(300, 5, 4)
(450, 8, 5)
```

##### 逆时针旋转矩阵：

```python 
matrix = list(zip(*matrix))[::-1]   # 90度逆时针旋转剩下的矩阵元素
```

##### 顺时针旋转矩阵：

```python 
matrix = list(zip(*matrix[::-1]))   # 90度逆时针旋转剩下的矩阵元素
```

##### all()函数：

```
# all() 函数用于判断给定的可迭代参数 iterable 中的所有元素是否都为 TRUE，如果是返回 True，否则返回 False。

# 元素除了是 0、空、None、False 外都算 True。
```

#### ascii转化：

```python
a = '!'
b = 97
print(ord(a))
print(chr(b))
```

```
33
a
```

#### 生成空集合：

```
a = set() # 不能用{}，{}是用来生成空字典的
```

#### 集合的添加元素：

```
a.add('ws')
```

#### .index()方法：

```python 
a = 'dogdog'
print(a.index('g'))
print(a.index('og'))
print(list(map(a.index,a)))
```

```
2
1
[0, 1, 2, 0, 1, 2]
```

#### .find():

与.index（）的区别：

找不到的时候，find（）返回-1；index（）找不到就报错。







#### sort和sorted:

```python 
# 字符串没有sort()方法
s = 'wre'
s.sort()
```

```
AttributeError: 'str' object has no attribute 'sort'
```

```Python
# ！但是，可以使用sorted对str进行排序，
# 生成list格式
s = 'wre'
print(sorted(s))
```

```
['e', 'r', 'w']
```

#### collections.defaultdict():

> 生成一个字典，并默认好了字典的值的数据类型，如collections.defaultdict(list)  添加新的键，其值都是默认放在列表里。

```python
from collections import defaultdict
dic = defaultdict(list)
dic[2].append(3)
dic[2].append(4)
dic[2].append(3)
print(dic)
dicc = dict(dic)
print(dicc)
```

```
defaultdict(<class 'list'>, {2: [3, 4, 3]})
{2: [3, 4, 3]}
```

#### 输出字典的值到 【列表】：dic.values()

```Python
dic = {2:[3,7],4:[6,5]}
dic2 = {4:6,2:3}
print(dic.values())
print(dic2.values())
```

```
dict_values([[3, 7], [6, 5]])
dict_values([6, 3])
```





#### enumerate() 函数:

> #### 用于将一个可遍历的数据对象组合为一个索引序列，同时列出数据和数据下标

```python
a = ['Spring', 'Summer', 'Fall', 'Winter']
print(list(enumerate(a)))
print(list(enumerate(a,start=1)))  # 下标从1开始
```

```
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

#### 合并两个字典：

```python
d1 = {'dog':3,'cat':5}
d2 = {'miemie':2,'gigi':7}
d1.update(d2)
print(d1)
```

```
{'dog': 3, 'cat': 5, 'miemie': 2, 'gigi': 7}
```

#### 使用zip实现字典的键值反转：

```Python
d1 = {'dog': 3, 'cat': 5, 'miemie': 2, 'gigi': 7}
d2 = dict(zip(d1.values(),d1.keys()))
print(d2)
```

```
{3: 'dog', 5: 'cat', 2: 'miemie', 7: 'gigi'}
```

#### zip合并不同类型，只要可迭代就行：

```python 
a = [1,2,3]
b = 'edw'
c = list(zip(a,b))
d = dict(zip(a,b))
print(c)
print(d)
```

```
[(1, 'e'), (2, 'd'), (3, 'w')]
{1: 'e', 2: 'd', 3: 'w'}
```







#### operator 里的 itemgetter：

> 对字典组成的列表排序，按照字典的某一个/几个字段。

```python
rows = [
    {'fname': 'Big', 'lname': 'Jones', 'uid': 1003},
    {'fname': 'David', 'lname': 'Beazley', 'uid': 1002},
    {'fname': 'John', 'lname': 'Cleese', 'uid': 1001},
    {'fname': 'Big', 'lname': 'Aones', 'uid': 1004}]
from operator import itemgetter
rows_sortby_fname = sorted(rows,key=itemgetter('fname'))
print(rows_sortby_fname)
print('--')
rows_sortby_fname2 = sorted(rows,key=itemgetter('fname','lname'))
print(rows_sortby_fname2)
```

```
[{'fname': 'Big', 'lname': 'Jones', 'uid': 1003},
 {'fname': 'Big', 'lname': 'Aones', 'uid': 1004}, 
 {'fname': 'David', 'lname': 'Beazley', 'uid': 1002}, 
 {'fname': 'John', 'lname': 'Cleese', 'uid': 1001}]
 --
[{'fname': 'Big', 'lname': 'Aones', 'uid': 1004}, 
{'fname': 'Big', 'lname': 'Jones', 'uid': 1003}, 
{'fname': 'David', 'lname': 'Beazley', 'uid': 1002}, 
{'fname': 'John', 'lname': 'Cleese', 'uid': 1001}]
```

#### 一道关于lambda函数的经典面试题:

#### list[0]能输出什么？这个主要考函数对象列表，千万不要和列表表达式搞混了啊

```python
list = [ lambda x:x*x for x in range(1, 3)]
print(list)
print(list[0])
print(list[1](5))
```

```
[<function <listcomp>.<lambda> at 0x7f3029c45ea0>, <function <listcomp>.<lambda> at 0x7f3029c45e18>]
<function <listcomp>.<lambda> at 0x7f3029c45ea0>
25
```

#### 统计字符串中有多少个某字母/字符串：

```python 
a = 'wwwderft'
print(a.count('w'))
print(a.count('er'))
```

```
3
1
```

#### 题目：

> 统计字符串A中有多少个字符也在字符串B中可以找到
>
> 分析：
>
> python自带的string.count(char)函数的作用是统计一个字符串string含有字符char的数量。在本例中strB相当于char的一个参数列表["a", "A"], map函数先统计strA中字符a的数量，再统计strA中字符A的数量，获得列表[1, 3], 然后将它们相加，即可获得字符串A中总共有多少字符可以在B中找到。

```python 
strA = "aAAAbBCC"
strB = "aA"
print(sum(map(strA.count,strB)))
```

```
4
```

#### reduce()函数：

> 用传给 reduce 中的函数 function先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。

```Python
from functools import reduce
a = [1,2,3,4]
b = reduce(lambda x,y:x+y,a)
print(b)
```

```
10
```

#### filter()函数：

> 过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表

```Python
a = list(filter(lambda x:x%2 == 0,range(1,10)))
print(a)
```

```
[2, 4, 6, 8]
```







#### 判断字符串是否以‘te’结尾：

```python 
a = 'wdsdfertr'
print(a.endswith('rtr'))
print(a.endswith('twr'))
```

```
True
False
```

#### 字符串大小写小小的总结：

```Python
a = 'i love you. Do you know? BIG'
# 每个单词的首字母大写
title = a.title()
print('1、',title)
# 所有字母大写
upper = a.upper()
print('2、',upper)
# 所有字母小写
lower = a.lower()
print('3、',lower)
# 字符串的第一个字符大写，注意不是第一个字母
capitalize = a.capitalize()
print('4、',capitalize)
# 所有字母大小写互换
swapcase = a.swapcase()
print('5、',swapcase)
```

```
1、 I Love You. Do You Know? Big
2、 I LOVE YOU. DO YOU KNOW? BIG
3、 i love you. do you know? big
4、 I love you. do you know? big
5、 I LOVE YOU. dO YOU KNOW? big
```

#### os.path和sys.path：

> os.path主要用于用户对系统路径的操作。
>
> sys.path主要用于python解释器的系统参数的操作。

#### 反转字符串：

```Python
a = 'dogg'
print(a[::-1])
print(''.join(reversed(a)))
```

```
ggod
ggod
```

#### is和==：

> is通过id判断；==通过value判断。

