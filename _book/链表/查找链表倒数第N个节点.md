```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if head==None or k<=0:
            return None
        fast = slow = head
        count = 0
        while fast.next:
            fast = fast.next
            count += 1
            if count > k-1:
                slow = slow.next
        if count < k-1:
            return None
        return slow
```





```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if head==None or k<=0:
            return None
        fast = slow = head
        # 记住常用关系：大于0，是循环n次，所以推出，大于1是循环n-1次
        while k>1:
            if fast.next:
                fast = fast.next
                k -= 1
            else:
                return None
             
         
        while fast.next is not None:
            fast = fast.next
            slow = slow.next
        return slow
```

