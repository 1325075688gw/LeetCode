### [平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)(LeetCode_110)

#### 1.题目

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

- 一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

**示例 1:**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。

**示例 2:**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

返回 `false` 。



#### 2.分析

- 对于二叉树，很多题既要判断根节点，还有判断左节点，右节点，这个题也是，如果只判断根节点，就会出错



#### 3.代码



```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        # write code here
        if not root:
            return True
        def func(node):
            if node is None:
                return 0
            return max(func(node.left),func(node.right))+1
        
        return abs(func(root.left)-func(root.right))<=1 and self.isBalanced(root.left) and self.isBalanced(root.right)
```

