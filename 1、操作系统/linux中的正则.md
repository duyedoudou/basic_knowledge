### linux中的正则：

2019.10.21

#### 一：与位置匹配有关的：

这是实例使用的文件。

```txt
guo jing
huang rong dadaguo
guo huangrong
da xia guo jing

guo
tian xia wu di 
liu guoda
```

##### 1、找出行首是guo的行：使用 ^

```
cat regular.txt grep | --color "^guo"
```

```
guo jing
guo huangrong
guo
```

##### 2、找出行尾是guo的行：用$

```
cat regular.txt | grep --color "guo$"
```

```
huang rong guo
guo
```

刚才找的是行，现在找词首：

##### 3、找到词首为guo的行：用(看下边)

```
用 \< 或者 \b
cat regular.txt | grep --color "\<guo"
或者
cat regular.txt | grep --color "\bguo"
```

```
guo jing
guo huangrong
da xia guo jing
guo
liu guoda
```

##### 4、找到词尾为guo的行

```
用\>  或者  \b   没错，\b通吃！
cat regular.txt | grep --color "guo\>"
```

```
guo jing
huang rong dadaguo
guo huangrong
da xia guo jing
guo
```

现在给示例文件增加一行：doudouguodoudou

##### 5、\B表示什么意思呢？

答：和\b取反的意思。

```
cat regular.txt |grep --color "guo\B"
表示含有guo，但是guo不在词尾
```

```
liu guoda
doudouguodoudou
```

```
cat regular.txt |grep --color "\Bguo"
表示含有guo，但是guo不在词首
```

```
huang rong dadaguo
doudouguodoudou
```

##### 6、取出空行：

```
cat regular.txt |grep --color "^$"
```

##### 7、取出只含有guo的那行，即完全匹配。

```
cat regular.txt | grep --color "^guo$"
```

#### 二：与匹配次数有关的：

这是使用的例子。

```
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_1.txt 
x       y    1
xax     y    2
xaax    y    3
xaaax   y    4
xaaaax  y    5
xaaaaax y    6
```

##### 1、找到连续2个a的行：

```
cat regular_1.txt | grep --color "a\{2\}"    最后的两个斜杆是转义符
```

```
xaax    y    3
xaaax   y    4
xaaaax  y    5     // 这行的aa实际是被匹配了两次
xaaaaax y    6
```

![image-20191021124508104](/Users/mac/Library/Application Support/typora-user-images/image-20191021124508104.png)

（看红色的）

##### 2、找到至少有2个a的行：带个逗号

```
cat regular_1.txt | grep --color "a\{2,\}"
```

```
xaax    y    3
xaaax   y    4
xaaaax  y    5
xaaaaax y    6
```

![image-20191021124756735](/Users/mac/Library/Application Support/typora-user-images/image-20191021124756735.png)

（看红色的）

##### 3、找到至少有2个a，至多3个a的行：

```
cat regular_1.txt | grep --color "a\{2,3\}"
```

```
xaax    y    3
xaaax   y    4
xaaaax  y    5
xaaaaax y    6
```

![image-20191021125207410](/Users/mac/Library/Application Support/typora-user-images/image-20191021125207410.png)

##### 4、*号表示匹配任意次，即0次或多次：

```
cat regular_1.txt | grep --color "a*"
```

```
全部匹配
x       y    1
xax     y    2
xaax    y    3
xaaax   y    4
xaaaax  y    5
xaaaaax y    6
```

##### 5、匹配0次或1次的：用\?

```
cat regular_1.txt | grep --color "a\?"
```

```
全部匹配,尽管和上个结果一样，但是匹配原理不一样
x       y    1
xax     y    2
xaax    y    3
xaaax   y    4
xaaaax  y    5
xaaaaax y    6
```

##### 6、那我不要匹配0次的，只要匹配1次或多次

```
使用\+
cat regular_1.txt | grep --color "a\+"
```

