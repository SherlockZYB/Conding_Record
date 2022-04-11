# 剑指 Offer 36. 二叉搜索树与双向链表

### 二叉搜索树与双向链表

### 原题：

### 解题方法：

解法一：

```cpp
    //对二叉搜索树进行中序遍历操作
    //始终存在相邻两个节点，该两个节点进行相互连接
    //最后把头部和尾部的结点连接起来
class Solution {
public:
    Node* treeToDoublyList(Node* root) {
        if(root == nullptr) return nullptr;
        dfs(root);
        head->left = pre;
        pre->right = head;
        return head;
    }
private:
    Node *pre, *head;
    void dfs(Node* cur) {
        if(cur == nullptr) return;
        dfs(cur->left);
        if(pre != nullptr) pre->right = cur;
        else head = cur;
        cur->left = pre;
        pre = cur;
        dfs(cur->right);
    }
};

```

### 做题小结：

针对解法一：

1. 对回溯似乎存在误区，此处严格意义上并不需要回溯，只是需要一个节点来保存上一个节点，而回溯是随着遍历层数而不断变化（此处不需要不断变化）。
2. 思路有错，之前想的是对单个节点的左右进行操作，但事实上应该是对两个节点，进行相互连接。按照我之前的思路，就需要同时存在三个节点。
