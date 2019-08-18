## 前K个高频元素

#### 1.题目

给定一个非空的整数数组，返回其中出现频率前 **k** 高的元素。

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

**说明：**

- 你可以假设给定的 *k* 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
- 你的算法的时间复杂度**必须**优于 O(*n* log *n*) , *n* 是数组的大小。

#### 2.分析

#### 3.代码1

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        import collections
        obj = collections.Counter(nums)
        res = (obj.most_common(k))
        # print(obj)
        ans =  map(lambda x:x[0], res)
        return list(ans)
```

#### 代码2

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:    
    # 代码2，用字典来计算
        bag = {}
        for i in nums:
            if i not in bag:
                bag[i] = 1
            else:
                bag[i] += 1
        outPut = sorted(bag.items(), key=lambda x:x[1], reverse=True)
        res = []
        for i in range(k):
            res.append(outPut[i][0])
        return res      
```



