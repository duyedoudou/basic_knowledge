## Python 面向对象：

> 内容提要：
>
> 1、常见的类；2、类变量和实例变量对比；3、含有类变量；4、含有类方法；5、私有属性；6、私有属性的访问；7、普通继承；8、super继承；9、类中重构__repr__和__str__；10、\_\__new\_\__和\___init\_\__；11、\_\_call\_\_方法；
>
> 

#### 常见的类：

```python
class Student():
    def __init__(self,name,score):
        self.name = name
        self.score = score
    
    def show(self):
        info = '姓名:{},成绩:{}'.format(self.name,self.score)
        return info
                
a = Student('de',33)
print(a.name)
print(a.score)
print(a.show())        
```

```
de
33
姓名:de,成绩:33
```

#### 类变量和实例变量：

这个程序简单明了：

```python
class Student():
    age = 0
    name = 'stu'
    # age,name是类变量
    def __init__(self,age,name):
        self.age = age
        self.name = name
    # 访问实例变量(用self.age  self.name)

student1 = Student(18,'hello')
print(student1.name) 
# 打印实例变量，输出hello
print(Student.name)  
# 打印类变量，输出stu

```

#### 含类变量：（所有实例都可访问，即公共的）

```python 
class Student():
    number = 0                # 类变量
    def __init__(self,name,score):
        self.name = name
        self.score = score
        Student.number += 1   # 修改类变量：每有一次实例化，+1
    
    def show(self):
        print('姓名:{},成绩:{}'.format(self.name,self.score))
        
a = Student('de',33)
print(Student.number)         # 可通过Student访问
print(a.number)               # 也可通过实例访问，但是实例只能访问，不能修改
```



#### 含类方法：（所有实例都可访问，即公共的）借助@classmethod

```python 
class Student():
    number = 0
    def __init__(self,name,score):
        self.name = name
        self.score = score
        Student.number += 1
    
    def show(self):
        info = '姓名:{},成绩:{}'.format(self.name,self.score)
        return info
    
    @classmethod
    def total(cls):
        info = '创建了{}个实例。'.format(cls.number)
        return info
        
a = Student('de',33)
print(Student.total())          # 可通过Student访问
print(a.total())                # 也可通过实例访问

```

```
创建了1个实例。
创建了1个实例。
```

#### 私有属性：前边加上双下划线__。不能通过实例直接访问

```Python
class Student():
    def __init__(self,name,score):
        self.name = name
        self.__score = score    # 私有属性
    
    def show(self):
        info = '姓名:{},成绩:{}'.format(self.name,self.__score)
        return info
                
a = Student('de',33)
print(a.name)                   # OK
print(a.show())                 # OK
print(a.__score)                # 报错
```

```
de
姓名:de,成绩:33
AttributeError: 'Student' object has no attribute '__score'
```



#### 又想通过a.score访问私有属性：借助@property

```Python
class Student():
    def __init__(self,name,score):
        self.name = name
        self.__score = score
    
    def show(self):
        info = '姓名:{},成绩:{}'.format(self.name,self.__score)
        return info
# 新增    
    @property
    def score(self):
        info = self.__score
        return info 
                
a = Student('de',33)
print(a.name)
print(a.show())
print(a.score)                # 使用了这个装饰器，调用的时候就不用加括号了
        
```

```
de
姓名:de,成绩:33
33
```

#### 普通继承：

```python 
class Student():
    def __init__(self,name,score):
        self.name = name
        self.score = score
    
    def show(self):
        info = '姓名:{},成绩:{}'.format(self.name,self.score)
        return info
                   
class Dage(Student):
    def __init__(self,name,score,q_num):
        Student.__init__(self,name,score)     # 普通继承，使用Student.
        self.q_num = q_num
    def big_show(self):
        info = '{}考了{}分，有{}个枪。'.format(self.name,self.score,self.q_num)
        return info 
    
ming = Dage('m',55,2)
print(ming.big_show())
print(ming.show())
```

```
m考了55分，有2个枪。
姓名:m,成绩:55
```

#### super（）继承：

1、https://www.runoob.com/w3cnote/python-super-detail-intro.html

2、https://blog.csdn.net/lb786984530/article/details/81192721

3、https://blog.csdn.net/zsh142537/article/details/82685721

```python 
class Parent():
  pass
class Son1(Paernt):
  super().__init__()
class Son2(Paernt):
  super().__init__()

class Grendson(Son1,Son2):
  super().__init__()
  
d = Grendson()
# 简单记录调用顺序：mro顺序
Grendson开始调用-->Son1开始调用-->Son2开始调用-->Parent开始调用-->Parent结束调用
-->Son2结束调用-->Son1结束调用-->Grendson结束调用
```

 #### 类中重构__repr__和__str__的思考和理解：

```Python
# 1/使用print,不带别的，调用__str__方法
class Demo():
    def __repr__(self):
        return 'sd'
    def __str__(self):
        return 'sss'
    
a = Demo()
print(a)           # 使用print时候，调用重构的str方法
print(str(a))      # 这句和上句实现的一模一样功能
```

```
sss
sss
```

```python 
# 2/使用repr()，调用__repr__方法
class Demo():
    def __repr__(self):
        return 'sd'
    def __str__(self):
        return 'sss'
    
a = Demo()
print(repr(a))   # 这样和下边一行输出一样的东西，调用重构的str方法
a
```

```
sd
sd
```

```python 
# 3/str比较随和，如果没有__str__,就调用__repr__
class Demo():
    def __repr__(self):
        return 'sd'
#     def __str__(self):
#         return 'sss'
    
a = Demo()
print(a)
```

```
sd
```

```Python
# 如果没有__repr__,不会去找__str__,而是向上层object里找
class Demo():
#     def __repr__(self):
#         return 'sd'
    def __str__(self):
        return 'sss'
    
a = Demo()
print(repr(a))
```

```
<__main__.Demo object at 0x109b40898>
```

#### \_\__new\_\__和\___init\_\__

> \_\__new\_\__是在`生成对象之前`所做的动作，接收参数是cls，由python解释器自动提供。
>
> \_\__init\_\__是在`对象生成之后`完善对象的属性，接收参数是self。
>
> 所以，\_\__new\_\__里要有return，才能生成对象，有了对象，init才开始工作。
>
> 绝大部分是不需要重写new的。

应用：new实现单例。只生成一个实例化对象。

```Python
class Singleton:
    instance = None 
    def __new__(cls, xx, yy):
        if cls.instance is None:
            cls.instance = super().__new__(cls)
        return cls.instance 
    def __init__(self, xx, yy):
        self.xx = xx
        self.yy = yy
 
obj1 = Singleton(1, 2)
obj2 = Singleton(2, 1)
print(obj1.xx, obj2.xx)
print(obj1 is obj2)
```

```
2 2
True
```

#### 类中定义\_\_call\_\_方法，实现将类的实例化作为函数使用

> 类中如果定义了\_\_call\_\_方法，那么他的实例可以作为函数调用。

```Python
import random
class Bingocage:
    def __init__(self,item):
        self._item = list(item)  # 构建副本
        random.shuffle(self._item)
        
    def pick(self):
        return self._item
    
    def __call__(self):      # 定义__call__
        return self.pick()
    

bingo = Bingocage([1,2,3,4])
print(bingo.pick())           # 正常操作
print(bingo())                # 作为函数调用，即可以运用()运算符

print(callable(bingo))        # 判断是否可调用
```

```
[4, 2, 3, 1]
[4, 2, 3, 1]
True
```

#### 