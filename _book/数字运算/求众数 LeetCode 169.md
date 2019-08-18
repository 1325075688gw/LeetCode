#### [求众数](https://leetcode-cn.com/problems/majority-element/)(LeetCode 169)

#### 1.题目

给定一个大小为 *n* 的数组，找到其中的众数。众数是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

**示例 1:**

```
输入: [3,2,3]
输出: 3
```

**示例 2:**

```
输入: [2,2,1,1,1,2,2]
输出: 2
```

#### 2.分析

我们一直有一个条件没有使用 众数是指在数组中出现次数大于`n/2` 的元素。那么问题就很容易了，我们可以先将nums排序，然后返回中间元素的值即可（众数的个数大于一半，排好序的nums中间元素一定是众数）

#### 3.代码

##### Counter模块

```python
    def majorityElement(self, nums):
        from collections import Counter
        most_val = Counter(nums).most_common(1)
        return most_val[0][0]
```

##### 利用`n/2`条件

```python
    # def majorityElement(self, nums):
    #     nums.sort()
    #     return nums[len(nums)//2]
        
```

##### 字典

```python
    def majorityElement(self, nums: List[int]) -> int:
        bag = {}
        for i in nums:
            if i not in bag:
                bag[i] = 1
            else:
                bag[i] += 1 
        return max(bag,key = bag.get)
```

##### 摩根投票法

```python
    def majorityElement(self, nums):
        num, count = None, 0
        for i in nums:
            if num == i:count+=1
            elif count == 0:
                num, count = i, 1
            else:
                count -= 1
        return num
```

##### 摩尔投票算法

- 假设有这样一个场景：票选村长，每人可投一票，我们将候选村长从1开始编号，村民们在票上写上候选村长的编号即可完成投票。那么最后统计的票可形成一个整型数组。那么谁是村长呢？票数过半的那个人。
- 摩尔投票算法可以快速的计算出一个数组中出现次数过半的数即大多数（majority），算法核心思想是同加，异减。我们举个例子。
- 假设数组是：[1,2,1,1,2,1]。算法步骤如下：

```python
1。当前大多数是1，得分置1
2。与当前大多数不同，得分 - 1，得分为0，当前大多数 = 1
1。与当前大多数不同，得分为0，所以设置当前大多数 1 -> 1，得分置1
1。与当前大多数相同，得分 + 1，得分为2，当前大多数 = 1
2。与当前大多数不同，得分 - 1 ，得分为1，当前大多数 = 1
1。与当前大多数相同，得分 + 1，得分为2，当前大多数 = 1
```

- 这意味着1是这个数组中出现次数过半的数。
- 可以感受得到，算法会保存一个当前大多数，和得分，当遇到一个数不是当前大多数时，得分会减一，当减到0时，大多数会发生改变，并且重置得分为1。
- 这里需要区分的是，摩尔算法不能用来得到众数（mode），例如数组：[1,1,1,2,2,3,3,4,4]，摩尔算法得出最后的结果应该是4，但4并不是众数，可是显然4也不是大多数，那是因为，大多数是指出现次数过半的数，而这个数组中没有这样的数，所以摩尔算法是是失效的，对于这种情况采取需要重新投票。