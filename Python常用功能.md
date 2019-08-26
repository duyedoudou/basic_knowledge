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

