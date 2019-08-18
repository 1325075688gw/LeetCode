## 旋转字符串（LeetCode796）

#### 1.题目

给定两个字符串, `A` 和 `B`。

`A` 的旋转操作就是将 `A` 最左边的字符移动到最右边。 例如, 若 `A = 'abcde'`，在移动一次之后结果就是`'bcdea'` 。如果在若干次旋转操作之后，`A` 能变成`B`，那么返回`True`。

```
示例 1:
输入: A = 'abcde', B = 'cdeab'
输出: true

示例 2:
输入: A = 'abcde', B = 'abced'
输出: false
```

**注意：**

- `A` 和 `B` 长度不超过 `100`。

#### 2.分析

#### 3.代码

##### 3.1代码1

```python
    def rotateString(self, A: str, B: str) -> bool:
        if len(A) != len(B):
            return False
        if not A and not B:
            return True
        str_all = A*2
        return self.substr(B, str_all)
    # 判断一个串是不是另一个串的子串
    def substr(self, s1, s2):
        s1_len = len(s1)
        s2_len = len(s2)
        index = 0
        for i in range(s2_len):
            if s2[i] == s1[index]:
                index += 1
                if index == s1_len:
                    return True
            else:
                index = 0
                if s2[i] == s1[index]:
                    index += 1
        return False
```

##### 3.2代码2

```python
    def rotateString(self, A: str, B: str) -> bool:
        if len(A) != len(B):
            return False
        if not A and not B:
            return True
        return B in A*2
```

##### 3.3代码3

```python
    def rotateString(self, A: str, B: str) -> bool:
        if len(A) != len(B):
            return False
        if not A and not B:
            return True
        for i in range(0,len(A)):
            if A == B:
                return True
            A = A[1:]+A[0]
        return False
```

