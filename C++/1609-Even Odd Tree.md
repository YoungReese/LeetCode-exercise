https://leetcode.com/problems/even-odd-tree/

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
// O(n)
class Solution {
public:
    bool isEvenOddTree(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        TreeNode* pre;
        TreeNode* cur;
        int level = 0;
        
        while (q.size() > 0) { // 0：奇数单增   1：偶数单减
            int len = q.size();
            pre = q.front();
            q.pop();
            if ((level & 1 && pre->val & 1) || 
                ((level & 1) != 1 && (pre->val & 1) != 1)) return false;
            if (pre->left) q.push(pre->left);
            if (pre->right) q.push(pre->right);
            
            for (int i = 1; i < len; i++) {
                cur = q.front();
                q.pop();
                if (level & 1) { // 奇数层偶数单减
                    if (cur->val & 1 || cur->val >= pre->val) return false;
                } else {         // 偶数层奇数单增
                    if ((cur->val & 1) != 1 || cur->val <= pre->val) return false;
                }
                if (cur->left) q.push(cur->left);
                if (cur->right) q.push(cur->right);
                pre = cur;
            }
            level++;
        }
        
        return true;
    }
};
```

