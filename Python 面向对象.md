## Python 面向对象：

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

