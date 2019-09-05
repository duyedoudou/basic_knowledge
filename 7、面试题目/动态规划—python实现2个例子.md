### 动态规划—python实现

> 两个案例：斐波那契&凑硬币

##### 斐波那契：

```python
# 暴力解法
def fib(n):
    if n == 1 or n == 2:
        return 1
    else :
        return fib(n-1)+fib(n-2)
fib(7)
```

```python
# 带备忘录解法
def fib2(n):
    f = [0 for i in range(n+1)]
    f[1],f[2] = 1,1
    return helper(f,n)

def helper(f,n):
    if n>2:
        f[n] = helper(f,n-1) + helper(f,n-2)
    return f[n]

fib2(7)
```

```python
# 使用动态规划方法，从小到大
def fib3(n):
    f = [0,1,1]
    for i in range(3,n+1):
        f.append(f[i-1]+f[i-2])
    return f[n]

fib3(7)
    
```











##### 凑硬币：

```Python
# 暴力
def coinChange(lis,amount):
    ans = 9999
    if amount == 0:
        return 0
    for i in lis:
        if amount-i < 0:               # 剩余的钱不够当前面值
            continue
        sub = coinChange(lis,amount-i)
        if sub == -1:                  # 凑不成的情况
            continue 
        ans = min(ans,sub+1)                         
    return -1 if ans == 9999 else ans
  
coinChange([1,2,5],11)
'''
对ans = min(ans,sub+1) 的解释：(以11块钱，【1元，2元，5元】为例)
如1+min(5,3,4) = 4。
即凑成10块钱要5个硬币，凑成9块钱要3个硬币，凑成6块钱要4个硬币。那么凑成11块钱最少要3+1个硬币。

在[1，2，5]的循环体里：ans初始为9999，
则有ans = min（9999，5+1）=6;再有ans = min（6，3+1）=4；再有ans = min（4，4+1）=4
最终ans为4
'''      
```

```python
# 带备忘录 coins：硬币面值   amount：要凑的钱数
def coinChange(coins,amount):
    lis = [-2 for i in range(amount+1)]  # 存放中间算出过的值，全部置成-2是为了不重复
    return helper(coins,amount,lis)  
def helper(coins,amount,lis):
    ans = 9999
    if amount == 0:
        return 0
    if lis[amount] != -2:
        return lis[amount]
    for i in coins:
        if amount-i < 0:
            continue
        sub = helper(coins,amount-i,lis)
        if sub == -1:
            continue
        ans = min(ans,sub+1)
    lis[amount] = -1 if ans == 9999 else ans
    return lis[amount]  
coinChange([1,2,5],11)   
```

```Python
# 动态规划
def coinChange3(coins,amount):
    dp = [0]
    for i in range(1,amount+1):     # 外循环，依次填充dp列表
        tem = 999999                # 置为一个非常非常大的值
        for j in coins:             # 内循环，依次比较如[1，2，5]
            if i - j < 0:
                continue
            tem = min(dp[i-j]+1,tem)
        dp.append(tem)              # 内循环结束后，dp列表增加
    return dp[amount] if dp[amount]!=999999 else -1

print(coinChange3([1,2,5],11))
print(coinChange3([5],11))
        
```

