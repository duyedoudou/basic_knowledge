## 冒泡排序：

```python
def buttle_sort(arr):
    for i in range(len(arr)): # 外循环，每循环一次使得有序的数增加一个
        indicator = False     # 设置指示器，没有交换时表示array已经有序，用于结束循环
        for j in range(len(arr)-1-i): # 内循环，每循环一次取出剩余数中的最大数
            if arr[j]>arr[j+1]:
                arr[j],arr[j+1] = arr[j+1],arr[j]
                indicator = True      # 标志放在if判断里
        if not indicator:             # 放在外循环里
            break
            
# 测试
import random             
arr= random.sample(range(100),10) # 从range(100)中随机取出10个数
print(arr)
buttle_sort(arr)
print(arr)
```

## 简单选择排序：

> 先标记最小下标。内循环中，如果发现有比这个标记的还小的，不着急交换，而是只做标记。循环结束后，都会标记得出最小的数，再做交换。

```python
def select_sort(arr):
    for i in range(len(arr)):         # 外循环，每循环一次，最前边的为从小到大有序数+1
        min_index = i                 # 标记最小值的下标
        for j in range(i+1,len(arr)): # 内循环,注意！range是前闭后开
            if arr[j]<arr[min_index]:
                min_index = j         # 把较小值得下标更改
        if min_index!=i:
            arr[i],arr[min_index]=arr[min_index],arr[i]    
```















## 直接插入排序：

> 先认为第一个数最小，然后来一个新数就和前边从小到大排序好的序列比较，从最后一个依次比较，插入到对应位置。

```python
def insert_sort(arr):
    for i in range(1,len(arr)): # 循环长度-1次
        index = i               # 记录元素插入的位置
        target = arr[i]         # 临时变量存储待插入元素
        while index>0 and target<arr[index-1]:
            arr[index] = arr[index-1]  # 前边的元素后移
            index=index-1              # 记录下标前移
        arr[index] = target            # while循环结束后，把缓存给到插入位置
```

## 希尔排序：

> 希尔排序的基本思想是：将数组列在一个表中并对列分别进行插入排序，重复这过程，不过每次用更长的列（步长更长了，列数更少了）来进行。最后整个表就只有一列了。将数组转换至表是为了更好地理解这算法，算法本身还是使用数组进行排序。

```python
def shell_insert(arr2,d):
    for i in range(d,len(arr2)):  # 子函数的循环次数是从间隔长度到最后
        index = i                 # 记录元素插入的位置
        target = arr[i]           # 临时变量存储待插入元素
        while index>0 and target<arr[index-d]:
            arr[index] = arr[index-d]  # 前边的变量后移
            index = index-d            # 坐标前移，看看对应的多整齐！
        if index!=i:                   # while循环结束后，如果记录坐标发生变化
            arr[index] = target        # 将元素插入index指示的位置
        
def shell_sort(arr):
    d = len(arr)//2       # d为间隔长度
    while d>=1:
        shell_insert(arr,d)
        d = d//2
```

