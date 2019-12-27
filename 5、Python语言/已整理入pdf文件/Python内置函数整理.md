## Python内置函数整理

68个内置函数

> #### **分类记忆**
>
> - 数学运算 × 7
>
>   abs() 、 divmod() 、 max() 、 min() 、pow() 、round() 、sum()
>
> - 类型转换 × 24
>
>   bool() 、 int() 、 float() 、 complex() 、str() 、 ord() 、 chr() 、 bytearray() 、 bytes() 、 memoryview() 、 bin() 、 oct() 、 hex() 、 tuple() 、 list() 、 dict() 、 set() 、 frozenset()、 enumerate() 、 range() 、 iter() 、 slice() 、super() 、object()
>
> - 序列操作 × 8
>
>   all() 、any() 、 filter() 、 map() 、next() 、reversed() 、sorted() 、zip()
>
> - 对象操作 × 9
>
>   help() 、dir() 、 id() 、hash() 、type() 、len() 、ascii() 、format() 、vars()
>
> - 反射操作 × 8
>
>   Import() 、isinstance() 、issubclass() 、hasattr() 、getattr() 、setattr() 、delattr() 、callable()
>
> - 变量操作 × 2
>
>   globals() 、locals()
>
> - 交互操作 × 2
>
>   print()、input()
>
> - 文件操作 × 1
>
>   open()
>
> - 编译执行 × 4
>
>   compile() 、eval() 、exec() 、repr()
>
> - 装饰器 × 3
>
>   property() 、 classmethod() 、staticmethod()









##### 1、abs()  返回绝对值

```python 
abs(-30.4)
```

```
30.4
```

##### 2、all()  所有元素都为真返回true，否则返回false

```Python
print(all([30,'d',0]))  # 含有非true元素
print(all(['dog',88]))
```

```
False
True
```

##### 3、any()  

```python
print(any([30,'d',0]))  # 含有true元素
print(any([0]))         # 没有元素为真
print(any([]))          # 迭代器为空
```

```
True
False
False
```

##### 4、bin() 将一个整数转变为一个前缀为“0b”的二进制字符串

```python 
bin(5)
```

```
'0b101'   # 字符串
```

##### 5、chr()  

```python 
chr(97)  
```

```
'a'    # 97对应字母a
```

##### 6、ord()

```python 
ord('a')
```

```
97
```



##### 7、dict()  生成字典

```Python
dict(a=2,b=3)   # 注意！a,b没有引号
```

```
{'a': 2, 'b': 3}
```

##### 8、dir()  返回一个列表，包含对象的所有属性

```python 
dir(int)
```

```
['__abs__',
 '__add__',
 '__and__',
 '__bool__',
 '__ceil__',
 '__class__',
 '__delattr__',
 '__dir__',
...
]
```

##### 9、divmod()   返回商和余数

```Python
divmod(11,5)   # 11除以5
```

```
(2, 1)
```

##### 10、eval()  执行所给定的字符串表达式，并且返回表达式的值

```python
eval('2*4')
```

```
8
```

##### 11、hex()   返回整数对应的16进制

```Python
hex(13)
```

```
'0xd'
```

##### 11.2、oct()   返回整数对应的8进制

```python 
oct(8)
```

```
'0o10'
```

##### 12、id()   返回对象的内存地址

##### 13、list()   传入的参数创建新的列表

```Python
list('3456')
```

```
['3', '4', '5', '6']
```

##### 14、pow()   幂运算

```Python
pow(2,4)   # 2的4次方
```

```
16
```

15、