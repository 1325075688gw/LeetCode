## [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)(LeetCode 124)

#### 1.题目

给定一个**非空**二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径**至少包含一个**节点，且不一定经过根节点。

**示例 1:**

```
输入: [1,2,3]

       1
      / \
     2   3

输出: 6
```

**示例 2:**

```
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```

#### 2.分析

#### 3.代码

```python
class Solution:
    def maxPathSum(self, root):
        self.re = float('-inf')
        self.func(root)
        return self.re
    def func(self,root):
        if root == None:
            return 0
        left = max(0,self.func(root.left))
        right = max(0,self.func(root.right))
        self.re = max(self.re,root.val + left + right)
        return max(root.val,root.val + max(right,left))
```





