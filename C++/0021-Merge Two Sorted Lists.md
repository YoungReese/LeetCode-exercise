https://leetcode.com/problems/merge-two-sorted-lists/

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
// O(n) O(1) use dummy head
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr) return l2;
        if (l2 == nullptr) return l1;
        
        ListNode* dummyHead = new ListNode(-110);
        ListNode* dummy = dummyHead;
        ListNode* p1 = l1;
        ListNode* p2 = l2;
        while (p1 && p2) {
            if (p1->val <= p2->val) {
                dummy->next = p1;
                p1 = p1->next;
            } else {
                dummy->next = p2;
                p2 = p2->next;
            }
            dummy = dummy->next;
        }
        
        if (p1) {
            dummy->next = p1;
        } else {
            dummy->next = p2;
        }
        
        dummy = dummyHead->next;
        delete dummyHead;
        dummyHead = nullptr;
        return dummy;
    }
};
```

