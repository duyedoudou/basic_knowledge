## （未打印）python常用方法：

#### 查看内置函数：

 import math

 dir(math)

 help(math)

help(math.pi)

------

 使用man:例：man tar

使用工具自带的help。例：pip --help

使用man的替代品。安装`pip install tldr` 例：`tldr tar`

------

 安装`pip install httpie`  在命令行里请求网页内容 

常见的http请求头：从Accept开始。

![image-20190725165618824](/Users/mac/Library/Application Support/typora-user-images/image-20190725165618824.png)



全排列&组合：

```python
from itertools import permutations,combinations
c = [1,2,3,4]
lisss = list(permutations(c,2)) # 排列
lisss2 = list(combinations(c,2))# 组合 
print(lisss)
print(lisss2)
```

```
[(1, 2), (1, 3), (1, 4), (2, 1), (2, 3), (2, 4), (3, 1), (3, 2), (3, 4), (4, 1), (4, 2), (4, 3)]
[(1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4)]
```

斐波那契数列？

```python
def fib (num):
    numlist = [0,1]
    for i in range(num-2):
        numlist.append(numlist[-2]+numlist[-1])
    return numlist

```

