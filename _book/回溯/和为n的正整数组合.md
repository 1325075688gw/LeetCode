### 和为n的正整数组合

#### 1.题目

                # 如 n = 3
                # 输出 【1,1,1】【1，2】【3】
                # 我们只需修改candidates为【i for i in range(n+1)】
#### 2.分析

回溯

#### 3.代码

##### 可以使用重复元素

```python
    def combinationSum(self, target):
        candidates = [i for i in range(1,target+1)]
        self.res = []
        self.func(0,target, candidates,[])
        return self.res
        
    def func(self,index, target,nums,x):
        if 0 == target:
            self.res.append(x[:])
            return 
        for i in range(index,len(nums)):
            k = target-nums[i]
            if k >= 0:
                self.func(i,target-nums[i],nums,x+[nums[i]])
```

##### 不可使用重复元素

```python
    def combinationSum(self, target):
        candidates = [i for i in range(1,target+1)]
        self.res = []
        self.func(0,target, candidates,[])
        return self.res
        
    def func(self,index, target,nums,x):
        if 0 == target:
            self.res.append(x[:])
            return 
        for i in range(index,len(nums)):
            k = target-nums[i]
            if k >= 0:
            # func(i+1)
                self.func(i+1,target-nums[i],nums,x+[nums[i]])
```

