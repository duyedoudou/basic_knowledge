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

