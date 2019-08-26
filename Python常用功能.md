### 常用功能：

```Python
# 把列表按空格输出
a = [1,2,3]
c = [str(i) for i in a]
print(c)
print(' '.join(c))
```

```
['1', '2', '3']
1 2 3
```

```python
# 输入存进二维列表
arr = []
for i in range(4):
    arr.append(list(map(int,input().split())))
print(arr)
```

```Python
1 2 3 4
2 3 4 2
2 1 3 4
1 5 4 6
[[1, 2, 3, 4], [2, 3, 4, 2], [2, 1, 3, 4], [1, 5, 4, 6]]
```

![image-20190826101002053](/Users/mac/Library/Application Support/typora-user-images/image-20190826101002053.png)