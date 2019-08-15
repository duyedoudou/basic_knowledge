#### 链表：

> 1、从尾到头打印链表
> 输入一个链表头，按链表值从尾到头的顺序返回一个列表。

思路：使用列表[]存储，列表的insert（）方法，在0位置插入。

> 2、删除链表的节点

思路：用后一个节点，把前边节点的信息覆盖。实际上被删除的节点依然指向不变

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteNode(self, node):
        node.val = node.next.val  # 4->1->2->9
        node.next = node.next.next  # 4->1->9
#                                           ^
#                                           |
#                                           2
    
```

> 3、链表中倒数第k个节点
> 输入一个链表，输出该链表中倒数第k个结点。

思路：快慢指针，快指针比慢指针先走k步。

> 4、反转一个单链表

思路1：原地反转。

思路2：递归法：先逆序第一个节点之外的子链表….

思路3：插入法：从第二个节点开始，把遍历到的每个节点插入到头结点之后。

















> 5、合并两个有序链表

方法1：递归

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution(object):
    def mergeTwoLists(self, l1, l2):   # 函数的功能是，对输入的两个有序链表整成一个有序的链表
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1 or not l2:   # 如果l1和l2有一个或者2个空的
            return l1 or l2    # return 和 or 的组合，返回第一个真值
        if l1.val <= l2.val:
            l1.next = self.mergeTwoLists(l1.next,l2)   # 括号里的参数位置可以随意。
            return l1           # 最后返回的是一个链表，而不是一个元素
        if l1.val > l2.val :
            l2.next = self.mergeTwoLists(l1,l2.next)   # 括号里的参数位置可以随意。
            return l2
         
```

方法二：迭代

```python
def mergeTwoLists(l1, l2):
    l = head = ListNode(0)   # head指向这个链表的头
    while l1 and l2:
        if l1.val <= l2.val:
            l.next, l1 = l1, l1.next
        else:
            l.next, l2 = l2, l2.next
        l = l.next   # 这一句是必须的，要让l指向自己的下一个元素，不然再一次循环时候，l还是指向头结点
    l.next = l1 or l2   # 谁不是空，l.next就指向谁
    return head.next    # 返回从头开始的链表
```

#### 