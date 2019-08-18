#### [相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)(LeetCode 160)

#### 1.题目

编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表**：**

[![img](相交链表 LeetCode 160.assets/160_statement.png)](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

**示例 1：**

[![img](相交链表 LeetCode 160.assets/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

**示例 2：**

[![img](相交链表 LeetCode 160.assets/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

**示例 3：**

[![img](相交链表 LeetCode 160.assets/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```

 

**注意：**

- 如果两个链表没有交点，返回 `null`.
- 在返回结果后，两个链表仍须保持原有的结构。
- 可假定整个链表结构中没有循环。
- 程序尽量满足 O(*n*) 时间复杂度，且仅用 O(*1*) 内存。

#### 2.分析

- 判断地址，而不是val，因为那两个1实际上不是同一个节点，地址不同，直接判断地址就行了
- 首尾相连法: 同时对A和B进行遍历, 并且让到达末尾的指针指向另一个链表的头结点. 例如A: 6->7->4->5; B: 1->2->3->4->5 遍历时会相交于4 (67451234, 12345674).
- 备用法（未实现）: 求出两个链表A和B的长度, 长链表先走|len(A)-len(B)|步, 然后同时遍历返回第一个公共节点.

#### 3.代码

#####  首尾相连法

```python
    def getIntersectionNode(self, headA, headB):
        # 首尾相连法
        if headA is None or headB is None:
            return None
        p = headA
        q = headB
        while p != q:
            p = p.next if p else headB
            q = q.next if q else headA
        return p
```

##### 字典法

```python
    def getIntersectionNode(self, headA, headB):
        d = {}
        while headA:
            d[headA] = 1
            headA = headA.next
        while headB:
            if headB in d:
                return headB
            headB = headB.next
        return None
```

##### 集合法

```python
    def getIntersectionNode(self, headA, headB):
        d = set()
        while headA:
            d.add(headA)
            headA = headA.next
        while headB:
            if headB in d:
                return headB
            headB = headB.next
        return None
```

