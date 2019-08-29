#### [实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)(Leetcode 208)

#### 1.题目

实现一个 Trie (前缀树)，包含 `insert`, `search`, 和 `startsWith` 这三个操作。

**示例:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```

**说明:**

- 你可以假设所有的输入都是由小写字母 `a-z` 构成的。
- 保证所有输入均为非空字符串。

#### 2.分析

​	trie树，即字典树，又称单词查找树或键树，是一种树形结构，是一种哈希树的变种。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。” 
       总体来讲，前缀树的构造过程，通过不断插入新的字符串来丰富这棵26叉树。强调注意这里是26叉树，因为每一个英文字符串中下一个字母都只能是a-z中的一种可能。 

      前缀树的功能很强大，可以做文本词频统计，例如我们在搜索框中的搜索提示，就可以利用前缀树实现。因此，前缀树基本的操作是字符串的插入，搜索，删除，查找前缀等。

```python
apple:{'a': {'p': {'p': {'l': {'e': {'end': True}}}}}}             #第一次insert，最后一个'e'存在结束'end'
app:  {'a': {'p': {'p': {'l': {'e': {'end': True}}, 'end': True}}}}#第二次insert，第二个'p'存在结束'end'

```



#### 3.代码

##### 法一

```python
class TrieNode(object):
    def __init__(self):
        self.nodes = [None]*26
        self.last = False

class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()
        

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        tree = self.root
        for i in word:
            if tree.nodes[ord(i) - ord('a')] == None:
                tree.nodes[ord(i)-ord('a')] = TrieNode()
            tree = tree.nodes[ord(i)-ord('a')]
        tree.last = True
        

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        tree = self.root
        for i in word:
            if tree.nodes[ord(i)-ord('a')]==None:
                return False
            tree = tree.nodes[ord(i)-ord('a')]
        return tree.last
        

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        tree = self.root
        for i in prefix:
            if tree.nodes[ord(i)-ord('a')] == None:
                return False
            tree = tree.nodes[ord(i)-ord('a')]
        return True
        


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

##### 法2(推荐)

```python
class Trie(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: None
        """
        node = self.root
        for char in word:
        # 没有就新建{}，有就利用char对应的{}
            node = node.setdefault(char, {})
        node["end"] = True
        
        ==================================================== 等价
        for char in word:
            if char not in node:
                node[char] = {}
            node = node[char]
        node['end'] = True
         =========================================================================   
        

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        node = self.root
        for char in word:
            if char not in node:
                return False
            node = node[char]
            
        return "end" in node
        

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        node = self.root
        for char in prefix:
            if char not in node:
                return False
            node = node[char]
        
        return True
```

