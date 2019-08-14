#### python程序员面试宝典 7

1、用1，2，3，2，4，5这六个数，打印出所有的排列组合。要求：‘4’不在第三位，‘3’和‘5’不能相连。

思路：使用无向图的思想。

```python
# 深度遍历  
class Test():
    def __init__(self,arr):
        self.numbers = arr
        self.n = len(arr)                  # 数组长度
        self.visited = ['False']*self.n    # 标记是否走过
        self.graph = [([None]*self.n) for i in range(self.n)]  # 图
        self.combination =''               # 临时存储 
        self.s = set()                     # 用集合存符合的结果
        
    def depth_first_search(self,start):
      # 功能：对图从start节点出发，深度遍历
        self.visited[start] = 'True'             # 操作1
        self.combination += str(self.numbers[start])# 操作2
        if len(self.combination) == self.n:      # 长度符合时  
            if self.combination.index("4") != 2:
                self.s.add(self.combination)     # 使用add
                
        for j in range(self.n):                  # ！！此处最难懂
            if self.graph[start][j] == 1 and self.visited[j] == 'False':
                self.depth_first_search(j)
        self.combination = self.combination[:-1] # 对操作2还原
        self.visited[start] = 'False'            # 对操作1还原
        
    def get_all_combinations(self):
        # 功能：构造图
        for i in range(self.n):
            for j in range(self.n):
                if i == j:
                    self.graph[i][j] = 0
                else:
                    self.graph[i][j] = 1
        self.graph[3][5] = 0
        self.graph[5][3] = 0
        for i in range(self.n):
            self.depth_first_search(i)
        
    def print_combination(self):          # 功能：打印集合元素
        print('共%i个元素。'%len(self.s))
        for i in self.s:
            print(i)
            
arr = [1,2,2,3,4,5]        
a = Test(arr)
a.get_all_combinations()
print(a.combination)       # 空
a.print_combination()

        
```

那么几个元素的全排列怎么写呢？

```python
# 全排 深度优先遍历
arr = ["a","b","c"]
visit = [True, True, True]           # true标记没访问过
temp = ["" for x in range(len(arr))]
s = []                               # 存放最终结果
def dfs(position):
    if position == len(arr):
        s.append(temp[:])            # 要使用拷贝
#         print(temp)
        return

    for i in range(0,len(arr)):
        if visit[i] == True:
            temp[position] = arr[i]
            visit[i] = False
            dfs(position + 1)
            visit[i] = True
 
dfs(0)
print(s)
```

```python
# 全排 递归
def permutations(arr, position, end):
    if position == end:
        print(arr)
    else:
        for i in range(position, end):
            arr[i], arr[position] = arr[position], arr[i]
            permutations(arr, position+1, end)
            arr[i], arr[position] = arr[position], arr[i]
 
arr = ["a","b","c"]
permutations(arr, 0, len(arr))
```

