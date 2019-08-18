## 合并K个排序链表

#### 1.题目

合并 *k* 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**

```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

#### 2.分析

​	首先将list中的每个 链表 比较首元素，然后依次加入优先队列（或者一个堆，我这里使用堆）
然后判断这个 优先队列 是否为空，不为空，我们弹出队首元素（1），接着判断这个弹出的元素作为一个链表节点，其后是否还有元素，如果有元素，将元素加入队列。同时将结果加入到result中

#### 3.代码

##### 优先队列（每次只加入各队列最小值比较）

```python
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        import heapq
        gw = []
        new_head = cur = ListNode(0)
        x = 0
        for i in lists:
            if i:
                heapq.heappush(gw, (i.val, x, i))
                x += 1
        while len(gw) > 0:
            tmp = heapq.heappop(gw)[2]
            cur.next = tmp
            cur = cur.next
            if tmp.next:
                heapq.heappush(gw, (tmp.next.val, x, tmp.next))
                x += 1
        return new_head.next
```

##### 优先队列（一次性加入所有元素）

```python
    def mergeKLists(self, lists):
        import heapq
        result = ListNode(-1)
        cur = result
        p = list()
        x = 0
        for i in lists:
            while i:
                heapq.heappush(p, (i.val, x, i))
                i = i.next
                x += 1
        while p:
            cur.next = heapq.heappop(p)[2]
            cur = cur.next
        return result.next

```

##### 分治法（未完成）

```python
  def mergeKLists(self, lists: List[ListNode]) -> ListNode:
            def merge(a, b):
                head = ListNode(0)
                cur = head
                while a and b:
                    if a.val > b.val:
                        cur.next = b
                        b = b.next
                    else:
                        cur.next = a
                        a = a.next
                    cur = cur.next
                if a:
                    cur.next = a
                if b:
                    cur.next = b
                return head.next

            # 采用分治法
            n = len(lists)
            if n == 0:
                return None
            def deal(l, r):
                if l > r:
                    return None
                if l == r:
                    return lists[0]
                middle = (l+r) // 2
                a = deal(l, middle)
                b = deal(middle, r)
                return merge(a, b)
            return deal(0, n-1)
```



> [!NOTE]
>
> ​	当对一个 tuple 排序时， python 会从 0 开始对两个 tuple 的成员依次比较，如果两个成员相同就再比较下一个成员。问题中的 tuple 很有趣，前两个链表的第一项比较结果都相同（ 1 ），于是 python 开始比较第二个成员，第二个成员是一个ListNode，没有比较方法，在处理这个问题上 py2 和 py3 有了差异， py2 随机瞎排， py3 则是抛出异常。
> 	一种解决办法是我们重写一个ListNode，给他添加val元素方法。我这里使用了另外的一种解决思路，就是在tuple中再添加一个元素。

