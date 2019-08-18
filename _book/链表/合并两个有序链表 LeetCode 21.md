## [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)(LeetCode 21)

#### 1.题目

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

#### 2.分析

​	新建立一个新的链表。建立两个指针cur1和cur2，分别指向两个链表。然后只需要通过比较两个链表每个元素的大小，小的元素添加到新的链表中即可。最后，我们要分别判断cur1和cur2是否是各自链表的末尾，如果不是，将剩余元素添加到新的链表末尾即可。

#### 3.代码

##### 非递归

```python
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        tail = head = ListNode(0)
        while l1 and l2:
            if l1.val < l2.val:
                node = ListNode(l1.val)
                tail.next = node
                tail = node
                l1 = l1.next
            else:
                node = ListNode(l2.val)
                tail.next = node
                tail = node
                l2 = l2.next
        if l1:
            tail.next = l1
        if l2:
            tail.next = l2
        return head.next
```

> [!NOTE]
>
> ```python
>     if l1:
>         tail.next = l1
>     if l2:
>         tail.next = l2
>     
>     改为：tail.next = l1 or l2
> ```

##### 代码2非递归

```python
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2
        if not l2: return l1

        tail = head = ListNode(0)
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        if l1:
            tail.next = l1
        if l2:
            tail.next = l2
        return head.next
```

##### 递归版

```python
        def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
            if not l1:return l2
            if not l2:return l1
            if l1.val < l2.val:
                l1.next = self.mergeTwoLists(l1.next, l2)
                return l1
            else:
                l2.next = self.mergeTwoLists(l1, l2.next)
                return l2
```

