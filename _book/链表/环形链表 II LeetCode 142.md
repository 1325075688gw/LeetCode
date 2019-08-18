#### [环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)(LeetCode 142)

#### 1.题目

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**说明：**不允许修改给定的链表。

 

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

**示例 2：**

```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

**示例 3：**

```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**进阶：**
你是否可以不用额外空间解决此题？

#### 2.分析

使用快慢指针先确定是否有环，有的话，将fast指向head，和slow指针以相同的速度移动，当fast==slow时则找到了环的入口。

第一次相遇，肯定是在环内，因为快指针比慢指针快一倍，所以，快指针比慢指针多走一倍路程，其中满指针走过的路程就是这一倍路程，快指针走的两倍路程是这样来的，慢指针的一倍路程，加上圆圈的长度（从相遇点出发，沿着环走，再次回到相遇点）。现在两个指针都剪掉，入环点到相遇点的路程，两边剩下的路程长度相同（慢指针到入环点，和快指针从入环点逆时针回到相遇点），所以，一个从head出发，一个从相遇点出发，走到入环点的路程长度相同。

#### 3.代码

##### 字典法

```python
    def detectCycle(self, head):
        if head == None:
            return None
        bag = {}
        index = 0
        while head.next:
            if head not in bag:
                bag[head] = index
                index += 1
                head = head.next
            else:
                # 输出环形链表是第几个节点，但是有错，深拷贝也不行
                # return bag[cur]
                return head
        return None
```

##### 快慢指针，写成两个函数

```python
class Solution(object):
    def detectCycle(self, head):
        count = self.func(head)
        if count ==0:return None
        t1,t2 = head,head
        for i in range(count):
            t2 = t2.next
        while t1!=t2:
            t1 = t1.next
            t2 = t2.next
        return t1
    
    # 先判断有没有环
    def func(self,head):
        if head == None or head.next == None:
            return 0
        fast = slow = head
        count = 0
        while fast.next and fast.next.next:
            count+=1
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return count
        return 0
        
```

##### 快慢指针，写成一个函数

```python
class Solution(object):
    def detectCycle(self, head):
        if not head or not head.next:
            return None
        fast = slow = head
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                slow = head
                while fast != slow:
                    fast = fast.next
                    slow = slow.next
                return fast
        return None
```

