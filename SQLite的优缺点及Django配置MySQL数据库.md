# SQLite的优缺点及Django配置MySQL数据库

> 内容：为什么Django项目中不建议使用自带的SQLite数据库及如何配置使用MySQL数据库

### 1、SQLite的应用场景及优缺点

SQLite数据库：轻量级、开源、免费。

它**只是一个.db格式的文件**，无需安装，配置和启动。

SQLite试图为单独的应用程序和设备提供本地的数据存储。

SQLite常见应用场景包括中小型网站，嵌入式设备和应用软件(如android)，文件档案管理和桌面程序(exe)文件数据库。

### 2、SQLite不适用以下场景:

- ##### 客户端/服务器程序

   如果你有许多的客户端程序要通过网络访问一个共享的数据库, 你应当考虑用一个客户端/服务器数据库来替代SQLite。

- ##### 高流量网站

  SQLite通常情况下用作一个中小型网站(日访问次数**少于10万)的后台数据库是完全可以胜任的**。

  网站的访问量大到采取分布式的数据库部署, 那么应当用一个企业级的客户端/服务器数据库来替代SQLite。

- ##### 超大的数据集

  当你在SQLite中开始一个事务处理的时候, 数据库引擎将不得不分配一小块内存(文件缓冲页面)来帮助它自己管理回滚操作。每1MB的数据库文件SQLite需要256字节。对于小型的数据库这些空间不算什么, 但是当数据库增长到数十亿字节的时候, 缓冲页面的尺寸就会相当的大了。如果你需要存储或修改几十GB的数据, 你应该考虑用其他的数据库引擎。

- ##### 高并发访问

  SQLite对于整个数据库文件进行读取/写入锁定， 这意味着如果任何进程<u>读取、写入</u>了数据库中的某一部分, 其他所有进程都不能再对该数据库的任何部分进行<u>写入、读取</u>操作。对于大多数情况这不算是什么问题， 在这些情况下每个程序使用数据库的时间都很短暂, 并且不会独占, 这样**锁定至多会存在十几毫秒**。

  但是如果有些程序需要高并发, 那么这些程序就需要寻找其他的解决方案了。

### 3、为什么使用MySQL

- 开发一个高流量或高并发的网站，SQLite将不能需求。

- 如果你要开发一个Web APP, 不同用户通过网络对数据库进行读写操作，那么SQLite也将不能胜任（比如分布式数据库)。

### 4、Django项目中如何配置使用MySQL

<u>刚开始可以不使用MySQL数据库，但一定要学会如何配置使用MySQL。</u>

Django项目中配置使用MySQL一共分四步: 

安装MySQL, 创建数据库名和用户名，通过pip安装第三方库pymysql和修改配置文件settings.py。

第一步 安装MySQL

```
sudo apt-get install mysql-server
```

第二步 创建数据库名和用户

> 打开MySQL终端，（mysql -u root -p）输入以下命令先创建数据库和用户，并给创建的用户授权。数据库名字，用户名和密码待会会用到。第一步和第二步非常重要。myapp.*表示授权操作myapp中所有的表。

```
CREATE DATABASE myapp charset=utf8; 
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON myapp.* TO 'username'@'localhost' IDENTIFIED BY 'password';
```

第三步 安装第三方库pymysql

需要借助于第三方库比如pymysql, Django才能直接访问MySQL数据库。进入虚拟环境(venv)后使用如下命令安装pymysql。

```
pip install pymysql
```

然后在项目文件夹的__init__.py中文件中写入如下两行代码：

```
import pymysql                                                                        
pymysql.install_as_MySQLdb()
```

第四步 修改数据库配置文件

> 修改项目文件夹里的settings.py的文件，添加创建的数据库和用户信息。

```python 
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',   # 数据库引擎
        'NAME': 'myapp',         # 你要存储数据的库名，事先要创建。
        'USER': 'root',         # 数据库用户名
        'PASSWORD': '123456',     # 密码
        'HOST': 'localhost',    # 默认主机
        'PORT': '3306',         # 数据库使用的端口
    }
}
```

创建一个简单模型，使用如下命令，如果没有出现错误，那么恭喜你已经在Django项目中使用MySQL数据库啦。

```
python manage.py makemigrations                               
python manage.py migrate
```

出现错误查看另一篇文档。