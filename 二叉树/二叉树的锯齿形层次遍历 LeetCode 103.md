### [二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)(LeetCode 103)

#### 1.题目

给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```sql lite
    3
   / \
  9  20
    /  \
   15   7
```

返回锯齿形层次遍历如下：

```
[
  [3],
  [20,9],
  [15,7]
]
```

#### 2.分析

和层次遍历一样，只不过加一个，判断语句

#### 3.代码

```python
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if root == None: return []
        res = []
        queue = [root]
        deepth = 0
        while queue:
            deepth += 1
            res_tmp = []
            queue_tmp = []      
            for node in queue:
                if deepth%2==0:
                    res_tmp.append(node.val)
                else:
                    res_tmp.insert(0,node.val)
                if node.right:
                    queue_tmp.append(node.right)
                if node.left:
                    queue_tmp.append(node.left)
            queue = queue_tmp
            res.append(res_tmp)
        return res
```

