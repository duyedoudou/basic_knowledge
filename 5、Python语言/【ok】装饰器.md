## 装饰器：

> 内容提要：
>
> 1、什么是装饰器；2、装饰器实现单例模式；3、重新认识装饰器；4、functools.lru_cache装饰器；

#### 什么是装饰器：

装饰器的目的是在不改变原函数名的情况下改变被包装对象的行为。

产生原因：已有的程序已经上线，不能大批修改源码。

举例：原函数是小盒子。装饰器是大盒子。使用中盒子来对小盒子做扩展功能。

大盒子返回中盒子的函数名，不带括号。

中盒子的定义体里包括小盒子，还包括其他功能。

看个例子就明白了。

#### 使用装饰器实现单例模式：

```python 
def single01(cls):
    s = {}
    def wrap(*args,**kwargs):
        if 'j' not in s:
            s['j'] = cls(*args,**kwargs)
        return s['j']
    return wrap

@single01
class A():
    def __init__(self,name):
        self.name = name
        
a = A('du')
b = A('y')
print(a.name)
print(b.name)
```

```
du
du
```

#### 重新认识装饰器:

```python 
@decorate 
def target():
    print('hello')
    
# 上述代码的效果和下边的一样

def target():
    print('hello')
target = decorate(target)
```

> 装饰器有这么两个特点：1、把被装饰的函数替换成其他函数。2、**装饰器在加载模块时立即执行**。

关于第二点，看个例子：

```Python
registry = []
def register(func):                    # 定义装饰器
    print('我是装饰器，我在搞:%s'%func)
    registry.append(func)
    return func

@register                              # 装饰f1
def f1():
    print('我是f1')
  
@register                              # 装饰f2
def f2():
    print('我是f2')

def f3():                              # 没有装饰f3
    print('我是f3')
    
print('registry里有这些：',registry)
f1()
f2()
f3()

```

```
我是装饰器，我在搞:<function f1 at 0x1054fc510>
我是装饰器，我在搞:<function f2 at 0x1054fc2f0>
registry里有这些： [<function f1 at 0x1054fc510>, <function f2 at 0x1054fc2f0>]
我是f1
我是f2
我是f3
```

这个例子主要强调在加载模块时候立即执行，被装饰的函数（f1,f2,f3）只在明确调用时候才运行。

此处显示了`导入时`和`运行时`之间的区别。

#### functools.lru_cache装饰器：

```python 
%%time
import functools
@functools.lru_cache()        # 有一对括号，原因是lru_cache可接受配置参数
def fib(n):
    if n<2:
        return n
    return fib(n-2) + fib(n-1)

print(fib(30))
```

```
832040
CPU times: user 266 µs, sys: 110 µs, total: 376 µs
Wall time: 328 µs
```

对比：

```Python
%%time
# import functools
# @functools.lru_cache()        # 有一对括号，原因是lru_cache可接受配置参数
def fib(n):
    if n<2:
        return n
    return fib(n-2) + fib(n-1)

print(fib(30))
```

```
832040
CPU times: user 572 ms, sys: 14.2 ms, total: 586 ms
Wall time: 781 ms
```

看见时间差异没？使用functools.lru_cache() 装饰器时，性能明显改善，因为他实现了缓存技术。

那现在具体看下他的参数配置：

`functools.lru_cache(maxsize=128,typed=False)`

maxsize指存储多少个调用结果，存满后，旧的会被扔掉，maxsize应设为2的幂。

typed如果设为True，通常会把1和1.0区分开。

另外，lru_cache使用字典存储，字典的键是根据电泳时传入的参数创建，因此，被装饰的函数的参数都必须是可以散列的。

#### functools.singledispatch装饰器：

抽空看帖子