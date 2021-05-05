https://leetcode.com/problems/linked-list-random-node/

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
// 水库抽样算法
class Solution {
private:
    ListNode* head;
public:
    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    Solution(ListNode* head) : head(head) {}
    
    /** Returns a random node's value. */
    int getRandom() {
        int res = head->val;
        ListNode* node = head->next;
        int i = 2;
        while (node) {
            if ((rand() % i) == 0) res = node->val;
            node = node->next;
            ++i;
        }
        return res;
    }
};
```

