# \*剑指 Offer 14- I. 剪绳子

### [减绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

### 原题：

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m-1]` 。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

**示例 1：**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

**示例 2:**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

**提示：**

* `2 <= n <= 58`

注意：本题与主站 343 题相同：[https://leetcode-cn.com/problems/integer-break/](https://leetcode-cn.com/problems/integer-break/)

### 解题方法：

解法一（数学推导）：

```cpp
class Solution {
public:
    int m = 1;
    int cuttingRope(int n) {//使用递归，最后都划分成若干2和若干3的乘积
        int res=1;
        if(n==3)
            return 2;
        while(n>=3)
        {
            m++;
            n=n-3;
            res*=3;
        }
        if(n==2&&m!=1)
        {
            res*=2;
        }
        if(n==1)
        {
            res/=3;
            res*=4;
        }
        return res;
    }
};
```

### 做题小结：

