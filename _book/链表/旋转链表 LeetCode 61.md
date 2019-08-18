#### [旋转链表](https://leetcode-cn.com/problems/rotate-list/)(LeetCode 61)

#### 1.题目

给定一个链表，旋转链表，将链表每个节点向右移动 *k* 个位置，其中 *k* 是非负数。

**示例 1:**

```python
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```

**示例 2:**

```ython
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

#### 2.分析

这个问题其实和 Leetcode 19: 删除链表的倒数第 N 个节点（最详细解决方案！！！）是一样的。其实就是一个循环链表首先，如果head == None or head.next == None我们直接返回head就可以了。

因为q = q.next，所以是左旋

#### 3.代码

```python
 def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if head == None or head.next == None:
            return head
        # 初始有一个点
        count = 1
        cur = head
        while cur.next:
            count += 1
            # 前指针，这儿没有用，但是可以看看怎么写
            # pre = cur
            cur = cur.next
        # 首尾连接
        cur.next = head
        # 从尾巴开始左旋
        tmp = cur
        # print(cur.val)
        k = count - k%count
        for _ in range(k):
            # 这句话阐述了是左旋，我们可以这么理解，左边的等于右边的就是左旋；右边的等于左边的，就是右旋
            tmp = tmp.next
        # 旋转完毕，断开换
        new_head = tmp.next
        tmp.next = None
        return new_head
        
```

