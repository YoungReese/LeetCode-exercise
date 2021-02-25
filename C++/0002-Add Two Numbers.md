[Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

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
// O(n + m)  O(1)
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        if (l1 == NULL) return l2;
        if (l2 == NULL) return l1;
        
        ListNode* head = l1;
        ListNode* prev = l1;
        
        int carry = 0;
        
        while (l1 && l2) {
            carry += l1->val + l2->val;
            l1->val = carry % 10;
            carry /= 10;
            prev = l1;
            l1 = l1->next;
            l2 = l2->next;
        }
        
        if (l2) {
            l1 = prev;
            l1->next = l2;
            l1 = l1->next;
        }
        
        while (l1) {
            carry += l1->val;
            l1->val = carry % 10;
            carry /= 10;
            prev = l1;
            l1 = l1->next;
        }
        
        if (carry != 0) {
            l1 = prev;
            l1->next = new ListNode(carry);
        }
        
        return head;
    }
};
```

