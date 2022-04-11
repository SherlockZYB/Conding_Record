# 剑指 Offer 12. 矩阵中的路径

矩阵中的路径

### 原题：

### 解题方法：

解法一（暴力）：

```cpp
class Solution {
public:
    bool flag = false;
    bool exist(vector<vector<char>>& board, string word) {
        vector<vector<int>> visited(board.size(),vector<int>(board[0].size(),0));
        
        for (int i = 0; i < board.size(); i++)
        {
            for (int j = 0; j < board[0].size(); j++)
            {
                if (board[i][j] == word[0])
                {
                    if (check(board, word, i, j, 1, visited))
                        return true;
                }
            }
        }
        return false;
    }

    bool check(vector<vector<char>>& board, string word, int posx, int posy, int k, vector<vector<int>> visited)
    {
        
        if (visited[posx][posy])
        {
            return false;
        }
        visited[posx][posy] = 1;
        if (k == word.size())
        {
            return true;
        }
        if (posx > 0 && board[posx - 1][posy] == word[k])  //上
        {
            flag = check(board, word, posx - 1, posy, k + 1, visited);
            if (flag)
                return true;
        }
        if (posx < board.size() - 1 && board[posx + 1][posy] == word[k]) //下
        {
            flag = check(board, word, posx + 1, posy, k + 1, visited);
            if (flag)
                return true;
        }
        if (posy > 0 && board[posx][posy - 1] == word[k]) //左
        {
            flag = check(board, word, posx, posy - 1, k + 1, visited);
            if (flag)
                return true;
        }
        if (posy < board[0].size() - 1 && board[posx][posy + 1] == word[k])  //右
        {
            flag = check(board, word, posx, posy + 1, k + 1, visited);
            if (flag)
                return true;
        }
        return false;
    }

};
```

```cpp
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        rows = board.size();
        cols = board[0].size();
        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(dfs(board, word, i, j, 0)) return true;
            }
        }
        return false;
    }
private:
    int rows, cols;
    bool dfs(vector<vector<char>>& board, string word, int i, int j, int k) {
        if(i >= rows || i < 0 || j >= cols || j < 0 || board[i][j] != word[k]) return false;
        if(k == word.size() - 1) return true;
        board[i][j] = '\0';
        bool res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) || 
                      dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i , j - 1, k + 1);
        board[i][j] = word[k];
        return res;
    }
};

```

### 做题小结：

针对解法一：

1. 简直折磨，有很多需要注意的细节的地方：
   1. visited不要引用，因为从每个点开始都是重新去遍历
   2. 要考虑数组中元素有重复，所以肯定要把重复的每一个初始点都拿来遍历
   3. 不要使用else if，也不要在if中直接return，因为这样都会导致走了一条路径后不去走其他路径
   4. 使用flag就是为了避免直接return，但是当flag为true时要马上return，不然后面flag可能就又被覆盖了，所以才在每个if里面判断flag
2. 总之这种方法效率极低，时间复杂度和空间复杂度都高

针对解法二：

1. 其实思路完全一样，就是dfs+剪枝，但是有很多很妙的简化
2. 首先在辅助函数的前面判断是否越界，省的再挨个检查是否越界
3. 其次直接用||来判断四个方向是否存在一个可行的
4. 使用"\0"临时赋值board来判断是否遍历，省去了visited数组的空间，之后在把board赋值回来
