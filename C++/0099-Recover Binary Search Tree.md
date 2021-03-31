https://leetcode.com/problems/recover-binary-search-tree/

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
    void recoverTree(TreeNode* root) {
        TreeNode* preNode = nullptr;
        TreeNode* node1 = nullptr;
        TreeNode* node2 = nullptr;
        bool recovered = false;
        helper(root, preNode, node1, node2, recovered);
        if (!recovered) swap(node1->val, node2->val);
    }
private: // left - middle - right
    void helper(TreeNode* node, TreeNode*& preNode, TreeNode*& node1, TreeNode*& node2, bool& recovered) {
        if (node == nullptr || recovered) return;
        
        helper(node->left, preNode, node1, node2, recovered);
        if (preNode && preNode->val > node->val) {
            if (node1 == nullptr) {
                node1 = preNode;
                node2 = node;
            } else {
                node2 = node;
                swap(node1->val, node2->val);
                recovered = true;
            }
        }
        preNode = node;
        helper(node->right, preNode, node1, node2, recovered);
    }
};
```

