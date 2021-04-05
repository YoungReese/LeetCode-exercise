https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

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
    void flatten(TreeNode* root) {
        dfs(root, root);
    }
private:
    void dfs(TreeNode* node, TreeNode*& last) {
        if (node == nullptr) return;
        
        TreeNode* leftNode = node->left; 
        TreeNode* rightNode = node->right;
        if (leftNode == rightNode) {
            last = node;
            return;
        }
        
        if (leftNode) {
            node->left = nullptr;
            node->right = leftNode;
            dfs(leftNode, last);
            last->right = rightNode;
        }
        dfs(rightNode, last);
    }
};
```

