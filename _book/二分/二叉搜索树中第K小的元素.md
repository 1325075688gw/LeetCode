## 二叉搜索树中第K小的元素

#### 1.题目

给定一个二叉搜索树，编写一个函数 `kthSmallest` 来查找其中第 **k** 个最小的元素。

**说明：**
你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。

**示例 1:**

```python
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 1
```

**示例 2:**

```python
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 3
```

#### 2.分析

#### 3.代码1

```python
class Solution(object):
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        arr = []
        def inder(root, arr, k):
            if root:
                inder(root.left, arr, k)
                if len(arr) >= k:
                    # print(root.val)
                    return
                arr.append(root.val)
                inder(root.right, arr, k)
        inder(root, arr, k)
        # print(arr[-1])
        # 必须这样，而不能直接在if语句返回 return arr[-1]
        return arr[-1]
```

#### 代码2

```python
class Solution(object):
    def countNodes(self, root): # 计算树的节点数
        if root == None: 
            return 0
        else:
            return 1 + self.countNodes(root.left) + self.countNodes(root.right)
    
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        # 先遍历所有的值，然后找到第k小的数字，最后利用二分搜索进行处理
        if root == None:
            return None
        leftCount = self.countNodes(root.left)
        if k < leftCount + 1:
            return self.kthSmallest(root.left, k)
        elif k == leftCount + 1:
            return root.val
        else:
            return self.kthSmallest(root.right, k - 1 - leftCount)    
        
```

> [!TIP]
>
> 计算树的节点数
>
> ```python
> def countNodes(self, root):
>     if root == None:
>         return 0
>     else:
>         return 1 + self.countNodes(root.left) + self.countNodes(root.right)
> ```

