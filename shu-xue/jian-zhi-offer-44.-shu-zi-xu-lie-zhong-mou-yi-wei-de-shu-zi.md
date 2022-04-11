# 剑指 Offer 44. 数字序列中某一位的数字

### [数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

### 原题：

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

**示例 1：**

```
输入：n = 3
输出：3
```

**示例 2：**

```
输入：n = 11
输出：0
```

**限制：**

* `0 <= n < 2^31`

注意：本题与主站 400 题相同：[https://leetcode-cn.com/problems/nth-digit/](https://leetcode-cn.com/problems/nth-digit/)

### 解题方法：

解法一：

```cpp
class Solution {
public:
    //先根据n把字符序列生成：当生成的字符序列长度小于n，就继续延长字符序列(会超时)

    //根据n本身的数值，算出之前到达了至少是几位数，再进行计算

    int findNthDigit(int n) {
        string str;
        int digit = 1;          //用digit来表示位数
        int num;                //用num来表示n对应的那个数的数值
        long long strLength = 10;//用strLength表示序列的长度,从两位数开始
        if (n < 10)             //个位数可以直接返回
            return n;
        else
        {
            while (strLength < n)  //两位数、三位数...对应的数目分别为90、900个,其字符数则为180、2700个
            {
                digit++;
                strLength += 9 * pow(10, digit - 1) * digit;
            } //此时digit就是n对应的数的位数
            strLength -= 9 * pow(10, digit - 1) * digit;
            num = pow(10, digit - 1);      //num从n对应位数的最小值开始
            while (strLength <= n)          //此时精确到数值,要用小于等于
            {
                strLength += digit;
                num++;
            }
            strLength -= digit;
            num--;
            n = n - strLength;             //此时n就表示对应数值num的第n位
        }
        str = to_string(num);
        return str[n]-'0';
    }
};
```

### 做题小结：

针对解法一：

1. 这道题用暴力是肯定会超时的，因此要想办法进行简化
2. 首先想到的就是需要先找到n对应的那个数的位数，然后再从那个位数的最小数开始，精确到n对应的数值
