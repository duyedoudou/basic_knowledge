分享一套阿里巴巴Python面试题。先看下阿里巴巴对Python工程师招聘岗位要求：

![img](https://mmbiz.qpic.cn/mmbiz_png/X36HLl2EicOd3IX5NGh3jhice1qr0DmftKJV2xFapic31ibFgXicjpjnTLo6UR6iaLbmrYwulOYvjrrhoQiciblEiawjU2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/X36HLl2EicOd3IX5NGh3jhice1qr0DmftKHSX0yXdHhEW6VRUJTVTRicKY14zuaPvSibDjTUhd9r0e4IialRDYkdoCA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

阿里巴巴Python工程师的真题

1、请尽可能列举python列表的成员方法，并给出列表操作的答案：

（1） a=[1, 2, 3, 4, 5], a[::2]=?, a[-2:] = ?

（2）一行代码实现对列表a中的偶数位置的元素进行加3后求和？

（3）将列表a的元素顺序打乱，再对a进行排序得到列表b，然后把a和b按元素顺序构造一个字典d。



2、用python实现统计一篇英文文章内每个单词的出现频率，并返回出现频率最高的前10个单词及其出现次数，并解答以下问题？（标点符号可忽略）

（1）创建文件对象f后，解释f的readlines和xreadlines方法的区别？

（2）追加需求：引号内元素需要算作一个单词，如何实现？

3、简述python GIL的概念， 以及它对python多线程的影响？编写一个多线程抓取网页的程序，并阐明多线程抓取程序是否可比单线程性能有提升，并解释原因。

4、用python编写一个线程安全的单例模式实现。

5、请回答一下问题：

（1）阐述一下装饰器，描述符（property）、元类的概念，并列举其应用场景；

（2）如何动态获取和设置对象的属性。

6、Python里面如何拷贝一个对象？（赋值，浅拷贝，深拷贝的区别）

答：赋值（=），就是创建了对象的一个新的引用，修改其中任意一个变量都会影响到另一个。

浅拷贝：创建一个新的对象，但它包含的是对原始对象中包含项的引用（如果用引用的方式修改其中一个对象，另外一个也会修改改变）{1,完全切片方法；2，工厂函数，如list()；3，copy模块的copy()函数}

深拷贝：创建一个新的对象，并且递归的复制它所包含的对象（修改其中一个，另外一个不会改变）{copy模块的deep.deepcopy()函数}

7、介绍一下except的用法和作用？

答：try…except…except…[else…][finally…]

执行try下的语句，如果引发异常，则执行过程会跳到except语句。对每个except分支顺序尝试执行，如果引发的异常与except中的异常组匹配，执行相应的语句。如果所有的except都不匹配，则异常会传递到下一个调用本代码的最高层try代码中。

try下的语句正常执行，则执行else块代码。如果发生异常，就不会执行

如果存在finally语句，最后总是会执行。



8、Python中pass语句的作用是什么？

答：pass语句不会执行任何操作，一般作为占位符或者创建占位程序，whileFalse:pass



9、介绍一下Python下range()函数的用法？

答：列出一组数据，经常用在for  in range()循环中



10、如何用Python来进行查询和替换一个文本字符串？

答：可以使用re模块中的sub()函数或者subn()函数来进行查询和替换，



格式：sub(replacement, string[,count=0])（replacement是被替换成的文本，string是需要被替换的文本，count是一个可选参数，指最大被替换的数量）

![img](https://mmbiz.qpic.cn/mmbiz_png/X36HLl2EicOd3IX5NGh3jhice1qr0DmftKNSmNevhk5J51maJqgm4TB5HSico9ibMzCiaVeMj1OyXMC3ZAicweZJxiavA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

subn()方法执行的效果跟sub()一样，不过它会返回一个二维数组，包括替换后的新的字符串和总共替换的数量



11、Python里面match()和search()的区别？

答：re模块中match(pattern,string[,flags]),检查string的开头是否与pattern匹配。

re模块中research(pattern,string[,flags]),在string搜索pattern的第一个匹配值。



![img](https://mmbiz.qpic.cn/mmbiz_png/X36HLl2EicOd3IX5NGh3jhice1qr0DmftKcG0jAdib6jVGN3TefRgQ9m0cbNQ7HRzOO1iapgWokibX6bJyxsCsoCiaNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1)



12、用Python匹配HTML tag的时候，<.*>和<.*?>有什么区别？

答：术语叫贪婪匹配( <.*> )和非贪婪匹配(<.*?> )

例如:

test

<.*> :

test

<.*?> :



13、Python里面如何生成随机数？

答：random模块

随机整数：random.randint(a,b)：返回随机整数x,a<=x<=b

random.randrange(start,stop,[,step])：返回一个范围在(start,stop,step)之间的随机整数，不包括结束值。

随机实数：random.random( ):返回0到1之间的浮点数

random.uniform(a,b):返回指定范围内的浮点数。



14、有没有一个工具可以帮助查找python的bug和进行静态的代码分析？

答：PyChecker是一个python代码的静态分析工具，它可以帮助查找python代码的bug, 会对代码的复杂度和格式提出警告；而Pylint是另外一个工具可以进行codingstandard检查



15、如何在一个function里面设置一个全局的变量？

答：解决方法是在function的开始插入一个global声明：

def f()

global x



16、单引号，双引号，三引号的区别

答：单引号和双引号是等效的，如果要换行，需要符号(\),三引号则可以直接换行，并且可以包含注释

如果要表示Let’s go 这个字符串

单引号：s4= ‘Let\’s go’

双引号：s5= “Let’s go”

s6 = ‘I realy like“python”!’

这就是单引号和双引号都可以表示字符串的原因了

