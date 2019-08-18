#### [删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)(LeetCode 82)

#### 1.题目

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 *没有重复出现* 的数字。

**示例 1:**

```
输入: 1->2->3->3->4->4->5
输出: 1->2->5
```

**示例 2:**

```
输入: 1->1->1->2->3
输出: 2->3
```

#### 2.分析

#### 3.代码

```python
def deleteDuplicates(self, head: ListNode) -> ListNode:

    # 设置虚拟头结点
    
    if head is None:
        return
    newHead = ListNode(None)
    newHead.next = head
    pre = newHead
    cur = head
    while cur:
        
        if cur.next and cur.val == cur.next.val:
            # 如果重复元素有很多个连着的，需要走到重复元素的最后一个
            while cur.next and cur.val == cur.next.val:
                cur = cur.next
            pre.next = cur.next
            cur = cur.next
        else:
            pre = pre.next
            cur = cur.next
    # 最后不能返回head,因为【1，1，2，3】->【2，3】,head一直都指着链表的第一个元素
    return newHead.next
```
##### 延伸一

```python
不设置虚拟头结点，删除有序列表，但是最后要保留一个，而不是全部删   
#除 【1，2，3，3】->【1,2,3】
        
        if head is None:
            return
        pre = head
        cur = head.next
        
        while cur:
            if pre.val == cur.val:
                pre.next = cur.next
                cur = cur.next
            else:
                pre = cur
                cur = cur.next
        return head
```

##### 延伸二

```python
设置虚拟头结点，删除有序列表，但是最后要保留一个，而不是全部删       
#除 【1，2，3，3】->【1,2,3】
        if head is None:
            return
        newHead = ListNode(None)
        newHead.next = head
        pre = newHead
        cur = head
        
        while cur:
            if cur.next and cur.val == cur.next.val:
                pre.next = cur.next
                cur = cur.next
            else:
                pre = cur
                cur = cur.next
        return newHead.next
```

