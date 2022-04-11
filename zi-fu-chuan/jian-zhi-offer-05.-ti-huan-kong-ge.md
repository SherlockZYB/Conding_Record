# 剑指 Offer 05. 替换空格

### [替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

### 原题：

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

**限制：**

`0 <= s 的长度 <= 10000`

### 解题方法：

解法一：

```cpp
class Solution {
public:
    string replaceSpace(string s) {
        string res="";
        for(auto ch:s)
        {
            if(ch==' ')
                res+="%20";
            else
                res+=ch;
        }
        return res;
    }
};
```

解法二：

```cpp
class Solution {
public:
    string replaceSpace(string s) {
        int count=0;
        int soldSize=s.size();
        for(auto ch:s)
        {
            if(ch==' ') count++;
        }
        s.resize(s.size()+count*2);
        int snewSize=s.size();
        for(int i=snewSize,j=soldSize;j<i;i--,j--)
        {
            if(s[j]!=' ') s[i]=s[j];
            else
            {
                s[i]='0';
                s[i-1]='2';
                s[i-2]='%';
                i-=2;         //注意变化i的大小
            }
        }
        return s;
    }
};
```

### 做题小结：

针对解法二：

1. 这道题如果使用辅助空间是很简单的，但是其实可以不用辅助空间，也达到O(n)的复杂度。
2. 先计算字符串的空格数目，按照替换后的长度对其进行扩容
3. 从后面向前进行挨个替换（**注意：此处不从前向后，因为从前向后每次都要把数组向后移，时间复杂度为O(n^2)**）

