#### 数组：

> 1、数组中重复的数字，输出第一个重复的数。

思路1：先排序，在从头遍历，当前数和后一个数相同，则返回。

思路2：定义一个新的空列表，从头遍历原数组，当前元素在空列表中，则返回。

思路3：from collections import Counter 

```python
#方法三：使用counter函数统计元素出现的次数
# number:原数组
duplication: 存放重复的数
import collections
class Solution:
    def duplicate(self, numbers, duplication):
        flag = False
        c = collections.Counter(numbers)        
        for k,v in c.items():
            if v >1:
                duplication[0] = k
                flag = True
                break
        return flag
```

```python
c = collections.Counter([1,2,3,2,1,4,3,2])
print(c,type(c))

>>>Counter({2: 3, 1: 2, 3: 2, 4: 1}) <class 'collections.Counter'>
```

> 2、在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

思路1：遍历二维数组，不推荐。

思路2 ：根据二维数组的特点，从`右上角`开始遍历。右上角是该行最大，该列最小。

​			  如果比要查找的数字大，就抛弃这一列；如果比要查找的数字小，就抛弃这一行。













> 3、顺时针循环打印二维数组    
>
> 逆时针旋转90度  ：list(zip(*matrix))[::-1]

```python
# 使用循环更容易理解
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        tem = []
        while matrix:                     # 循环条件：矩阵不为空
            tem.extend(matrix.pop(0))     # 使用extend而不是append
            matrix = list(zip(*matrix))[::-1]   # !!90度逆时针旋转剩下的矩阵元素
            # self.spiralOrder(matrix)
        return tem

```

> 4、逆时针打印二维数组    没啥意思

```Python
# 逆时针打印
sss = [[1,2,3],[4,5,6],[7,8,9]]
def spiralOrder(matrix):
    """
    :type matrix: List[List[int]]
    :rtype: List[int]
    """
    tem = []
    matrix = list(zip(*matrix))[::-1]
    tem.extend(matrix.pop(-1))
    while matrix:
        matrix = list(zip(*matrix[::-1]))
        tem.extend(matrix.pop(-1))
    return tem
spiralOrder(sss)
```

