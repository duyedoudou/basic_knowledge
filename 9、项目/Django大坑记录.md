## Django大坑

1.定义数据库模型时候CharField（），缺少max_length

```python 
# 如
name = models.CharField(max_length = 100)
```

2.使用ForeignKey时候，1️⃣把Person加了引号，就变成普通字符串了；2️⃣on_delete不可省略

```
author = models.ForeignKey(Person,relatad_name = 'author',on_delete = CASCADE)
```

3.settings.py文件中，总会忘记在INSTALLED_APP里加入新建的app

4.最长见的错误，拼写错误，如忘了个s

#### 创建一个应用有哪些步骤：

1、创建app；并将app名字加入到setting的INSTALLED_APP

```Python
Python manage.py startapp blog  # blog是应用的名字
```

2、需要的话，要编写数据模型类，在models.py文件中。即Django的ORM的表现形式

3、数据迁移

> python manage.py makemigrations  这个命令是记录我们对models.py的所有改动，并且将这个改动迁移到migrations这个文件下`生成`一个文件例如：0001文件；但是这个命令并没有作用到数据库
>
> python manage.py migrate  这条命令的主要作用就是把这些改动作用到数据库，也就是`执行`migrations里面新改动的迁移文件更新数据库，比如创建数据表，或者增加字段属性

```
python manage.py makemigrations # 根据数据库模型建立数据库
python manage.py migrate        # 真正创建数据库
```

4、配置URL：

​	1）在项目url文件里加入app的url

```python 
urlpatterns = [
    path('blog/', include('blog.urls',namespace='blog')),
    ]
```

​	2)配置app的url.py

5、在view.py中写函数。

6、编写模板

#### Django5个核心技术

model、URL、view、template、form