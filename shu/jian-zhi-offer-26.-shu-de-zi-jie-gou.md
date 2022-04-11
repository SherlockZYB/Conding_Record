# 剑指 Offer 26. 树的子结构

### [树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

### 原题：

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:\
&#x20;给定的树 A:

&#x20;    `3`\
&#x20;    `/ \`\
&#x20;   `4   5`\
&#x20;  `/ \`\
&#x20; `1   2`\
&#x20;给定的树 B：

&#x20;  `4` \
&#x20;  `/`\
&#x20; `1`\
&#x20;返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

**示例 1：**

```
输入：A = [1,2,3], B = [3,1]
输出：false
```

**示例 2：**

```
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```

**限制：**

`0 <= 节点个数 <= 10000`

### 解题方法：

解法一：

```cpp
class Solution {
public:
    bool flag = false;
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if (A == NULL || B == NULL) return false;
        queue<TreeNode*> que;
        que.push(A);
        while (!que.empty())
        {
            TreeNode* node = que.front();
            que.pop();
            if (node->val == B->val)
            {
                flag = isSame(node, B);
                if (flag)
                    return true;
            }
            if (node->left != NULL) que.push(node->left);
            if (node->right != NULL) que.push(node->right);
        }
        return false;
    }

    bool isSame(TreeNode* A, TreeNode* B)
    {
        if (A == NULL && B == NULL)
            return true;
        else if (A == NULL && B != NULL)
        {
            return false;
        }
        else if (A != NULL && B == NULL)
        {
            return true;
        }
        if (A->val != B->val)
            return false;

        return isSame(A->left, B->left) && isSame(A->right, B->right);
    }
};

//简化后的方法
class Solution {
public:
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if (A == NULL || B == NULL) return false;
        if(isSame(A,B))
            return true;
        return isSubStructure(A->left,B)||isSubStructure(A->right,B);
    }

    bool isSame(TreeNode* A, TreeNode* B)
    {
        if (B == NULL)
            return true;
        else if (A == NULL || A->val != B->val)
        {
            return false;
        }
        return isSame(A->left, B->left) && isSame(A->right, B->right);
    }
};
```

### 做题小结：

针对解法一：

1. 很简单的思路，首先找到A中与B根相等的节点，然后从当前节点开始判断是否两棵树相等。
2. 要注意的是B不一定要包含到叶结点，在A内部也可以
3. 为了简化思路，A使用了队列的方式来遍历，但是可以考虑到使用递归
4. 在辅助函数中有很多条件判断都可以简化
5. （简化后的方法放在后面）
