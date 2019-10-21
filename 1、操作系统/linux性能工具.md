### linux性能工具：

2019.10.21

##### top命令：

![image-20191021154121067](/Users/mac/Library/Application Support/typora-user-images/image-20191021154121067.png)

```
查看pid为32468进程下的线程：
top -Hp 32468
```

![image-20191021154245963](/Users/mac/Library/Application Support/typora-user-images/image-20191021154245963.png)

下边来具体看看top：

![image-20191021154747743](/Users/mac/Library/Application Support/typora-user-images/image-20191021154747743.png)

圈出两个时间：系统时间和机器运行时间

后边的3个load，

3个load值是什么含义？分别代表的是1MIN,5MIN,15MIN机器的负载情况，如何确定负载的大小呢？需要和CPU的核数相结合来看，比如该机器是4核CPU，那么如果load值超过了4，就意味着负载很大了！【在top下按下1可以观察出CPU的个数】，关于系统负载，具体可以阅读前面文章[Linux中load average意义（请戳我）](https://mp.weixin.qq.com/s?__biz=MzIwNTc4NTEwOQ==&mid=2247484380&idx=1&sn=d57f761df6f2930739806040391f9da3&scene=21#wechat_redirect)。

![image-20191021155143453](/Users/mac/Library/Application Support/typora-user-images/image-20191021155143453.png)

**第二行**：表示多少个任务，重点应该关注僵尸状态的任务数。

**第三行**：主要是CPU的一些信息。

**US/SY**：说的就是用户进程和系统进程使用CPU的占比。

**NI**：即NICE，表示被调整过线程优先级的进程占比，这个比例正常不应该很大。

**ID**：表示空闲；WA表示资源等待的时间，比如在瞬时大流量下，服务打了很多日志的话，那么这个值就会飙高，因为这会很消耗资源的。

**HI**：硬中断，一般就是外设引起的，如果HI飙高的话，那么意味着外设在硬件层面出现了问题。SI表示软中断。

**ST**：即steel，如果该主机是虚拟的话会有这个ST信息，也即是该虚拟机从宿主机获取CPU的时间片的百分占比。



**第四、五行**：这里主要说2个概念性的东西：buffer 和 cache。

buffer主要是什么呢？应该是待处理的数据，主要是处理2个系统之间速度不匹配的问题。而cache，一般应该是结果数据的缓存，比如从DB加载一些信息供查询用。

SWAP分区，就是想利用硬盘的做一部分缓存，如果SWAP交换非常频繁的话，就是说内存不够用！



**列表说明**：PID  进程ID、USER 用户、PR 优先级、VIRT 虚拟内存、RES 驻留内存、SHR 共享内存

这里需要指出的是，RES表示的是该进程实际占用的内存，而并不是申请的内存大小。也就是说当前进程所占用的内存物理大小是   RES-SHR。