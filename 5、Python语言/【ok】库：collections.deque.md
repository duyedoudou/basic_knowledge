## 库：collections.deque

> 内容提要：
>
> 1、右加，左加；2、清空；3、统计数目；4、右扩展，左扩展；5、元素索引；6、插入元素；7、右弹出，左弹出，指定删除；8、队列反转；9、rotate

```python
from collections import deque

d = deque()
```

#### append（往右边添加一个元素）:

#### appendleft(往左边添加一个元素) ：

```python
d.append(1)
d.append(2)
d.appendleft(333)
```

#### 清空：

```
d.clear()
```

#### ✨count：返回指定元素的出现次数

```python
d.count(1)  # d中，1出现的次数
```

#### extend：从队列右边扩展一个列表的元素

```python
d.extend([2,3,5,7])
>>> d
>>> deque([1, 3, 4, 5])
```

#### extendleft：从队列左边扩展一个列表的元素

```python
d.clear()
d.append(1)
d.extend([2,3,5,7])
>>> d
>>> deque([7,5,3,2,1])
```





#### index：查找某个元素的索引位置

```python
>>> d
deque(['a', 'b', 'c', 'd', 'e'])
d.index("c",0,3) #指定查找区间,！前闭后开！
2
d.index("c",0,2)
ValueError: 'c' is not in deque
```

#### insert：在指定位置插入元素

```
>>> d
deque(['a', 'b', 'c', 'd', 'e'])
>>> d.insert(2,"z")
>>> d
deque(['a', 'b', 'z', 'c', 'd', 'e'])
```

#### pop（获取最右边一个元素，并在队列中删除）

#### popleft（获取最左边的一个元素，并在队列中删除）

#### remove：删除指定元素

```
>>> d
deque(['b', 'z', 'c', 'd'])
>>>
>>> d.remove("c")
>>> d
deque(['b', 'z', 'd'])
```

#### reverse：队列翻转

```
>>> d
deque(['a', 'b', 'c', 'd', 'c'])
>>> d.reverse()
>>> d
deque(['c', 'd', 'c', 'b', 'a'])
```

#### rotate：把右边元素放在左边

```
>>> d
deque(['c', 'd', 'c', 'b', 'a'])
>>> d.rotate(2)
>>> d
deque(['b', 'a', 'c', 'd', 'c']
```

