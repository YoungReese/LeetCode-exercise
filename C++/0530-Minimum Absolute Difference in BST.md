https://leetcode.com/problems/minimum-absolute-difference-in-bst/

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
    int getMinimumDifference(TreeNode* root) {
        int res = INT_MAX;
        TreeNode* prev = nullptr;
        inorder(root, prev, res);
        return res;
    }
private:
    void inorder(TreeNode* node, TreeNode*& prev, int& res) {
        if (node == nullptr) return;
        inorder(node->left, prev, res);
        if (node && prev) res = min(res, node->val - prev->val);
        prev = node;
        inorder(node->right, prev, res);  
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
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
// binary search tree with non-negative values
// so optimize it
class Solution {
public:
    int getMinimumDifference(TreeNode* root) {
        int prev = -1;
        int diff = INT_MAX;
        inorder(root, prev, diff);
        return diff;
    }
private:
    void inorder(TreeNode* node, int& prev, int& diff) {
        if (node == nullptr) return;
        inorder(node->left, prev, diff);
        if (prev >= 0) diff = min(diff, node->val - prev);
        prev = node->val;
        inorder(node->right, prev, diff);
    }
};
```

