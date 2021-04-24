https://leetcode.com/problems/increasing-order-search-tree/

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
    TreeNode* increasingBST(TreeNode* root) {
        TreeNode* dummyHead = new TreeNode();
        TreeNode* dummy = dummyHead;
        inorder(root, dummy);
        root = dummyHead->right;
        delete dummyHead; dummyHead = nullptr;
        return root;
    }
private:
    void inorder(TreeNode* node, TreeNode*& dummy) {
        if (node == nullptr) return;
        inorder(node->left, dummy);
        dummy->right = node;
        node->left = nullptr;
        dummy = node;
        inorder(node->right, dummy);
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
class Solution {
public:
    TreeNode* increasingBST(TreeNode* root) {
        TreeNode* prev = nullptr;
        TreeNode* newRoot = nullptr;
        inorder(root, prev, newRoot);
        return newRoot;
    }
private:
    void inorder(TreeNode* node, TreeNode*& prev, TreeNode*& newRoot) {
        if (node == nullptr) return;
        inorder(node->left, prev, newRoot);
        if (newRoot == nullptr) newRoot = node;
        
        if (prev != nullptr) {
            prev->right = node;
            node->left = nullptr;
        }
        
        prev = node;
        inorder(node->right, prev, newRoot);
    }
};
```

