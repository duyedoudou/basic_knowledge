## redis

https://blog.csdn.net/chenyao1994/article/details/79491337

#### 什么是Redis：

Redis是一个开源的`内存中`的数据结构存储系统，它可以用作：**数据库、缓存和消息中间件**。

#### Redis常见的数据结构类型有哪些：

常见的数据结构类型有：String、List、Set、Hash、ZSet这5种。

#### Redis是如何进行持久化的：

Redis也提供了持久化的选项，这些选项可以让用户将自己的数据保存到磁盘上面进行存储。根据实际情况，可以每隔一定时间将数据集导出到磁盘（快照），或者追加到命令日志中（AOF只追加文件），他会在执行写命令时，将被执行的写命令复制到硬盘里面。

也可以关闭持久化功能，将Redis作为一个高效的网络的缓存数据功能使用。

#### redis为什么这么快：

Redis不使用表，他的数据库不会预定义或者强制去要求用户对Redis存储的不同数据进行关联。

数据库的工作模式按存储方式可分为：硬盘数据库和内存数据库。

Redis 将数据储存在`内存`里面，读写数据的时候都`不会受到硬盘 I/O 速度的限制`，所以速度极快。

![image-20190909162902301](/Users/mac/Library/Application Support/typora-user-images/image-20190909162902301.png)

![image-20190909162925428](/Users/mac/Library/Application Support/typora-user-images/image-20190909162925428.png)

#### 为什么用单线程：

CPU不是Redis的瓶颈，Redis的瓶颈最有可能是机器内存的大小或者网络带宽。

单线程容易实现，而且CPU不会成为瓶颈，那就顺理成章地采用单线程。