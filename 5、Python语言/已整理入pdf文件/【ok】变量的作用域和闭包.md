## 变量的作用域和闭包

#### 变量作用域：

先看个例子，吃上一惊。回头再解释。

```Python
b = 8
def f2(a):
    print(a)
    print(b)
    b = 9      # b在此处定义
f2(6)
```

```
6
UnboundLocalError: local variable 'b' referenced before assignment
```

报错看见没，上边有全局变量b啊，为啥还报错。（先说个没写出来的，如果b=9注释掉，结果是6  8）。

下面解释报错的原因：

> Python在编译函数的定义体时候，他判断b是局部变量，生成的`字节码`证实了这种判断，python会尝试从本地环境获取b,但是打印b时候b还没绑定值。所以就报错了。
>
> Python不要求声明局部变量，但是假定在函数体中的变量是局部变量。

LEGB:

#### 闭包：

```python 
def func():
    liss = []             
    def f(a):
        liss.append(a)           # 在函数f中，liss是自由变量，指没在本地作用域中绑定的变量
        total = sum(liss)
        return total/len(liss)
    return f

aa = func()
print(aa(2))                     # 调用函数func()
print(aa(8))
```

```
2.0
5.0
```

注意，在调用函数aa(2)时候，func()函数就已经返回了，他的本地作用域也拜拜了。

> 但是闭包会保留定义函数时候存在的自由变量的绑定，这样的话，在调用函数时，虽然func()的作用域拜拜了，但是仍然能使用那些绑定。

下边来看一个错误的例子：

```python 
def func():
    count = 0
    total = 0
    def f(a):
        count += 1
        total += a
        return total/count
    
aa = func()
aa(2)
```

```
报错:UnboundLocalError: local variable 'count' referenced before assignment
```

原因：首先count是不可变类型。count += 1的操作相当于在f的函数体中对count赋值了，**这就隐式的把count变成了局部变量，那就不是自由变量了**，就不能保存在闭包中了。total也是一样的。

##### 那怎么办呢？看注释。

```Python
def func():
    count = 0
    total = 0
    def f(a):
        nonlocal count,total        # 使用nonlocal声明成全局变量
        count += 1
        total += a
        return total/count
    return f
    
aa = func()
print(aa(2))
print(aa(8))
```

```
2.0
5.0
```

