## 快速排序

```python
# 简单粗暴的快速排序
# 存在额外的开销存放左右，要多次遍历数组
def quicksort(array):  # 直接递归
    if len(array)<2:   # 递归出口
        return array
      
    pivot_index = 0
    pivot = array[pivot_index]
    left_arr = [i for i in array[1:] if i<=pivot]
    right_arr = [i for i in array[1:] if i>pivot]
    return quicksort(left_arr) + [pivot] + quicksort(right_arr)

  # 测试
import random
seq = [random.randint(1,100) for i in range(10)]
print(seq)
quicksort(seq)  
```

```python
# 改进，不产生多余的开销。-->在原数组上用左右指针
def partition(array,beg,end):     # pivot左边的都比pivot小，右边的都比pivot大
    pivot_index = beg
    pivot = array[pivot_index]
    left = pivot_index+1
    right = end
    
    while True:
        while left<=right and array[left]<=pivot:
            left += 1
        while left<=right and array[right]>pivot:
            right -=1
        if left>right:
            break
        else:
            array[left],array[right] = array[right],array[left]
            
    array[right],array[pivot_index] = array[pivot_index],array[right]
    return right                    # 返回pivot的下标
    
def quicksort_pro(array,beg,end):   # 改进后的快速排序
    if beg < end :
        pivot = partition(array,beg,end)
        quicksort_pro(array,beg,pivot)
        quicksort_pro(array,pivot+1,end)      
```

