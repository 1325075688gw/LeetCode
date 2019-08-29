### 判断一棵树是不是对称的

#### 题目描述

​	请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。



```python
class Solution:
    def isSymmetrical(self, pRoot):
        # write code here
        if not pRoot:
            return True
        def func(left, right):
            if left is None and right is None:
                return True
            if left and right and left.val == right.val:
                return func(left.left, right.right) and func(left.right, right.left)
            else: # 左边有，右边没有； 右边有，左边没有
                return False
        return func(pRoot.left, pRoot.right)
```

