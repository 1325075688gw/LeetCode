### [有序数组的平方](https://leetcode-cn.com/problems/squares-of-a-sorted-array/)(LeetCode_977)

#### 1.题目

给定一个按非递减顺序排序的整数数组 `A`，返回每个数字的平方组成的新数组，要求也按非递减顺序排序。

**示例 1：**

```
输入：[-4,-1,0,3,10]
输出：[0,1,9,16,100]
```

**示例 2：**

```
输入：[-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

**提示：**

```python
 1 <= A.length <= 10000
 -10000 <= A[i] <= 10000
 A 已按非递减顺序排序。
```



#### 2.分析

```python
因为数组 A 已经排好序了， 所以可以说数组中的负数已经按照平方值降序排好了，数组中的非负数已经按照平方值升序排好了。

举一个例子，若给定数组为 [-3, -2, -1, 4, 5, 6]，数组中负数部分 [-3, -2, -1] 的平方为 [9, 4, 1]，数组中非负部分 [4, 5, 6] 的平方为 [16, 25, 36]。我们的策略就是从前向后遍历数组中的非负数部分，并且反向遍历数组中的负数部分。
```

- 两种双指针方法



#### 3.代码



**二分法：查找距离某个元素最近的位置 （如果存在该元素，就输出该元素位置）（此处查找0元素）**

当前数组有序

```python

        li = [-5,-3,-1,2,3,6,7]

        def func(li):
            left,right = 0,len(li)-1

            while left <= right:
                mid = (left+right)//2
                if li[mid]<0:
                    left = mid+1
                elif li[mid]>0:
                    right = mid-1
                else:
                    print('有相等元素,最近下标为',mid)
                    return
            print(left,right)
            # 如果没有相等元素，最后left>right,且left=right+1
            if li[left]-0 > 0-li[right]:
                print("没有相等，最近下标为",right)
                return
            else:
                print('没有相等，最近下标为',left)
                return 
                
        func(li)
        
```



**普通法查找**

```python
        li = [-5,-3,-1,0,2,3,6,7]
        def func(li):
            A = li[:]
            left, right = 0, len(A)-1
            if A[0]>=0:
                print('最近下标为',0)
                return
            while left<=right:
                while left < right and A[left]<0:
                    left += 1
                print(left)
                if A[left] == 0:
                    print('有相等元素,下标为',left)
                    return
                if 0-li[left-1]>li[left]-0:
                    print("没有相等，最近下标为",left)
                    return 
                else:
                    print('没有相等，最近下标为',left-1)
                    return
        func(li)
```





**找到离0最近的值，向两边遍历 (找0时候用的是二分法查找，因为0应该在中间附近，二分法查找更快)**

```python
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        n = len(A)
        left, right = 0, n-1
        if n == 1:
            return [A[0]**2]
        
        def func(li, left, right):
            while left <= right:
                mid = (left+right)//2
                if li[mid] > 0:
                    right = mid-1
                elif li[mid] < 0:
                    left = mid + 1
                else:
                    return mid
            # 如果没有相等元素，最后left>right,且left=right+1  
            if li[left]-0 > 0-li[right]:
                return right
            return left
        res = []
        if A[0] < 0:
            mid = func(A, left, right)
        else:
            mid = 0
        res.append(A[mid]**2)
        i, j = mid-1, mid+1
        while left<=i and j<=right:
            if -A[i] < A[j]:
                res.append(A[i]**2)
                i -= 1
            else:
                res.append(A[j]**2)
                j += 1
        while left<=i:
            res.append(A[i]**2)
            i -= 1
        while j<=right:
            res.append(A[j]**2)
            j += 1
        return res
```



**两边向中间遍历 **

```python
class Solution(object):
    def sortedSquares(self, A):
        left, right = 0, len(A)-1
        # 先定义好res,后面再相应位置修改res里面的值,而不是res = [],然后一个个添加元素,因为从两边向中间遍历,添加的元素从大到小,如果我们用res.append(...)，则最后需要res.resverse().如果添加元素时候，res.insert(0,...)则每次添加元素,其实内部都有大量操作(当前元素向后移位)。所以我们先定义好res.直接修改相应位置
        res = [0] * (right+1)
        cur = right
        while left<=right:
            if -A[left] < A[right]:
                res[cur] = A[right]**2
                right -= 1
                cur -= 1
            else:
                res[cur] = A[left]**2
                left += 1
                cur -= 1
        return res
```

