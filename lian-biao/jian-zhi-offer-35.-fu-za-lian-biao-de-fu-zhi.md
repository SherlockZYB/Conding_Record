# 剑指 Offer 35. 复杂链表的复制

### [复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

### 原题：

请实现 `copyRandomList` 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 `next` 指针指向下一个节点，还有一个 `random` 指针指向链表中的任意节点或者 `null`。

**示例 1：**

```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**示例 2：**

```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

**示例 3：**

```
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

**示例 4：**

```
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```

**提示：**

* `-10000 <= Node.val <= 10000`
* `Node.random` 为空（null）或指向链表中的节点。
* 节点数目不超过 1000 。

**注意：**本题与主站 138 题相同：[https://leetcode-cn.com/problems/copy-list-with-random-pointer/](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

### 解题方法：

解法一：

```cpp
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head==NULL) return nullptr;
        Node* dummy = new Node(0);
        unordered_map<Node*, int> nodes;
        nodes.emplace(head, 0);
        int i = 1;  //用来记录节点对应的index
        Node* cur = head->next;
        Node* helper = new Node(head->val);
        dummy->next = helper;

        while (cur != nullptr)
        {
            nodes.emplace(cur, i++);
            helper->next = new Node(cur->val);
            cur = cur->next;
            helper = helper->next;
        }

        nodes.emplace(nullptr, i); //放入空指针在末尾
        cur = head;  //重头开始给random赋值
        helper = dummy->next;


        while (cur != nullptr)
        {
            Node* temp = dummy->next;  //用temp辅助寻找新链表中random该指向的节点,放在循环内部，以便每次寻找前都都初始化
            i = nodes[cur->random];
            while (i--)
            {
                temp = temp->next;
            }
            helper->random = temp;
            cur = cur->next;
            helper = helper->next;
        }
        return dummy->next;
    }
};
```

### 做题小结：

针对解法一：

1. 使用了一个哈希表来记录原链表中每个节点的位置，方便在新建链表时，用于找到random的位置
2. 采用先复制整个横向链表的方式（即先不管random），来保证链表节点创建完成
3. 再使用一个循环来对random进行赋值，由之前保存的哈希表来辅助找到random在新链表中应该指向的位置
4. **注：注意在最开始一定要给helper赋值（C++在函数中的变量必须要初始化）并分配内存空间，然后必须要有dummy->next=helper，才能保证后续对helper的调整能够应用到dummy对应的链表上**

解法一优化：

1. 哈希表可以直接使用\<Node\*,Node\*>来把两个链表的结点对应起来，而不需要记录位置，之后又重新去找

