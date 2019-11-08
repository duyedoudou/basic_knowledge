## book_python3学习笔记

3:实际上，**所有的类型都是由type创造的，这个和继承无关**。

就类对象来说，他的本质就是存储字段成员和方法的特殊容器。

```python 
print(type(float))
print(isinstance(int,type))
```

```
<class 'type'>
True
```

#### 名字空间：

1：内置函数`globals()`和`locals()`分别返回全局名字空间和本地名字空间。

2：比如定义x = 100,那么名字空间就用字典来存储{x:100}，我通过名字（即x）访问目标对象（100），无非就是以名字为主键在字典里读取目标对象的指针引用。所以就有那么一句话：

```
Names have no type, but objects do.
```

那既然这么说，我就完全可以让x = ‘abc'

在Python中，10000是一个对象(我们不使用像100这样的小数字，因为Python会对先数字提前赋值缓存之类的，此处先不关心)，这个对象可以被x指向，也可以被y，z指向。也就是说，10000就像个瓶子，身上可以绑好多纸条，这里的纸条指的就是`名字`。

当x和y都指向10000这个对象的时候，我们又不能可视化的看到，那么怎么判断呢？一般使用is来判断。

```python 
x = 10000
y = 10000
print(x is y)  # 不是同一个"人"
print(x == y)  # 但是值相同
```

```
False
True
```

#### 命名规则：

使用keyword模块查看保留字

```Python
import keyword
print(keyword.kwlist)
```

```
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

```Python
# 查看某字是不是保留字
keyword.iskeyword('with')
```

看一个关于下划线的好玩的用法：

在交互式模式下，单下划线（_）返回最后一个表达式的结果。

------

2019.10.28

使用 `sys.getsizeof` 方法可以查看 python 对象的内存占用，单位：字节 (byte)
实际上是调用了 `__sizeof__` 方法：

```python 
import sys

a = 6
st = 'word'
print(sys.getsizeof(s))    
print(s.__sizeof__())
print(st.__sizeof__())
```

```
28
28
53
```

python可用下划线作为千分位的分隔符，但是不能用逗号

```Python
a = 34_342_321   # 使用下划线
print(a)
b = 34,321,34
print(b)         # 使用逗号，返回的是tuple 
```

```
34342321
(34, 321, 34)
```

python对于常用的小数字，解释器会在初始化时候进行预缓存，以提高性能，节省内存开销。3.6版本的预存范围是[-5,256]

```python 
# is是通过id来判断，==是通过value来判断

a = 5                # 预存范围内
b = 5
print(a is b)
print(id(a),id(b))
c = 300              # 超预存范围
d = 300
print(c is d)
print(id(c),id(d))

```

```
True
4396000608 4396000608
False
4431610832 4433545264
```

3.6新增了f-string支持，阅读体验上更加完整简洁

```Python
x = 10
y = 20
print('{}+{}={}'.format(x,y,x+y))
print(f'{x}+{y}={x+y}')            # 使用f-string，实现相同的效果
```

```
10+20=30
10+20=30
```

