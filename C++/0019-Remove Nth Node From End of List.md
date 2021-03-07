https://leetcode.com/problems/remove-nth-node-from-end-of-list/

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
// O(n)  sloved by two pass
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // count size of the list
        int count = 0;
        ListNode* cur = head;
        while (cur) {
            count++;
            cur = cur->next;
        }
        
        cur = head;
        n = count - n + 1;
        // not exist
        if (n <= 0) return head;
        // delete head
        if (n == 1) {
            head = head->next;
            delete cur;
            cur = NULL;
            return head;
        }
        // delete node except head
        ListNode* pre = head;
        while (--n) {
            pre = cur;
            cur = cur->next;
        }
        pre->next = cur ? cur->next : NULL;
        delete cur;
        cur = NULL;
        
        return head;
    }
};
```

**Follow up:** Could you do this in one pass?

```c++
// Yes! Use two pointer technology
// O(n)  only one pass
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* fast = head;
        for (int i = 0; i < n; i++) fast = fast->next;
        // case1: delete node is head node
        if (fast == NULL) {
            fast = head;    // record the node which should be delete
            head = head->next;
            delete fast;
            return head;
        }
        // case2: delete node is not head node
        ListNode* slow = head;
        while (fast->next) {
            fast = fast->next;
            slow = slow->next;
        }
        fast = slow->next;   // record the node which should be delete
        slow->next = slow->next->next;
        delete fast;
        fast = NULL;
        return head;
    }
};
```

