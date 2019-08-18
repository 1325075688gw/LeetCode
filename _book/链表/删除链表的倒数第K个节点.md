### [删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)(LeetCode_19)

#### 1.题目

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

```
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 n 保证是有效的。

**进阶：**

你能尝试使用一趟扫描实现吗？

#### 2.分析

​	第一个指针从列表的开头向前移动 n+1n+1 步，而第二个指针将从列表的开头出发。现在，这两个指针被 nn 个结点分开。我们通过同时移动两个指针向前来保持这个恒定的间隔，直到第一个指针到达最后一个结点。此时第二个指针将指向从最后一个结点数起的第 nn 个结点。我们重新链接第二个指针所引用的结点的 next 指针指向该结点的下下个结点。

#### 3.代码

![Remove the nth element from a list](删除链表的倒数第K个节点.assets/4e134986ba59f69042b2769b84e3f2682f6745033af7bcabcab42922a58091ba-file_1555694482088.png)

```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        if head is None or n < 1:
            return head
        cur = head
        while cur!=None:
            n -= 1
            cur = cur.next
        
        if n == 0:
            head = head.next
        elif n > 0:
            pass
        elif n < 0:
            cur = head
            n = n+1
            while n !=0:
                n = n+1
                cur = cur.next
            cur.next = cur.next.next
        return head
```

```python
# 首先我们将添加一个哑结点作为辅助，该结点位于列表头部。哑结点用来简化某些极端情况，例如列表中只含有一个结点，或需要删除列表的头部。
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        fast = slow = dummy
        while n>=0:
            n -= 1
            fast = fast.next
        while fast is not None:
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next
        return dummy.next
            
```

