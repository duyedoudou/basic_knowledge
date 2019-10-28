## lambda函数：

#### 匿名函数：

除了作为参数传给高阶函数（如map）之外，Python很少使用lambda函数。

#### 一道关于lambda函数的经典面试题:

> list[0]能输出什么？这个主要考函数对象列表，千万不要和列表表达式搞混了啊

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

#### 题目：一行代码实现对列表a中的偶数位置的元素进行加3后求和？

```python 
a = [1,2,3,4,5]
sum(map(lambda y:y+3,filter(lambda x:a.index(x)%2==0,a)))
```

```
18
```

#### 题目：对字典按value、key值排序：

###### ！！sorted之后字典变成了元组构成的列表

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

再看个例子：

![image-20190807101532488](/Users/mac/Library/Application%20Support/typora-user-images/image-20190807101532488.png)

#### 