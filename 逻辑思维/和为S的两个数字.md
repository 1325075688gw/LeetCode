### 和为S的两个数字



#### 1.题目

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

##### 输出描述:

```
对应每个测试案例，输出两个数，小的先输出。
```

#### 2.分析

- 我们要记住：两个数和为定值，那么这两个数差越大，这两个数的乘积就越小


- 可以用二分法，
- 可以用回溯
- 可以用双指针法

#### 3.代码



**双指针法**

```python
class Solution:
    def FindNumbersWithSum(self, array, tsum):
        # write code here
        l,r=0,len(array)-1
        
        for i in range(r+1):
            tmp = tsum-array
            
        def func():
            while 1<r:
                if array[l]+array[r]>tsum:
                    r-=1
                elif array[l]+array[r]<tsum:
                    l+=1
                else:
                    return[array[l],array[r]]
            return []  
```



**回溯**

```python
# -*- coding:utf-8 -*-
class Solution:
    def FindNumbersWithSum(self, array, tsum):
        # write code here
        if not array:
            return []
        X = []
        x = []
 
 
        def func(X, x, array, target, index):
            if target == 0 and len(x) == 2:
                X.append(x[:])
                return
            for i in range(index, len(array)):
                tmp = target - array[i]
                if tmp >= 0:
                    func(X, x + [array[i]], array, target - array[i], index + 1)
 
        func(X, x, array, tsum, 0)
        if not X:
            return X
         
        res = 0
        resu = X[0]
        for i in X:
            if i[0]*i[1] < res:
                resu = i
        sorted(resu)
        return resu

```





**双指针**

```python
# -*- coding:utf-8 -*-
class Solution:
    def FindNumbersWithSum(self, array, tsum):
        # write code here
        def func(array, tsum):
            if not array:
                return []
            left, right = 0, len(array) -1
            cur = array[0]+array[right]
            while left < right:
                if cur == tsum:
                    return [array[left], array[right]]
                elif cur > tsum:
                    cur -= array[right]
                    right -= 1
                    cur += array[right]
                elif cur < tsum:
                    cur -= array[left]
                    left += 1
                    cur += array[left]
            return []
 
        return func(array, tsum)
```

