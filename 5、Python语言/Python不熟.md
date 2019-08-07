### Python不熟

1、hasattr()函数    `判断对象是否包含对应的属性`      如果对象有该属性返回 True，否则返回 False。

语法：hasattr(object, name)     参数：object -- 对象；name -- 字符串，属性名。

```python
class Coor():
    x = 12
    y = 13
    z = 0 
c = Coor()
print(hasattr(c,'x'))
print(hasattr(c,'bb'))
```

```
True
False
```

2、倒叙生成列表。（使用-1步长）

```python
a = list(range(5))      # 生成5个数（自然顺序）
print(a)
b = list(range(1,5,2))  # 从1到4（因为前闭后开），步长为2
print(b)
c = list(range(5,1,-1)) # 从5到2（因为前闭后开），步长为-1，即每次+负1
print(c)
```

```
[0, 1, 2, 3, 4]
[1, 3]
[5, 4, 3, 2]
```

3、全排列&组合：

```python
from itertools import permutations,combinations
c = [1,2,3]
lisss = list(permutations(c,2)) # 排列
lisss2 = list(combinations(c,2))# 组合 
print(lisss)
print(lisss2)
```

```
[(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]
[(1, 2), (1, 3), (2, 3)]
```



3、函数带有默认参数，默认参数只创建一次

解释：lis1和lis3均使用默认lis[]，故指向相同；而lis2使用自己创建的[]。

![image-20190807102133505](/Users/mac/Library/Application Support/typora-user-images/image-20190807102133505.png)

4、对字典排序后，输出的是元组组成的列表

![image-20190807101532488](/Users/mac/Library/Application%20Support/typora-user-images/image-20190807101532488.png)

