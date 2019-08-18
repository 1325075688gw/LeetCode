#### [路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)(LeetCode 437)

#### 1.题目

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

**示例：**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
```

#### 2.分析

#### 3.代码

```python
def pathSum(self, root: TreeNode, sum: int) -> int:
    if root == None: return 0
    res = 0
    res += self.func(root, sum)
    
    # 这个判断可以不要，因为下个函数会判断
    if root.left:
       	# 注意这儿的调用，不是func(root.left, sum),因为这样的话，只会统计以root.left为根的左右子树的和是否满足要求。而忽略了以root.left和root.left.left root.left root.left.right加起来和为sum的情况
        res += self.pathSum(root.left, sum)
    if root.right:
        res += self.pathSum(root.right, sum)
    # print(res)
    return res

def func(self, root, sum):
    if root == None:
        return 0
    res = 0
    # 这儿不需要判断是不是叶子节点（根据题意）
    sum -= root.val
    # if not root.left and not root.right and sum == 0: 
    # 这儿出问题了，不能return 1，因为return 后，下面的代码就不执行了
    if sum == 0:
        # return 1
        res += 1
    left = self.func(root.left, sum)
    right = self.func(root.right, sum)
    return res+left+right
```