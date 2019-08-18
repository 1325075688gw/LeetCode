### [单词搜索](https://leetcode-cn.com/problems/word-search/)(Leetcode 79)(经典回溯，深度优先)

#### 1.题目

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

**示例:**

```python
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true.
给定 word = "SEE", 返回 true.
给定 word = "ABCB", 返回 false.
```

#### 2.分析

​	使用DFS，先在 board 中搜索 word 中第一个字符，再以此字符为起点进行 DFS 搜索，若搜索出的路径与 word 一致，则在网格中存在此单词。

​	为了避免循环搜索，我们还要将本轮深度优先搜索中搜索过的数字变一下，等递归回来之后再变回来。实现这个特性最简单的方法就是异或上一个特定数，然后再异或回来

​	(这儿也可以再使用一个矩阵，存放访问标志)，但是空间消耗太大。

#### 3.代码

##### python代码

```python
class Solution:
    def exist(self,board,word):
        self.path = []
        row,col = len(board),len(board[0])
        for i in range(row):
            for j in range(col):
                index = 0
                if self.func(board,index,i,j,word):
                    return True
        return False
    
    def func(self,board,index,i,j,word):
        if i<0 or j<0 or i>=len(board) or j >=len(board[0]) or (i,j) in self.path or word[index] != board[i][j]:
            return False
        # 注意这儿，字符串长度减一,因为上面的if判断，等于校验了最后个字符，比如word='ab',
        # index = 0,a
        # index = 1,时，如果能进来那么上面的if语句已经判断了b字符
        if index == len(word)-1:
            return True
        self.path.append((i,j))
        if self.func(board,index+1,i-1,j,word) or self.func(board,index+1,i,j-1,word) or self.func(board,index+1,i+1,j,word) or self.func(board,index+1,i,j+1,word):
            return True
        # 走不通，那么我们就要把这条路删除掉。回到原来的模样
        self.path.pop()
        return False
```



##### python2

```python
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        self.path = []
        
        row,col = len(board),len(board[0])
        for i in range(row):
            for j in range(col):
                if self.find(board,word,i,j):
                    return True
        return False
        
        # 经典
        # for idx,i in enumerate(board):
        #     for jdx,j in enumerate(i):
        #         if self.find(board,word,idx,jdx):
        #             return True
        # return False
    
    def find(self,board,word,i,j):
        # 这儿等于也是错的，也要退出      (i,j) in self.path 就是检验是否走重复的路，我们也可以额外定义一个标志数组
        if i<0 or j<0 or i>=len(board) or j >=len(board[0]) or (i,j) in self.path or word[0] != board[i][j]:
            return False
        
        word = word[1:]
        self.path.append((i,j))   
    
        # 减为空串，说明都匹配了
        if not word:
            return True 
          
        if self.find(board,word,i-1,j) or self.find(board,word,i,j-1) or self.find(board,word,i+1,j) or self.find(board,word,i,j+1):
            return True
        
        self.path.pop()
        return False
```

##### C++

```python
class Solution {
public:
    /**
     * @param board: A list of lists of character
     * @param word: A string
     * @return: A boolean
     */
    bool exist(vector<vector<char> > &board, string word) {
        // write your code here
        int sizeRow = board.size(), sizeStr = word.size();
        if(sizeRow <= 0 || sizeStr <= 0) {
            return false;
        }

        int sizeCol = board[0].size(), i = 0, j = 0;
        stack<pair<int, int> > path;

        for(i=0; i<sizeRow; i++) {
            for(j=0; j<sizeCol; j++) {
                if(board[i][j] == word[0]) {
                    bool isFind = DFSFind(board, word, i, j, 0);
                    if(isFind) {
                        return true;
                    }
                }
            }
        }

        return false;
    }

    bool DFSFind(vector<vector<char> > &board, string word, int i, int j, int wordStart) {
        if(wordStart == word.size()) {
            return true;
        }
        else if(i<0 || i>=board.size() || j<0 || j>= board[0].size() || 
                board[i][j]!=word[wordStart])
        {
            return false;
        } 

        board[i][j] ^= 255;
        bool result = (DFSFind(board, word, i-1, j,   wordStart+1) 
                    || DFSFind(board, word, i,   j-1, wordStart+1) 
                    || DFSFind(board, word, i+1, j,   wordStart+1) 
                    || DFSFind(board, word, i,   j+1, wordStart+1));

        board[i][j] ^= 255;
        return result;
    }
};
```

