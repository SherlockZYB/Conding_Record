# 剑指 Offer 13. 机器人的运动范围

### [机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

### 原题：

地上有一个m行n列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0]` 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 \[35, 37] ，因为3+5+3+7=18。但它不能进入方格 \[35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

**示例 1：**

```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2：**

```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示：**

* `1 <= n,m <= 100`
* `0 <= k <= 20`

### 解题方法：

解法一：

```cpp
class Solution {
public:

    int movingCount(int m, int n, int k) {
        vector<vector<int>> visited(m, vector<int>(n, 0));
        int raw = 0, col = 0;
        return Count(k, raw, col, m, n, visited);
    }

    int sumOfDigit(int num)
    {
        int sum = 0;
        while (num > 0)
        {
            sum += num % 10;
            num /= 10;
        }
        return sum;
    }

    int Count(int k, int raw, int col, int m, int n, vector<vector<int>>& visited)
    {
        if (raw<0 || raw>m - 1 || col<0 || col>n - 1 || sumOfDigit(raw) + sumOfDigit(col) > k|| visited[raw][col])
        {
            return 0;
        }
        visited[raw][col] = 1;
        return 1 + Count(k, raw + 1, col, m, n, visited) + Count(k, raw, col + 1, m, n, visited);
    }
};
```

### 做题小结：

针对解法一：

1. 依旧是采取dfs的方式，不能忘了添加visited数组，否则会陷入死循环
2. visited在这里是不能回溯的，因为这里是求能到达的节点数，而不是路径，如果回溯会造成节点重复计算，因此选择添加&来避免回溯。
3. 同时注意此处的搜索只需要向右向下搜索就够了，往左往上肯定都是遍历过的
