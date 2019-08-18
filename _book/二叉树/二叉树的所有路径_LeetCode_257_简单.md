### [二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)(LeetCode_257_简单)

#### 1.题目

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

```python
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```





#### 2.分析

- 显式回溯
- 隐式回溯
- 递归

#### 3.代码



**显式回溯**

```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        res = []
        self.func(root, [], res)
        return res
    
    def func(self, node, x, res):
        if node is None:
            return
        x.append(str(node.val))
        if node.left is None and node.right is None:
            res.append('->'.join(x))
        
        if node.left:
            self.func(node.left, x, res)
        if node.right:
            self.func(node.right, x, res)
        x.pop()
```



**隐式回溯**

```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        res = []
        if root is None:
            return []
        self.func(root, [str(root.val)], res)
        return res
    
    def func(self, node, x, res):
        if node is None:
            return
        if node.left is None and node.right is None:
            res.append('->'.join(x))
        
        if node.left:
            self.func(node.left, x+[str(node.left.val)], res)
        if node.right:
            self.func(node.right, x+[str(node.right.val)], res)
 
```



**递归**

```python
        def binaryTreePaths(self, root: TreeNode) -> List[str]:
            res = []
            # 前面先讨论递归到底的情况情况
            if root is None:
                return res

            if root.left is None and root.right is None:
                res.append(str(root.val))
                return res

            # 字符串列表
            left_paths = self.binaryTreePaths(root.left)
            for path in left_paths:
                res.append(str(root.val) + '->' + path)
            # 字符串列表
            right_paths = self.binaryTreePaths(root.right)
            for path in right_paths:
                res.append(str(root.val) + '->' + path)

            return res
```

