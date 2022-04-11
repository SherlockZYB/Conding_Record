# 剑指 Offer 58 - II. 左旋转字符串

### [左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

### 原题：

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

**限制：**

* `1 <= k < s.length <= 10000`

### 解题方法：

解法一：

```cpp
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        int slow=0;
        int fast=n;
        int soldSize=s.size();
        for(int i=0;i<n;i++)
        {
            s+=s[i];
        }
        while(fast!=s.size())
        {
            s[slow]=s[fast];
            slow++;fast++;
        }
        s.resize(soldSize);
        return s;
    }
};
```

### 做题小结：

针对解法一：

1. 使用双指针法，进行字符串数组的移动和替换

