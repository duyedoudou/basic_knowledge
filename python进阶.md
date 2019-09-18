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

字典推导式

```python 
a = [('w',2),('do',3),('ss',4)]
b = {i:j for i,j in a}
print(b)
```

```
{'w': 2, 'do': 3, 'ss': 4}
```

一行代码实现对列表a中的偶数位置的元素进行加3后求和？

```python 
a = [1,2,3,4,5]
sum(map(lambda y:y+3,filter(lambda x:a.index(x)%2==0,a)))
```

```
18
```

将列表a的元素顺序打乱，再对a进行排序得到列表b，然后把a和b按元素顺序构造一个字典d。

```python 
import random
a = [1,2,3,4,5]
b = a[:]
random.shuffle(b)
print(a,b)
dict(zip(a,b))
```

```
[1, 2, 3, 4, 5] [3, 1, 5, 4, 2]
{1: 3, 2: 1, 3: 5, 4: 4, 5: 2}
```

用python实现统计一篇英文文章内每个单词的出现频率，并返回出现频率最高的前10个单词及其出现次数。

```Python
import re

with open('this.txt','r') as f:
    word_list = []
    word_dict = {}
    for line in f.readlines():
        for word in line.strip().split():
            word_list.append(re.sub('[,|.|!|*|-]','',word.lower()))
    word_set = list(set(word_list))
    word_dict = {word:word_list.count(word) for word in word_set}
result = sorted(word_dict.items(),key = lambda i:i[1], reverse=True)[:10]
print(len(result))
print(result)
```

```python 
import re
from collections import Counter

with open('this.txt','r') as f:
    text = f.read()
    count = Counter(re.split('\W+',text))

result = count.most_common(10)
print(result)
print(count)
```

