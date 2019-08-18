#### [路径总和](https://leetcode-cn.com/problems/path-sum/)(LeetCode 112)

#### 1.题目

给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

**说明:** 叶子节点是指没有子节点的节点。

**示例:** 
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

返回 `true`, 因为存在目标和为 22 的根节点到叶子节点的路径 `5->4->11->2`。

#### 2.分析



#### 3.代码

```python
def hasPathSum(self, root: TreeNode, sum: int) -> bool:
    if not root:
        return False
    # 如果当前节点是叶子节点,且路径之和等于sum
    if not root.left and not root.right and root.val == sum:
        return True
    else:
        return self.hasPathSum(root.left,sum-root.val) or self.hasPathSum(root.right,sum-root.val)
    return False
```