#### 暂定他叫杂项：

> 1、斐波那契数列

思路1：递归 递归的效率很低

```python
def fibb(n):
    if n==1 or n ==2:
        return 1
    else: return fibb(n-1)+fibb(n-2)   # 因为没有存储，每次递归需要重新计算前边计算过的
```

思路2：循环   避免重复计算，即算过的数用变量存起来.

```python
def fib(N):            # N可以为0
    a=0
    b=1
    for i in range(N):
        a,b = b,a+b
    return a
```

> 2、青蛙跳台阶
>
> 青蛙一次可以跳上1级台阶，也可以跳上2级台阶，求跳上n级台阶有多少种跳法。

思路：设跳上n级台阶有f(n)种跳法，那么跳上n-1级台阶有f(n-1)种跳法；跳上n-2级台阶有f(n-2)种跳法。

第一次跳上1级，此时的跳法数目就是f(n-1)种；第一次跳上2级，此时的跳法数目就是f(n-2)种。

所以f(n)=f(n-1)+f(n-2)，这不就是斐波那契数列么。

```python
# 斐波那契的应用
# f(n)=f(n-1)+f(n-2)
def jump(n):                # n从1开始
    a=1
    b=2
    for i in range(n-1):
        a,b = b,a+b
    return a

```





> 3、动态规划
> 给你一根长度为 n 绳子，请把绳子剪成 m 段（m、n 都是整数，2≤n≤58 并且 m≥2）。
> 每段的绳子的长度记为k[0]、k[1]、……、k[m]。k[0]k[1] … k[m] 可能的最大乘积是多少？
> 例如：当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到最大的乘积18。

```python
# 方法二：动态规划
def dynamic_programming(n):
    if n==2:                         # 这3个特殊的长度，直接求出返回值
        return 1
    if n==3:
        return 2
    if n==4:
        return 4
    tem_lis = [0,0,2,3,4]                 # 这个列表的前两个数无所谓，因为根本用不到
    
    for i in range(5,n+1):                # 外循环：绳子长度从5到n  注意range()前闭后开。
        maxx = 0 
        for j in range(2,i//2+1):         # 内循环：所有可能的组合：2，3，4...中间值
            tem = tem_lis[j]*tem_lis[i-j] # i-j 为另一段长度
            if tem > maxx:
                maxx = tem                # maxx存放乘积最大的值
        tem_lis.append(maxx)              # tem_list中存储的是所有的可能绳子长度的解
    #print(tem_lis)
    return tem_lis[n]

dynamic_programming(8)
                
```

> 4、替换空格
> 将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

思路1：先把字符串转成列表，修改后，再拼接回去

思路2：字符串的 replace 方法

```python
# 方法二：字符串的 replace 方法
class Solution:
    def replaceSpace(self, s):
        s=s.replace(' ','%20')
        return s
```

> 5、二进制中的1的个数

利用二进制的数字特点

思路1：把一个整数减去1，在和原来的数做与运算，就会把原数`最右边`的1变成0，循环的次数和1的个数一样。

思路2：n&1==1  ，相等则计数加1，然后n>>1        循环的次数是二进制的长度。

> 6、数值的整数次方

思路：利用数学公式进行递归。

```python
# 使用的是数学公式，剑指offer书P112。
# 使用每次除以2 的方法，减少了非常多的计算量
def mypoww(x,n):
    def tem(x,n):   
        if n == 0:              # n=0和n=1两个边界情况
            return 1
        if n == 1:
            return x
        result =tem(x,n>>1)     # 递归调用；   同时使用右移代替除以2，效率高
        result*=result          # 此行和余下几行是根据公式写出的
        if n&1 == 1:            # 如果n是奇数
            result*=x
        return result
    
    if n>0:                  
        return tem(x,n)
    if n == 0:                  # 考虑n=0和n<0时候的特殊情况
        if x == 0:
            return 'error'
        else:
            return tem(x,n)
    if n<0:
        if x == 0 :
            return 'error'
        else:
            return 1/tem(x,abs(n))

mypoww(0.0001,234543)
```

#### 