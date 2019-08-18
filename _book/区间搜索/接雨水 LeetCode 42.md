#### [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)(LeetCode_42)

#### 1.题目

给定 *n* 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

![img](../%E5%8D%95%E8%B0%83%E6%A0%88/%E6%8E%A5%E9%9B%A8%E6%B0%B4_LeetCode_42.assets/rainwatertrap.png)

上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。

**示例:**

```c++
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```

#### 2.分析

- 这道题真正**难点**在于: 在一个位置能容下的雨水量等于它左右两边(`并不要求最近的最高`)柱子最大高度的最小值减去它的高度.比如下图所示,

- ![Snipaste_2019-05-11_18-02-16.png](../%E5%8D%95%E8%B0%83%E6%A0%88/%E6%8E%A5%E9%9B%A8%E6%B0%B4_LeetCode_42.assets/6db1fe9019dfbf4d5c2e472112c5cd227925d4b5a99ac48cd2a2779d2535b6ce-Snipaste_2019-05-11_18-02-16.png)

- 位置`i`能容下雨水量:`min(3,1) - 0 = 1`

  所以,问题就变成了: 如何找所有位置的左右两边的柱子的最大值?


- 单调栈
- 找最高点，然后从左右两边遍历到中间
- 动态规划
- 不用动态规划

#### 3.代码



**单调递增栈**:

==注意：==因为左边和右边对于接雨水没有用，所以第一个元素的左边我们不需要加float('inf') ,最后个元素也不需要float('inf')

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        # height = [float('inf')] + height[:] + [float('inf')]
        n = len(height)
        
        res = 0
        stack = []
        for i in range(n):
            while stack and height[i]>height[stack[-1]]:
                tmp = stack.pop()
                if not stack:
                    break
                res += (min(height[stack[-1]],height[i])-height[tmp]) * (i-stack[-1] - 1)
                # print(res)
            stack.append(i)
        return res
```



**单调递增栈**

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        # height = [float('inf')] + height[:] + [float('inf')]
        n = len(height)
        
        res = 0
        stack = []
        for i in range(n):
            if not stack or height[i]<height[stack[-1]]:
                stack.append(i)
            else:
                while stack and height[i]>=height[stack[-1]]:
                    tmp = stack.pop()
                    if stack:
                        res += (min(height[stack[-1]],height[i])-height[tmp]) * (i-stack[-1]-1)
                    else:
                        # 左右两边界不能装水，所以我们不需要 height = [float('inf')] + height[:] + [float('inf')]
                        pass
                stack.append(i)
        return res
```



**找最高点，然后从左右两边遍历到中间**

```python
# 找到最高点,然后从左右两边遍历到中间  
class Solution:
    def trap(self, height: List[int]) -> int:
        if len(height) == 1:return 0
        res = 0
        high_id = 0
        high_num = height[0]
# 找到最高点
        n = len(height)
        for i in range(1,n):
            if height[i]>high_num:
                high_id = i
                high_num = height[i]
        # print(high_id)
        # print(high_num)
   
# 从左边往最高点遍历
        tmp = height[0]
        for i in range(0,high_id):
            if height[i] > tmp:
                tmp = height[i]
            else:
                res += (tmp-height[i])
# 从右边往最高点遍历     
        tmp = height[-1]
        for j in range(n-1,high_id,-1):
            if height[j] > tmp:
                tmp = height[j]
            else:
                res += (tmp-height[j])
        return res
```



**动态规划**

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        if n <= 1:return 0
        
        res = 0
        left = [height[0]]*n
        right = [height[-1]]*n
        
        # 首先用两个数组，left [i]代表第 i 列左边最高的墙的高度，right[i] 代表第 i 列右边最高的墙的高度。（一定要注意下，第 i 列左（右）边最高的墙，是不包括自身的，和 leetcode 上边的讲的有些不同）
        # 对于 left我们其实可以这样求。
        # left [i] = max(left [i-1],height[i-1])。它前边的墙的左边的最高高度和它前边的墙的高度选一个较大的，就是当前列左边最高的墙了。
        # 对于 max_right我们可以这样求。
        # right[i] = max(right[i+1],height[i+1]) 。它后边的墙的右边的最高高度和它后边的墙的高度选一个较大的，就是当前列右边最高的墙了。

        # 左端点不用盛水，跳过
        for i in range(1,n):
            left[i] = max(left[i-1],height[i-1])
        # 右端点不用盛水，跳过
        for j in range(n-1-1,0,-1): # 本来最高位置下标为n-1，但是我们从倒数第二个位置开始遍历，所以再减去1
            right[j] = max(right[j+1],height[j+1])
        # print(left)
        # print(right)
        # 数组的端点，不可能盛水，所以跳过，不用遍历
        for i in range(1,n-1):
            tmp = min(left[i], right[i])
            # 当前柱子高度比左右两边都高，则该处不能盛水，跳过
            if tmp>height[i]:
                res += (tmp-height[i])
        
        return res

```



**不用动态规划**

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        if n <= 1:return 0
        
        res = 0
        
        # 不用递归，原始计算左边的高度
        left = [height[0]]
        for i in range(1,n):
            if height[i]>left[-1]:
                left.append(height[i])
            else:
                left.append(left[-1])
        
        right = [height[-1]]
        for j in range(n-1-1,-1,-1):
            if height[j] > right[0]:
                right.insert(0,height[j])
            else:
                right.insert(0,right[0])
        
        print(left)
        print(right)
        # 数组的端点，不可能盛水，所以跳过，不用遍历
        for i in range(1,n-1):
            tmp = min(left[i], right[i])
            # 当前柱子高度比左右两边都高，则该处不能盛水，跳过
            if tmp>height[i]:
                res += (tmp-height[i])
        
        return res

```



**测试用例**

```python
输入：[0,1,0,2,1,0,1,3,2,1,2,1]
stdout:
    [0, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 3]
	[3, 3, 3, 3, 3, 3, 3, 3, 2, 2, 2, 1]
输出：6
预期结果：6
```



**不用动态规划（...）**

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        if n == 1:return 0
        
        res = 0
        # 左右两边不可能盛水，所以跳过，不遍历
        for i in range(1,n-1):
            left = 0
            for j in range(0,i):
                if height[j]>left:
                    left = height[j]
            right = 0
            for j in range(i+1,n):
                if height[j]>right:
                    right = height[j]
            
            tmp = min(right,left)
            if tmp>height[i]:
                res += (tmp-height[i])
        return res
```

