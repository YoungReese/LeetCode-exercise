https://leetcode.com/problems/merge-k-sorted-lists/

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        int k = lists.size();
        priority_queue<ListNode*, vector<ListNode*>, Comp> pq; // 复杂类型的小顶堆
        for (auto& head : lists) {
            if (head) pq.push(head);
        }
        ListNode* dummyHead = new ListNode();
        ListNode* dummy = dummyHead;
        while (!pq.empty()) {
            dummy->next = pq.top(); pq.pop();
            dummy = dummy->next;
            if (dummy->next) pq.push(dummy->next);
        }
        dummy = dummyHead->next;
        delete dummyHead;
        dummyHead = nullptr;
        return dummy;
    }
private:
    struct Comp { // 复杂类型的比较需要实现一个仿函数
        bool operator() (ListNode*& l1, ListNode*& l2) {
            return l1->val > l2->val;
        }
    };     
};
```

