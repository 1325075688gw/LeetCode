#### [数据流的中位数](https://leetcode-cn.com/problems/find-median-from-data-stream/)(LeetCode 295) (如何从5亿个数中找出中位数)

#### 1.题目

中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

**示例：**

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

**进阶:**

1. 如果数据流中所有整数都在 0 到 100 范围内，你将如何优化你的算法？
2. 如果数据流中 99% 的整数都在 0 到 100 范围内，你将如何优化你的算法？

#### 2.分析

```
满足两个特性：
1.大顶堆中最大的数值小于等于小顶堆中的最小数，也就是小于小顶堆的堆顶
2.两个堆中元素相差为0，或者为1,不能>1

然后，我们观察可以发现，如果，数据总数是偶数，那么大顶堆，和小顶堆，
一边占一半元素，而且，还是有序的，很像二分法，这时，中位数为两堆顶平均值
如果数据个数为奇数，则，中位数出现在元素个数多的堆的堆顶中
```

```
# 每次都插入到最小堆，然后，将最小堆里面的栈顶元素，
# 取出来，放到最大堆中去，这样就能保证最小堆的堆，都比最大堆的堆顶大
#（因为最大堆是最小堆，一泡屎一趴尿，拉扯大的。）
# 下面的调整，使得最小最大堆元素相差最多为1，而且永远是 最小堆元素个数大于  等于最大堆元素个数
```

#### 3.代码

```python
from heapq import *
class MedianFinder:
    def __init__(self):
        self.max_h = []
        self.min_h = []
        heapify(self.max_h)
        heapify(self.min_h)
        
    def addNum(self, num):
        heappush(self.min_h,num)
        heappush(self.max_h,-heappop(self.min_h))
        if len(self.min_h) < len(self.max_h):
            heappush(self.min_h,-heappop(self.max_h))
            
    def findMedian(self):
        max_len = len(self.max_h)
        min_len = len(self.min_h)
        return self.min_h[0]*1. if max_len!=min_len else (-self.max_h[0]+self.min_h[0])/2.
        # if min_len == max_len:
        #     return (-self.max_h[0]+self.min_h[0])/2.
        # elif max_len > min_len:
        #     return -self.max_h[0]*1.
        # else:
        #     return self.min_h[0]*1.
```

```python
from heapq import *
class MedianFinder:

    def __init__(self):
        self.max_h = []
        self.min_h = []
        heapify(self.max_h)
        heapify(self.min_h)
    def addNum(self, num: int) -> None:
        if not self.max_h:
            heappush(self.max_h,-num)
            return
        if not self.min_h:
            tmp = -heappop(self.max_h)
            if num >= tmp:
                heappush(self.max_h,-tmp)
                heappush(self.min_h,num)
            else:
                heappush(self.max_h,-num)
                heappush(self.min_h,tmp)
        else:
            if num < -self.max_h[0]:
                if len(self.max_h)<=len(self.min_h):
                    heappush(self.max_h,-num)
                else:
                    tmp = -heappop(self.max_h)
                    heappush(self.min_h,tmp)
                    heappush(self.max_h,-num)
            elif -self.max_h[0]<=num<=self.min_h[0]:
                if len(self.max_h)<len(self.min_h):
                    heappush(self.max_h,-num)
                else:
                    heappush(self.min_h,num)
            else:
                if len(self.max_h)>=len(self.min_h):
                    heappush(self.min_h,num)
                else:
                    tmp = heappop(self.min_h)
                    heappush(self.max_h,-tmp)
                    heappush(self.min_h,num)
            
            
    def findMedian(self) -> float:
        # print(self.max_h,"====",self.min_h)
        max_len = len(self.max_h)
        min_len = len(self.min_h)
        
        if min_len == max_len:
            return (-self.max_h[0]+self.min_h[0])/2.
        elif max_len > min_len:
            return -self.max_h[0]*1.
        else:
            return self.min_h[0]*1.
```

