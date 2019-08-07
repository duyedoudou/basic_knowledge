# Django部署到远程服务器步骤记录

0、上传本地文件到服务器：

```
scp [本地文件目录]  [服务器用户名]@[服务器名]:/[服务器上文件路径]
例如：scp -r 文件目录  root@47.94.129.71:/home
```

1、重装系统后出现warning@@@@@的信息，解决：.ssh/known_hosts文件中**记录远程主机的公钥**，之前重装个系统，而保存的公钥还是未重装系统的系统公钥，在ssh链接的时候首先会验证公钥，如果公钥不对，那么就会报错，使用shh-keygen 命令`ssh-keygen -R 加IP地址`

2、pip3安装之后找不到在哪。原因是按照下边的操作，在/usr/bin文件夹下本来就是pip3，愣是给删掉了，软链接到一个不存在的pip3.6  所以一定要检查下自己的文件的实际情况。

```bash
cd /usr/bin
rm pip3
ln -s pip3.6 pip3
#重新登录可生效，然后就可以用pip3装库了
pip3 install --upgrade pip
```

解决是卸载pip3：`sudo apt-get remove python3-pip`

重新安装：`apt-get install python3-pip`

------

3、**第二天上午：**

然而我并不需要升级成python3.6

下面记录本次操作的流程：

使用 Nginx 和 Gunicorn 部署 Django 博客

在root权限下进行：

1、更新系统软件 ubuntu 升级软件：

```
apt-get update 更新源          # 最好来一下
apt-get upgrade 更新已安装的包  # 不是必须
```

2、安装必要的软件nginx、pip3、virtualenv

```
apt-get install nginx            # 装nginx
apt-get install python3-pip      # pip3
pip3 install virtualenv          # 虚拟环境
```



3、启动nginx

启动Nginx服务 Nginx 是用来处理静态文件请求的，包括图片、css、js 等存在服务器某个文件夹下的静态文件，而显示文章的详情信息由django处理。

```
service nginx start
```

此时在任意浏览器输入服务器的域名，就可以看到nginx在运行了。

4、新建虚拟环境env_site

```
root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite# virtualenv env_site
```

启动虚拟环境

```
root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite# source env_site/bin/activate
```

如何导出此TXT文件，在本地执行：

```
pip3 freeze > requirements.txt
```

虚拟环境下，在项目的文件夹中的txt文件，安装网站运行环境

```
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite/jdango_first# pip3 install -r djrequirements.txt 
```

5、==修改boke中==的settings.py文件，

```
vim settings.py 
```

为让Nginx处理静态文件，将项目所有的静态文件放入到文件夹static中。修改部分为：

```
DEBUG = False
```

```
ALLOWED_HOSTS = ['47.94.129.71','127.0.0.1']
```

```
STATIC_URL = '/static/'
# STATICFILES_DIRS = (
#     os.path.join(BASE_DIR,"STATIC"),
# )
# 加入下面的配置
STATIC_ROOT = os.path.join(BASE_DIR, 'static')  #STATIC_ROOT 指明了静态文件的收集目录
```



6、项目文件夹下，将项目中的静态文件收集到static文件夹下，以方便Nginx访问

```
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite/jdango_first# python3 manage.py collectstatic
```

7、配置Nginx：在服务器的/etc/nginx/sites-available/目录下新建一个配置文件demo_site

```
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:d# touch demo_site
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/etc/nginx/sites-available# vim demo_site 
```

文件内容为：

```
server {
    charset utf-8;
    listen 80;
    server_name 47.94.129.71;  #域名

    location /static {
        alias /home/mysite/jdango_first/static;   #静态文件目录
    }

    location / {
        proxy_set_header Host $host;
        proxy_pass http://unix:/tmp/47.94.129.71.socket;  # 域名
    }
}

```

然后把这个配置文件放入到启用网站列表中，被启用网站的目录在 /etc/nginx/sites-enabled/，从 sites-available/ 目录下发送了一个配置文件的快捷方式到 sites-enabled/ 目录。

```
ln -s /etc/nginx/sites-available/demo_site  /etc/nginx/sites-enabled/demo_site
```

另外我们还需要将启动`nginx`的用户改为`root`

打开`/etc/nginx/nginx.conf`文件，将第一行中`user`后面的用户改为`root`即可。

==重启nginx==

```
nginx -s reload     # 非常重要！！栽坑两天！！
```

8、使用 Gunicorn 来管理进程

安装 Gunicorn：

```
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/etc/nginx# pip install gunicorn
```

9、运行gunicorn

```
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite/jdango_first# gunicorn --bind unix:/tmp/47.94.129.71.socket  boke.wsgi:application
```

10、安装redis

```
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite# wget http://download.redis.io/releases/redis-3.2.6.tar.gz

(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite# tar xzf redis-3.2.6.tar.gz 
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite# cd redis-3.2.6/
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite/redis-3.2.6# make install
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite/redis-3.2.6# cd src
(env_site) root@iZ2ze1y6kf6efdv2i5q4egZ:/home/mysite/redis-3.2.6/src# ./redis-server # 启动
```

参考：

1.如何将Django项目部署到阿里云服务器上？ - 程序员向东的回答 - 知乎
https://www.zhihu.com/question/54982081/answer/656763472

2.https://github.com/783745660/BLOG_CMS