```
xax     y    2
xaax    y    3
xaaax   y    4
xaaaax  y    5
xaaaaax y    6
```

#### 三：其他常用符号：

使用的例子。

```
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_2.txt
a1bb hua
asd f
a^3de
a funny
aSD cat
a345 dogs
acc fukf
```

##### 1、[[::]]系列：

|             |                              |
| ----------- | ---------------------------- |
| [[:lower:]] | 匹配任意小写字母             |
| [[:upper:]] | 匹配任意大写字母             |
| [[:alpha:]] | 匹配任意大写和小写字母       |
| [[:digit:]] | 匹配任意数字                 |
| [[:alnum:]] | 匹配任意数字或大写或小写字母 |
| [[:space:]] | 匹配空格，如tab              |
| [[:punct:]] | 匹配标点符号                 |


```
找到a后边是小写字母的行
cat regular_2.txt | grep -n --color "a[[:lower:]]"  // -n表示打印行号
```

```
2:asd f
5:aSD cat
7:acc fukf
```

![image-20191021130927416](/Users/mac/Library/Application Support/typora-user-images/image-20191021130927416.png)

##### 2、[]

```
找到a后边是1或者s或者c的行
cat regular_2.txt | grep -n --color "a[1sc]"
```

```
1:a1bb hua
2:asd f
7:acc fukf
```

##### 3、^放在[]里表示：非

```
找到a后边不是字母的行(大小写都不要)
cat regular_2.txt | grep -n --color "a[^a-zA-Z]"
```

```
1:a1bb hua
3:a^3de
4:a funny
6:a345 dogs
```

##### 4、.符号：匹配一个字符

```
找到a什么c的行
cat regular_2.txt | grep -n --color "a.c"
```

```
7:acc fukf
```

#### 四：分组：

用例文件：

```
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_3.txt 
qinqin ni 
qinn ni
qin ni qin
abefefabefef
qu ni qu
```

```
想把第3行和第5行，取出来。使用()来先分组
cat regular_3.txt | grep --color "\(qin\)\{2\}"      
```

```
qinqin ni 
```

```
如果不分组，直接这样取出的是2个n
cat regular_3.txt | grep --color "qin\{2\}"
```

```
qinn ni
```

##### 再次使用前面的分组：

> 在一个含有分组的正则表达式中，默认情况下，每个分组会自动拥有一个组号（从左向右，以分组的**左括号**为标志，第一个出现的分组的组号为1，第二个为2，以此类推）后向引用用于重复搜索前面某个分组匹配的文本。例如，\1 代表此处需要再次匹配分组1 的内容。

如取出第3行和第5行：qin ni qin  ； qu ni qu

```
cat regular_3.txt | grep --color "\(.\+\) ni \1"
```

```
qin ni qin
qu ni qu
```

##### 分组嵌套：下边两种都可以

```
cat regular_3.txt | grep --color "\(ab\(ef\)\2\)\1"
```

```
cat regular_3.txt | grep --color "\(ab\(ef\)\{2\}\)\{2\}"
```

![image-20191021151657833](/Users/mac/Library/Application Support/typora-user-images/image-20191021151657833.png)

#### 五：扩展正则表达式：

扩展就是指（）和{}前边不用\。

> 要使得grep将正则表达式中的符号当做扩展表达式去理解，需要用到**-E**选项

```
带E和不带E对比
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_3.txt | grep --color "(.+) ni \1"
grep: Invalid back reference
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_3.txt | grep --color -E -n "(.+) ni \1"
3:qin ni qin
5:qu ni qu
```

##### 分组和|配合 ：|指或的意思. 这也是扩展里带的

```
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_3.txt | grep --color "(n|f)$"      不带
root@iZ2ze1y6kf6efdv2i5q4egZ:/home# cat regular_3.txt | grep --color -E "(n|f)$"   带
qin ni qin
abefefabefef
```





以上基本就够工作需要了。