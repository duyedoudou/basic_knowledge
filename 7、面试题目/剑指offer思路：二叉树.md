#### 二叉树：

> 1、重建二叉树
>
> 根据前序遍历和中序遍历重建二叉树，假设遍历结果中不包含重复的数字。

思路：前序的下标为0元素A就是根节点，在中序中找到A的下标flag1，即可确定下一层前序和中序的起始位置。

然后使用递归。

```python
tree.left = self.rebuild(pre[1:flag1+1],mid[:flag1])   
tree.right = self.rebuild(pre[flag1+1:],mid[flag1+1:]) 
```

> 2、二叉树的镜像

思路1：递归   改变了树，即在原来的基础上改动的

```python
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
# 递归的解法，注意看我copy的递归的另一种写法
class Solution:
    # 返回镜像树的根节点
    def Mirror(self, root):
        if root:
            root.left,root.right = root.right,root.left
            root.left = self.Mirror(root.left)
            root.right = self.Mirror(root.right)
        return root
```

```python
# 我不给左右赋值
class Solution:
    # 返回镜像树的根节点
    def Mirror(self, root):
        if root:
            root.left,root.right = root.right,root.left
            self.Mirror(root.left)   # 就是这两行
            self.Mirror(root.right)
        return root
```







> 3、判断2个二叉树是不是镜像对称的。

```python
class Solution(object):
    def isSymmetric(self, root):
         #  :type root: TreeNode     :rtype: bool
        def mirr(l1,l2):
            if not l1 and not l2:
                return True
            elif l1 and l2:
                if l1.val == l2.val:
                    return mirr(l1.left,l2.right) and mirr(l1.right,l2.left)
                else:
                    return False
            else:
                return False        
        if not root:
            return True
        else:
            return mirr(root.left,root.right)
```

> 4、二叉树中路径和是某值得路径

思路：递归。

​			利用栈的思想，压栈的时候，压一个列表进去，列表里多放点东西。

```python
# 本题注意压入的顺序和弹出的顺序
class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        stack = root and [(root,[root.val],sum)]   # 找假值，如果都为真，就返回最后一个真值
        liss = []                                  # 空表存放路径，路径是列表形式 
        while stack:
            n,v,s = stack.pop()                    # v是路径，是一个列表
            if not n.left and not n.right and n.val == s:  # 路径到底，且路径和满足条件
                liss.append(v)
            if n.right:                            # 先压右
                stack.append((n.right,v+[n.right.val],s-n.val))
            if n.left:                             # 在压左
                stack.append((n.left,v+[n.left.val],s-n.val))
        return liss                                # 坐等循环结束                                   
```

> 5、二叉树的中序遍历下一个节点
>
> 给定一个二叉树和其中的一个结点A，请找出中序遍历顺序的下一个结点并且返回。
>
> 注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

思路：A的右节点R如果存在，再用while循环判断R的左节点是否存在，最终的左节点即输出值。

​			A的右节点R如果不存在，则while循环找A的父节点F，判断A是不是F的左节点，如果是，则输出F。如果不是，则再向上一层，继续while的第二次循环。最后找不到，则输出False。

```python
# class TreeLinkNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None          # 指向父节点的指针
class Solution:
    def GetNext(self, pNode):       # 寻找给定节点的下一个节点
        if pNode == None:           
            return None
        if pNode.right:             # 右子树存在
            pre = pNode.right       # 锁定右子树
            while pre.left:         # 使用循环，找锁定的右子树的根节点的最下层左子树
                pre = pre.left
            return pre              # 循环结束后，最左的就是目标
        
        while pNode.next:           # 右子树不存在
            parent = pNode.next     # 锁定这个节点的父节点
            if parent.left == pNode:# 如果给定节点是其父节点的左子树
                return parent       # 那么其父节点就是目标
            pNode = parent          # 如果给定节点是其父节点的右子树，就往上层迭代，新一轮循环
        return None                 # 如果到顶了：不满足循环条件。说明，他没有下一节点了

```

