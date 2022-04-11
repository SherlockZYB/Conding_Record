# 剑指 Offer 33. 二叉搜索树的后序遍历序列

### [二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

### 原题：

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

**示例 1：**

```
输入: [1,6,3,2,5]
输出: false
```

**示例 2：**

```
输入: [1,3,2,6,5]
输出: true
```

**提示：**

1. `数组长度 <= 1000`

### 解题方法：

解法一：

```cpp
class Solution {
public:
    bool verifyPostorder(vector<int>& postorder) {
        return helper(postorder,0,postorder.size()-1);
    }

    bool helper(vector<int>& postorder,int left,int right)
    {
        if(left>=right)   //递归结束条件
            return true;
        int root=postorder[right];
        int mid=left;
        while(postorder[mid]<root)
        {
            mid++;
        }
        int temp=mid;
        while(temp<right)
        {
            temp++;
            if(postorder[temp]<root)
                return false;
        }
        return helper(postorder,left,mid-1)&&helper(postorder,mid,right-1);   
    }
};
```

### 做题小结：

针对解法一：

1. 很遗憾这道题没有靠自己想出来，主要是用到了分治的思想，在之前构造二叉树时其实也有类似的思想
2. 如何判断不是搜索二叉树是难点之一，这个解法的思路就是看在应该大于根节点的地方是否有小于根节点的值
3. 最后递归中的right-1卡了很久，需要想到的是
