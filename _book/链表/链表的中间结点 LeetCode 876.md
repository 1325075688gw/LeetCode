#### [链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)(LeetCode 876)

#### 1.题目

给定一个带有头结点 `head` 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

**示例 1：**

```
输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
```

**示例 2：**

```
输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。
```

**提示：**

- 给定链表的结点数介于 `1` 和 `100` 之间。

#### 2.分析

- 快慢指针，不过最后要分奇数、偶数讨论
  - 当链表长度为奇数时，快指针走到链表尾部时，慢指针恰好指向链表的中间
  - 当链表长度为偶数时，慢指针所指节点和所指节点的下一节点都是链表的中间节点
- 计算链表节点个数，然后扫描

#### 3.代码

##### 快慢指针

```python

class Solution(object):
    def middleNode(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        
        if not head or not head.next:return False
        
        fast = slow = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        
        # [1,2,3,4,5] 奇数个,又因为fast一次跳两个,所以第一次跳到3,第二次跳到5,所以当元素个数为奇数时候,fast.next为空,返回slow.next
        # [1,2,3,4,5,6] 偶数个, fast第一次跳到3,第二次跳到5,由于fast.next.next为None,所以退出循环,所以fast.next.val == 6, fast.next不为空
        if fast.next:
            return slow.next
        else:
            return slow
```

##### 遍历法

```python
        def middleNode(self, head: ListNode) -> ListNode:
            if head == None or head.next == None:
                return head
            k = 1
            cur = head
            while cur.next:
                k += 1
                cur = cur.next
            k //=2
            while k>0:
                head = head.next
                k -= 1
            return head
```



