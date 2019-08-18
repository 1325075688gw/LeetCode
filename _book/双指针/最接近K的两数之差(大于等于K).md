#### 1.题目

```
给定N个整数A1， A2， … ，AN，以及一个正整数K。问在所有的大于等于K的两个数的差(Ai-Aj)中，最小的差是多少。(N <= 100000)
```

#### 2.分析

```
双指针优化：
首先就是对A数组排序。比如假设排好序的A数组是：
　　A=[1, 3, 7, 8, 10, 15], K=3
这时我们枚举两个数中较小的是A[i]，较大的数是A[j]；对于A[i]来说，我们要找到最优的A[j]，也就是最小的A[j]满足A[j]-A[i]>=k
```

如下图：

- 当A[i]=1的时候，最优的A[j]=7
- 当A[i]=3的时候，最优的A[j]=7
- 当A[i]=7的时候，最优的A[j]=10
- 当A[i]=8的时候，最优的A[j]=15
- 当A[i]=10的时候，最优的A[j]=15

　　当i依次向右的时候，这个“最优的A[j]”或者不动或者向右，不会向左。换句话说，我现在已知A[i]=1的时候A[j]=7是最优的解；那当A[i]变成3的时候，A[j]我就可以从7位置向后找，不用再向前找。

![img](最接近K的两数之差(大于等于K).assets/5_4_题目_bestj.png)



#### 3.代码

**最接近K的两数之差（两数之差大于等于K）**

```python
        def func(li,key):
            li.sort()
            n = len(li)
            left, right = 0, n-1
            res = li[-1]-li[0]
            if res<key:
                print('无解')
                return
            
            # 有解的情况
            j = 0
            for i in range(n-1):
                while j <= right and li[j]-li[i]<key:
                    j += 1 
                if j <= right:
                    res = min(res, li[j]-li[i])

            print(res)
            
        li = [1, 3, 7, 8, 15]
        key = 8
        func(li, key)
```



**最接近K的两数之差 (两数之差不一定大于等于K)**

```python
        def func(li,key):
            li.sort()
            n = len(li)
            left, right = 0, n-1
            res = li[-1]-li[0]
            # if res<key:
            #     print('无解')
            #     return
            
            # 有解的情况
            j = 0
            for i in range(n-1):
                while j <= right and li[j]-li[i]<key:
                    j += 1 
                if j <= right:
                    res = min(res, li[j]-li[i],abs(li[j-1]-key))
                    if res == 0:
                        print('最小为0')
                        return
                else:
                    res = min(res, abs(li[j-1]-key))

            print(res)
            
        li = [1, 3, 7, 8, 15]
        key = 78
        func(li, key)
                    
```

