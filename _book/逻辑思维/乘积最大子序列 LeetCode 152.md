#### [乘积最大子序列](https://leetcode-cn.com/problems/maximum-product-subarray/)(LeetCode 152)

#### 1.题目

给定一个整数数组 `nums` ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。

**示例 1:**

```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```

**示例 2:**

```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```

#### 2.分析

- 一种方法类似于最大前缀和
- 另外一种方法，我们要保存前面走过的路，里面的最大最小值，因为这是乘法，乘法的话，会出现最大值，是由两个负数乘起来的。但是负数是最小的

#### 3.代码

##### 最大前缀和

```ython
    # 先计算从左到右的相乘的最大值，再计算从右到左的最大值；再将两组最大值相比
    # 
    def maxProduct(self, A):
        B = A[::-1]
        for i in range(1, len(A)):
            # 输入[-3,0,1,-2]
            # 不加 or 1，输出[-3, 0, 0, 0] [-2, -2, 0, 0]
            # 所以我们要把A【i】等于0时，置为1
            A[i] *= (A[i - 1] or 1)
            B[i] *= (B[i - 1] or 1)
        print(A,B)
        return max(max(A),max(B))
```

##### 保留前面计算过的最大最小值

```python
    def maxProduct(self, nums: List[int]) -> int:
        #  由于有正负，所以每次相乘完毕后，应该保留最大和最小值，也就是最大正数，最小负数
        maxnum = nums[0]
        minnum = nums[0]
        res = nums[0]
        for i in nums[1:]:
            print(i)
            maxnum_temp = maxnum
            minnum_temp = minnum
           # 1,-2,i=3，这一次来的数是i=3，则这次的最大，应该就是它自己，不需要乘以前面的最大或者最小
            maxnum = max(i, i*maxnum_temp, i*minnum_temp)
            minnum = min(i, i*maxnum_temp, i*minnum_temp)
            res = max(res,maxnum)
        return res
```



