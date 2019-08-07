## Python内置heapq用法：

```python
import heapq #载入heap库，heap指的是最小堆
```
1、将数组转换成堆：heapq.heapify(list)

```python
lis = [1,3,4,2,6,8,9]
heapq.heapify(lis)
print(lis)

```

2、给堆增加元素，形成新堆：heapq.heappush(heap,item)

```python
heapq.heappush(lis,5)
print(lis)
```

3、删除堆顶（即最小值）：heapq.heappop(heap)

```python
heapq.heappop(lis)
print(lis)
```

4、删除最小值并添加新值，并形成新堆：heapq.heapreplace(heap, item)

```python
heapq.heapreplace(lis,33)
print(lis)
```

5、查堆中的最大的N个数：heapq.nlargest (n, heap)

```python
result = heapq.nlargest(2,lis)
print(result)
```

6、查堆中的最小的N个数：heapq.nsmallest(n, heap) #查询堆中的最小元素，n表示查询元素个数

```python
result = heapq.nsmallest(2,lis)
print(result)
```

7、合并几个有序数组为一个有序数组。（和堆没啥关系。。）heapq.merge(a,b)

```python
a = [1,2,3,4]
b = [6,8,9]
result = list(heapq.merge(a,b))
print(result)
```