### 最小的K个数

#### 题目描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。



**堆排序（大根堆）**

每次插入一个元素后，就把堆里面的大元素丢出去，因此堆里面剩下的都是小的元素，同时我们需要维护堆的大小为K

```python
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        # write code here
        # write code here
        import heapq
        tmp = []
        for i in tinput:
            heapq.heappush(tmp, -i)
            if len(tmp)>k:
                heapq.heappop(tmp)
        res = []
        for i in tmp:
            res.append(-i)
        res.sort()
        print(res)
```



**快速排序**

```python
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        # write code here
        def func(nums, left, right):
            if left>=right:
                return 
            tmp = nums[left]
            i, j = left, right
            while i < j:
                while i<j and tmp<=nums[j]:
                    j -= 1
                nums[i] = nums[j]
                while i<j and tmp>=nums[i]:
                    i += 1
                nums[j] = nums[i]
            nums[i] = tmp
            func(nums, left, i-1)
            func(nums, i+1,right)
            
        if k>len(tinput) or tinput == []:
            return []
        nums = tinput
        func(nums, 0, len(nums)-1)

        return nums[:k]
```

