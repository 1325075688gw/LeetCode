#### [添加与搜索单词 - 数据结构设计](https://leetcode-cn.com/problems/add-and-search-word-data-structure-design/)(LeetCode 211)

#### 1.题目

设计一个支持以下两种操作的数据结构：

```
void addWord(word)
bool search(word)
```

search(word) 可以搜索文字或正则表达式字符串，字符串只包含字母 `.` 或 `a-z` 。 `.` 可以表示任何一个字母。

**示例:**

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

**说明:**

你可以假设所有单词都是由小写字母 `a-z` 组成的。

#### 2.分析



#### 3.代码

##### python代码

```python
class WordDictionary:

    def __init__(self):
        self.root = {}

    def addWord(self, word: str) -> None:
        tree = self.root
        for i in word:
            tree = tree.setdefault(i,{})
        tree['end'] = True
        
    def search(self, word: str) -> bool:
        return self.dfs(word,self.root)
    
    def dfs(self, word, root):
        if len(word) == 0:
            return 'end' in root
        if root == None: 
            return False
        for i in word:
            if i!='.':
                if i not in root:
                    return False
                # 不要忘记写return ，只写self...没有return，等于空了吹
                return self.dfs(word[1:],root[i])
            else:
                for ele in root.keys():# 可以不用keys,直接tree
                    # 这儿一定要注意，排除ele == ‘end’，这种情况，因为它没有对应一个字典，而是存储了False和True
                    if ele != 'end' and self.dfs(word[1:],root[ele]):
                        return True
                return False
```

##### C++

```
class WordDictionary:

    def __init__(self):
        self.root = {'end':False}

    def addWord(self, word: str) -> None:
        tree = self.root
        for i in word:
            tree = tree.setdefault(i,{'end':False})
        tree['end'] = True
        # for i in word:
        #     if i not in tree:
        #         tree[i] = {'isend':False}
        #     else:
        #         tree = tree[i]
        # tree['isend'] = True
        
    def search(self, word: str) -> bool:
        tree = self.root
        res = False
        for index,value in enumerate(word):
            if value not in tree:
                return False
            if (index < len(word)-1) and tree['end'] ==True:
                res = True
            tree = tree[value]
        return res

class Solution:
    def findAllConcatenatedWordsInADict(self, words: List[str]) -> List[str]:
        res = []
        tree = WordDictionary()
        for word in words:
            tree.addWord(word)
        for word in words:
            if tree.search(word):
                # print(word)
                res.append(word)
        return res
                

            
        
        
```

