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

------

中间件是Django的核心。

优势：数据库访问、业务逻辑、模板显示等层面的松耦合和各自的灵活性。

html文件分成头、尾、中间体。

写视图函数前先画逻辑图。

Django内置有用户认证和管理应用。

客户端通过url向服务器发出请求时候，Django回创建一个HttpRequest对象，request就是HttpRequest的替代。

Django内置了CSRF中间件。

csrf攻击：攻击者盗用了用户的身份，以用户的名义发送恶意请求。

刚开始改前端代码时候，经常抄错字母，比如col-md-5,写成col-mn等。

使用了内置的登录和退出。内置的修改密码。内置重置密码。

何时使用功能modelForm类？p65

默认情况下，Django会为每个数据模型类设置一个自增的id字段，并将其作为数据库的主键。

单击用户名，使用了bootstrap提供的下拉菜单。p78

忘记密码找回是不可能的。

Django使用PBKDF2加密算法。

在显示文章时候，想在url里显示文章标题，使用了库：awesome-slugify。将汉字转换成拼音。

如果两个对象之间建立了一对多或者多对多的关联关系，那么就可以使用add（）方法增加属性的值，从容建立两个对象的关系。