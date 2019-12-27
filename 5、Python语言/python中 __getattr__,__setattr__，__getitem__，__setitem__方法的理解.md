#### python中 `__getattr__`,`__setattr__`，`__getitem__`，`__setitem__`方法的理解

`__getattr__(self,item)`：使用.访问对象属性时候，如果对象没有这个属性，就会调用这个方法。那么反过来，如果对象有这个属性，如fjs.name = "fjs"，在访问时候，就不会调用`__getattr__(self,item)`这个方法。

`__setattr__(self,item,value)`：当试图对对象进行赋值（使用.赋值）时候调用。

`__getitem__(self,item)`：使用`[]访问`对象属性时候，调用。

`__setitem__(self,item,value)`：对对象进行赋值（使用`[]赋值`）时候调用。

下面看个例子：

```python 
class Student():
    def __getattr__(self,item):
        return '{}不存在'.format(item)
    def __setattr__(self,item,value):
        self.__dict__[item] = value
        
    def __getitem__(self,item):
        return self.__dict__[item]+'dou'
    
    def __setitem__(self,item,value):
        self.__dict__[item] = value
        
s = Student()
print(s.name)      # 调用__getattr__方法 输出'name is not exits'
s.age = '1'        # 调用__setattr__ 方法
print(s.age)       # 输出 1
print(s['age'])    # 调用 __getitem__方法 输出1dou

s['name'] = 'tom'  # 调用 __setitem__ 方法
print(s.name)      # 输出name的值
print(s['name'])   # 调用 __getitem__ 方法 输出 'tomdou'

```

```
name不存在
1
1 dou
tom
tom dou
```

