https://leetcode.com/problems/swap-nodes-in-pairs/

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode* newHead = head->next;
        ListNode* p = head;
        while (p && p->next) {
            ListNode* s = p->next->next; // 保存下下一个节点
            p->next->next = p;
            if (s && s->next) p->next = s->next;
            else p->next = s;
            p = s;
        }
        return newHead;
    }
};
```

