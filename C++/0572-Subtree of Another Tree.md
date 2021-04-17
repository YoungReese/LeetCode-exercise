https://leetcode.com/problems/subtree-of-another-tree/

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
class Solution {
public:
    bool isSubtree(TreeNode* s, TreeNode* t) {
        if (s == nullptr) return false;
        return isEqual(s, t) || isSubtree(s->left, t) || isSubtree(s->right, t);
    }
private:
    bool isEqual(TreeNode* s, TreeNode* t) {
        if (s == t) return true;
        if (s == nullptr || t == nullptr) return false;
        return s->val == t->val && isEqual(s->left, t->left) && isEqual(s->right, t->right);
    }
};
```



