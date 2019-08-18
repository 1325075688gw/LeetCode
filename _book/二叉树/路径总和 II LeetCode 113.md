#### [路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)(LeetCode 113)

#### 1.题目

给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

#### 2.分析

#### 3.代码

```python
def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
    X = []
    path = []
    self.func(root, sum, path, X)
    # print(X)
    return X
def func(self, root, sum, path, X):
    if not root:
        return 
    sum -= root.val
    path.append(root.val)
    if not root.left and not root.right and sum == 0:
        X.append(path[:])
    if root.left:
        self.func(root.left, sum, path, X)
    if root.right:
        self.func(root.right, sum, path, X)
    # 从root走到叶子节点了，但是路径之和不为sum，所以向上回溯
    path.pop()
```
##### 全局变量可以这么设

```python
def pathSum(self, root, sum):
    self.res = []
    self.track = []
    self.helper(root, sum)
    return self.res

def helper(self, node, sum):
    if not node:
        return
    self.track.append(node.val)
    sum -= node.val
    if not node.left and not node.right and sum == 0:
        self.res.append(self.track[:])
    else:
        self.helper(node.left, sum)
        self.helper(node.right, sum)
    self.track.pop()
```