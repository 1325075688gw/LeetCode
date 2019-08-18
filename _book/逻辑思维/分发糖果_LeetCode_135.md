### [分发糖果](https://leetcode-cn.com/problems/candy/)(LeetCode_135)

#### 1.题目

老师想给孩子们分发糖果，有 N 个孩子站成了一条直线，老师会根据每个孩子的表现，预先给他们评分。

你需要按照以下要求，帮助老师给这些孩子分发糖果：

每个孩子至少分配到 1 个糖果。

- 相邻的孩子中，评分高的孩子必须获得更多的糖果。
- 那么这样下来，老师至少需要准备多少颗糖果呢？

那么这样下来，老师至少需要准备多少颗糖果呢？

**示例 1:**

```
输入: [1,0,2]
输出: 5
解释: 你可以分别给这三个孩子分发 2、1、2 颗糖果。
```

**示例 2:**

```
输入: [1,2,2]
输出: 4
解释: 你可以分别给这三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这已满足上述两个条件。
```

#### 2.分析

...

#### 3.代码

```python
class Solution(object):
    def candy(self, ratings):
        """
        :type ratings: List[int]
        :rtype: int
        """
        n = len(ratings)
        res = n
        arr = [0] * n
        # 先正序遍历，如果后一位比前一位高分，就给比前一位多1的糖果，否则给1
        for i in range(1,n):
            if ratings[i]>ratings[i-1]:
                arr[i] = arr[i-1]+1
         
        # 在倒叙遍历，如果前一位比后一位高分并且得到的糖果小于或等于后一位，就给前一位孩子比后一位孩子多一个糖果
        # [1,2,3,99,8,7,6,5,4,3,2,1] 99就是上面的特殊情况 99的糖果数应该为8的糖果数+1
        for j in range(n-2,-1,-1):
            if ratings[j]>ratings[j+1] and arr[j]<=arr[j+1]:
                arr[j] = arr[j+1]+1
        res += sum(arr)
        return res
```



**优化**

```python
class Solution(object):
    def candy(self, ratings):
        """
        :type ratings: List[int]
        :rtype: int
        """
        n = len(ratings)
        res = n
        arr = [0] * n
        # 先正序遍历，如果后一位比前一位高分，就给比前一位多1的糖果
        for i in range(1,n):
            if ratings[i]>ratings[i-1]:
                arr[i] = arr[i-1]+1
        
        # 倒序过程中,统计数量
        res += arr[-1]
        # 在倒叙遍历，如果前一位比后一位高分并且得到的糖果小于或等于后一位，就给前一位孩子比后一位孩子多一个糖果
        for j in range(n-2,-1,-1):
            if ratings[j]>ratings[j+1] and arr[j]<=arr[j+1]:
                arr[j] = arr[j+1]+1
            res += arr[j]
        return res
        
```

