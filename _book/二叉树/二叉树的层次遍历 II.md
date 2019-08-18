## 二叉树的层次遍历 II

#### 1.题目

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```python
    3
   / \
  9  20
    /  \
   15   7
```

返回其自底向上的层次遍历为：

```python
[
  [15,7],
  [9,20],
  [3]
]
```

#### 2.分析

#### 3.代码

```python
class Solution:
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
        res = []
        if root == None:
            return res
        queue = [root]
        while queue:
            queue_tmp = []
            res_tmp = []
            for node in queue:
                res_tmp.append(node.val)
                if node.left:
                    queue_tmp.append(node.left)
                if node.right:
                    queue_tmp.append(node.right)
            queue = queue_tmp
            res.insert(0, res_tmp)
        return res
```

