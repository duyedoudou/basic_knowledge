## Python多进程与多线程

> 内容提要：1.1、进程和线程的概念；1.2、多进程和多线程的区别；2、协程介绍及形象类比；3、多进程；4、进程池；5.1、进程的通信方式；5.2、队列实现进程间通信；6、多线程；7、进程和现成的效率和选择讨论

#### 进程和线程概念：

进程是`资源分配`的最小单元，`独立内存`；线程是`操作系统调度`的最小单元，`共享内存`。

#### 多线程和多进程的区别：

在单个程序中同时运行多个线程完成不同的工作，称为多线程；共享内存空间；同一个进程的线程之间可以直接交流。

多进程优点：稳定，一个子进程崩溃不会影响到其他子进程；

缺点：创建代价大，因为操作系统要给每个进程分配固定的资源。

多线程优点：效率高。

缺点：但是任何一个线程崩溃都可能造成整个进程的崩溃，因为多线程共享内存资源池。

CPU密集型使用多进程。IO密集型使用多线程。

#### 单进程执行2次：

```python
import time
import os


def long_time_task():
    print('当前进程: {}'.format(os.getpid()))   # 获取进程号
    time.sleep(2)
    print("结果: {}".format(8 ** 20))


if __name__ == "__main__":
    print('当前母进程: {}'.format(os.getpid()))
    start = time.time()
    for i in range(2):
        long_time_task()
    end = time.time()
    print("用时{}秒".format((end - start)))

```

```
当前母进程: 15662
当前进程: 15662
结果: 1152921504606846976
当前进程: 15662
结果: 1152921504606846976
用时4.00621485710144秒
```

#### 介绍下协程，为何比线程还快：

如果一个线程等待某些条件，可以充分利用这个时间去做其它事情，其实这就是：协程方式。

协程创建的开销与线程相比完全可以忽略，这意味着，使用多协程可以处理更多的任务。原因是协程能保留上一次调用的状态。

拓展：

如果某个员工在上班时临时没事或者再等待某些条件（比如等待另一个工人生产完谋道工序 之后他才能再次工作） ，那么这个员工就利用这个时间去做其它的事情，那么也就是说：如果一个线程等待某些条件，可以充分利用这个时间去做其它事情，其实这就是：协程方式



#### Python多进程：multiprocessing模块的Process

> 注释：实际运行中包含了1个母进程和2个子进程

```Python
from multiprocessing import Process
import os
import time


def long_time_task(i):
    print('子进程: {} - 任务{}'.format(os.getpid(), i))
    time.sleep(2)
    print("结果: {}".format(8 ** 20))


if __name__ == '__main__':
    print('当前母进程: {}'.format(os.getpid()))
    start = time.time()
    p1 = Process(target=long_time_task, args=(1, ))   # 两个参数：函数名和向函数传的参数
    p2 = Process(target=long_time_task, args=(2, ))
    print('等待所有子进程完成。')
    p1.start()                                        # 启动进程
    p2.start()
    p1.join()                                         # 阻塞母进程，等待子进程结束
    p2.join() 
    end = time.time()
    print("总共用时{}秒".format((end - start)))

```

```
当前母进程: 15662
等待所有子进程完成。
子进程: 18152 - 任务1
子进程: 18153 - 任务2
结果: 1152921504606846976
结果: 1152921504606846976
总共用时2.0279181003570557秒
```



#### Python多进程：multiprocessing模块的Pool

```Python
from multiprocessing import Pool, cpu_count
import os
import time


def long_time_task(i):
    print('子进程: {} - 任务{}'.format(os.getpid(), i))
    time.sleep(2)
    print("结果: {}".format(8 ** 20))


if __name__ == '__main__':
    print("CPU内核数:{}".format(cpu_count()))   # 打印cpu的核数
    print('当前母进程: {}'.format(os.getpid()))
    start = time.time()
    p = Pool(4)                     # 开启容量为4的进程池
    for i in range(5):
        p.apply_async(long_time_task, args=(i, ))
    print('等待所有子进程完成。')
    p.close()                       # 关闭进程池，使不在接受新的任务
    p.join()                        # 阻塞主进程，join()要用在close()或者terminate()之后
    end = time.time()
    print("总共用时{}秒".format((end - start)))

```

```
CPU内核数:4
当前母进程: 15662
子进程: 18181 - 任务0
子进程: 18183 - 任务2
子进程: 18182 - 任务1
子进程: 18184 - 任务3
等待所有子进程完成。
结果: 1152921504606846976
结果: 1152921504606846976
结果: 1152921504606846976
子进程: 18183 - 任务4
结果: 1152921504606846976
结果: 1152921504606846976
总共用时4.12725305557251秒
```

#### 进程通信的方式：

管道、消息队列、共享内存（不同虚拟地址和同一物理地址的映射）、信号量。

#### 使用队列实现进程间通信：Queue

```Python
from multiprocessing import Process, Queue
import os, time, random


def write(q):       # 写数据进程
    print('Process to write: {}'.format(os.getpid()))
    for value in ['A', 'B', 'C']:
        print('Put %s to queue...' % value)
        q.put(value)
        time.sleep(random.random())

def read(q):        # 读数据进程
    print('Process to read:{}'.format(os.getpid()))
    while True:
        value = q.get(True)
        print('Get %s from queue.' % value)
        
        
if __name__=='__main__':
    q = Queue()     # 父进程创建Queue，并传给各个子进程
    pw = Process(target=write, args=(q,))
    pr = Process(target=read, args=(q,))
    pw.start()
    pr.start()
    pw.join()       # 等待pw结束
    pr.terminate()  # pr进程里是死循环，无法等待其结束，只能强行终止

```

```
Process to write: 18479
Put A to queue...
Process to read:18480
Get A from queue.
Put B to queue...
Get B from queue.
Put C to queue...
Get C from queue.
```

## Python多线程

#### threading模块的Thread：

> 可以看到也是只用了2.几秒，GIL锁没有锁子线程么？
>
> 有的。但是睡眠时候，并没有占用cpu，就释放GIL锁了。

```Python
from threading import Thread,current_thread
import os
import time


def long_time_task(i):
    print('子进程: {} - 任务{}'.format(current_thread().name,i)) # 打印主线程的名字
    time.sleep(2)
    print("结果: {}".format(8 ** 20))


if __name__ == '__main__':
    print('当前主线程: {}'.format(current_thread().name))
    start = time.time()
    t1 = Thread(target=long_time_task, args=(1, ))   # 两个参数：函数名和向函数传的参数
    t2 = Thread(target=long_time_task, args=(2, ))
    print('等待所有子进程完成。')
    t1.start()                                        # 启动进程
    t2.start()
    t1.join()                                         # 阻塞母进程，等待子进程结束
    t2.join() 
    end = time.time()
    print("总共用时{}秒".format((end - start)))
    
```

```
当前主线程: MainThread
等待所有子进程完成。
子进程: Thread-14 - 任务1
子进程: Thread-15 - 任务2
结果: 1152921504606846976结果: 1152921504606846976

总共用时2.0085318088531494秒
```

#### 多进程和多线程的效率问题：

- 对CPU密集型（如循环）                  —>多进程效率更高
- 对IO密集型（如文件操作、爬虫）  —>多线程效率更高

因为对于IO密集型，大部分时间是花在等待，等待时间是不占用CPU的，Python遇到等待会释放GIL供新的线程使用，实现了线程的切换。