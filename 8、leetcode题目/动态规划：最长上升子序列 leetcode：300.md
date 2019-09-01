#### 动态规划：leetcode：300  

> 给定一个无序的整数数组，找到其中最长上升子序列的长度。
>
> 示例:
>
> 输入: [10,9,2,5,3,7,101,18]
> 输出: 4 
> 解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。

```Python
# 时间复杂度：O（N**2)
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        lis = [1 for i in range(n)]
        for i in range(n):
            tem = [0]
            for j in range(0,i):
                if nums[j]<nums[i]:
                    tem.append(lis[j])
            lis[i] = max(tem) + 1
        return max(lis)

```

