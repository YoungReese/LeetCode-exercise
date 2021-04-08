https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == p || root == q) return root;
        return helper(root, p, q);
    }
private:
    TreeNode* helper(TreeNode* node, TreeNode*& p, TreeNode*& q) {
        if (node == nullptr || node == p || node == q) return node;
        
        TreeNode* leftNode = helper(node->left, p, q);
        TreeNode* rightNode = helper(node->right, p, q);
        
        if (leftNode && rightNode) return node;
        return leftNode ? leftNode : rightNode;
    } 
};
```



```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) return root;
        TreeNode* leftNode = lowestCommonAncestor(root->left, p, q);
        TreeNode* rightNode = lowestCommonAncestor(root->right, p, q);
        if (leftNode && rightNode) return root;
        return leftNode ? leftNode : rightNode;
    }
};
```

