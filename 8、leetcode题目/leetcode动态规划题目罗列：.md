leetcode动态规划题目：

力扣120：

```python
class Solution(object):
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        row = len(triangle)-2
        for row in range(row,-1,-1):
            for i in range(len(triangle[row])):
                triangle[row][i] += min(triangle[row+1][i],triangle[row+1][i+1])
        return triangle[0][0]
```

64题：

```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        row = len(grid)
        col = len(grid[0])
        tem = [[0 for i in range(col)] for j in range(row)]
        for i in range(row):
            for j in range(col):
                if i>0 and j >0:
                    tem[i][j] = min(tem[i-1][j],tem[i][j-1])+grid[i][j]
                elif i>0:
                    tem[i][j] = tem[i-1][j]+grid[i][j]
                elif j>0:
                    tem[i][j] = tem[i][j-1]+grid[i][j]
                else:
                    tem[i][j] = grid[i][j]
        print(tem)
        print(grid)
        return tem[-1][-1]
        
a = Solution()
a.minPathSum([
  [1,3,1],
  [1,5,1],
  [4,2,1]
])
```

279

91

62

63

198：小偷偷房子里

213

337

309

------

300：最长上升子序列

322：凑硬币

377：

474：

139

494

------

最长子序列问题。

300

376

------

最长公共子序列