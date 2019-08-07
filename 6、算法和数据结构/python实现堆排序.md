## 堆排序：

DY 2019.7.23

```python
#堆排序
def heap_sort(arr):
    root = len(arr)//2-1
    while(root>=0):
        heap_adjust(arr,root,len(arr)-1)    
        root=root-1   # 此时生成的大顶堆，满足每个根节点为子树中最大，因此，之后只需要对最顶的子树进行调整
        
    i = len(arr)-1
    while i>=0:
        arr[0],arr[i] = arr[i],arr[0]
        heap_adjust(arr,0,i-1)
        i=i-1
        
def heap_adjust(arr,start,end):
    temp=arr[start]       # 临时变量存储‘顶’位置的数据，temp不发生变化
    son=2*start+1         # son记录‘顶’的左节点的下标
    while son<=end:      # 循环条件耐琢磨，先往下看
        if son<end and arr[son]<arr[son+1]:  # 找出左右节点中较大的，
                                             # son<end,是为了保证此三角形有右节点
            son+=1                           # son指向较大那个位置
        if temp>=arr[son]:       # 第一轮判断是否为大顶堆，第二轮比较临时变量和下层的son的值得大小
            break                # 如果是大顶，直接退出while循环
        arr[start]=arr[son]      # 较大的左/右节点的值给‘顶’的位置，注意，此时该节点的值没有和‘顶’交换
        start=son                # ‘顶’的坐标指向下层的son
        son=2*son+1
    arr[start]=temp             # 将temp存储的原‘顶’的值，赋给start指向的位置，即最后的son的位置。
```

heap_adjust()函数的功能是将完全二叉树中，以start为根节点的子树进行构造大顶堆，**同时保证该子树的子树也是大顶堆。**这句话比较拗口。

举例：此时start为最顶端，元素为30，且不是最大值，那么在元素30下沉的过程中，会保证30下沉到合适位置，可能进行多次下沉，而不是只进行一次下沉。

heap_sort()函数中，有root = len(arr)//2-1，此位置是树中最后一个非叶子节点。

函数有两个循环，第一个循环是从最后一个非叶子节点一直往前作为堆顶。最后将序列构造成大顶堆。

> 原理是：从下往上，从右往左，将每个非叶子节点当做根节点，将其和其子树调整成大顶堆。

第二个循环是逐步将每个顶与末尾元素交换，并且再调整成大顶堆。