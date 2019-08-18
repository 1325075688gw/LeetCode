###  [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)(LeetCode_25)

####  1.题目

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

**示例 :**

```python
给定这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5

```



```python
说明 :

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。
```



#### 2.分析

- 递归

####  3.代码

```python
class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        count = 0
        cur = head
        while cur and count<k:
            count += 1
            cur = cur.next
        # cur找到下一个节点,即原链表为【1,2,3,4,5】,现在cur指向4,同时不用担心我们丢失1节点,因为head就是指向1节点
        
        if count == k:
            cur = self.reverseKGroup(cur, k)
            while count:
                next = head.next
                head.next = cur
                cur = head
                head = next
                count -= 1
            return cur
        # 当count != k时候,说明剩余不足k个节点,不用翻转,所以我们直接else： return head
        else:
            return head
```

