# \*剑指Offer 04. 二维数组中的查找

### [二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

### 原题：

在一个 n \* m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

**限制：**

`0 <= n <= 1000`

`0 <= m <= 1000`

**注意：**本题与主站 240 题相同：[https://leetcode-cn.com/problems/search-a-2d-matrix-ii/](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)

### 解题方法：

解法一：

```cpp
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if (matrix.empty()) return false;
        if (matrix[0].empty()) return false;
        int up_bound = 0, down_bound = 0;
        while (matrix[up_bound][matrix[up_bound].size() - 1] < target&&up_bound<matrix.size()-1)
        {
            up_bound++;
        }

        while (matrix[down_bound][0] < target && down_bound<matrix.size()-1 )
        {
            down_bound++;
        }

        for (int i = up_bound; i <= down_bound; i++)
        {
            int left = 0, right = matrix[i].size() - 1;
            while (left <= right)
            {
                int mid = left + (right - left) / 2;
                if (matrix[i][mid] < target)
                {
                    left = mid + 1;
                }
                else if (matrix[i][mid] > target)
                {
                    right = mid - 1;
                }
                else
                {
                    return true;
                }
            }
        }
        return false;
    }


};
```

### 做题小结：

针对解法一：

1. 采用暴力的方式，只是在暴力中，我又使用了二分来一定程度上的时间复杂度。
