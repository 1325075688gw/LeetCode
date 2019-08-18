### 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)(LeetCode 108)

#### 1.题目

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

#### 2.分析

高度差不超过一，说明是二叉搜索树

- 先取数组中间节点作为根节点，将数组分成左右部分，对数组的左右两部分采用递归的方法进行建立左右子树
- 时间复杂度（O(n)）:
- 因为这种方法只遍历了一遍数组，因此，算法的时间复杂度，是O(n)

#### 3.代码

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:    
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        # 平衡二叉树前序遍历是递增的，列表中间点是根节点
        if len(nums) < 1:
            return None
        return self.creat_BST(nums,0,len(nums)-1)
        
    def creat_BST(self, nums, left, right):
        if left <= right:
            mid = (left+right) // 2
            root = TreeNode(nums[mid])
            # print(root.val)
            root.left = self.creat_BST(nums, left, mid-1)# 递归如果有返回值,所有调用的地方必须写return,但是如果我们有变量接受了返回值，就不要return了
            root.right = self.creat_BST(nums, mid+1, right)
        else:
            root = None
        return root
```



```python
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        # 平衡二叉树前序遍历是递增的，列表中间点是根节点
        if len(nums) < 1:
            return None
        return self.creat_BST(nums,0,len(nums)-1)
        
    def creat_BST(self, nums, left, right):
        # print(nums)
        if left > right:
            return 
        mid = (left+right) // 2
        root = TreeNode(nums[mid])
        print(root.val)
        root.left = self.creat_BST(nums, left, mid-1)
        root.right = self.creat_BST(nums, mid+1, right)
        
        return root

```

