## Python的垃圾回收：

> 内容提要：
>
> 1、介绍；2、循环引用垃圾回收；

#### 介绍下垃圾回收机制

引用计数为主，分代回收和标记为辅。

引用计数、分代回收（0，1，2这三代）（对象存在的时间越长，越不可能是垃圾）、标记回收（标记阶段、清除阶段）、孤立的引用环。

#### 关于循环引用垃圾回收的补充：

```Python
class X:
    def __del__(self):
        print(self,'dead.')
        
a = X()
b = X()
a.x = b
b.x = a

import gc             # 使用循环引用的垃圾回收
del a
del b
gc.enable()           # 开启
gc.collect()          # 主动启动回收操作，循环引用对象被正确回收
```

```
<__main__.X object at 0x1085246a0> dead.
<__main__.X object at 0x108524cc0> dead.
```

