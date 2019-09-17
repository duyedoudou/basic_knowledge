## Python进阶

slice

```Python
a = slice(5,8,2)
b = range(10)
print(list(b[a]))
print(a)
```

```
[5, 7]
slice(5, 8, 2)
```

列表生成式

```Python
color = ['black','red','white']
size = ['s','m','l']
tshirt = [(i,j) for i in color for j in size]
print(tshirt)
```

```
[('black', 's'), ('black', 'm'), ('black', 'l'), ('red', 's'), ('red', 'm'), ('red', 'l'), ('white', 's'), ('white', 'm'), ('white', 'l')]
```

元组：1.不可变列表  2.没有字段名的记录（关注他的数量和位置信息）

```python 
name,age,city = ('wang',12,'nanjing')
print(name,city,age)
```

```
wang nanjing 12
```

```Python
tem = ('wang',12,'nanjing')
name2,age2,city2 = tem   # 神奇吧，元组拆包
print(name2,age2,city2)
```

```
wang nanjing 12
```

用*运算符把可迭代对象拆开作为函数的参数

```Python
def func(x,y):
    return (x+y)

t = (2,5)
print(func(*t))    # 就是以前见到的*args，不知道有几个参数的情况
```

```
7
```

具名元组

```python 
from collections import namedtuple
city = namedtuple('City','name country population')  # 头
beijing = city('beijing','china','1000')             # 实例化 
print(beijing.name)                                  # 使用字段名
print(beijing[1])                                    # 使用位置

```

