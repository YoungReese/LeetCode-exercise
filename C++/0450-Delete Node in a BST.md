https://leetcode.com/problems/delete-node-in-a-bst/

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
    TreeNode* deleteNode(TreeNode* root, int& key) {
        if (root == nullptr) return nullptr;
        if (root->val > key) root->left = deleteNode(root->left, key);
        else if (root->val < key) root->right = deleteNode(root->right, key);
        else {
            if (!root->left || !root->right) {
                TreeNode* leftNode = root->left;
                TreeNode* rightNode = root->right;
                delete root;
                root = nullptr;
                return leftNode ? leftNode : rightNode;
            }

            root->val = getRightMinVal(root->right);
            root->right = deleteNode(root->right, root->val);
        }
        return root;
    }
private:
    int getRightMinVal(TreeNode* node) {
        while (node->left) node = node->left;
        return node->val;
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
// optimized but not necessary, because it becomes a little complex 
// and the running time is same as the solution above !
class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int& key) {
        if (root == nullptr) return nullptr;
        if (root->val > key) root->left = deleteNode(root->left, key);
        else if (root->val < key) root->right = deleteNode(root->right, key);
        else {
            if (!root->left || !root->right) {
                TreeNode* leftNode = root->left;
                TreeNode* rightNode = root->right;
                delete root;
                root = nullptr;
                return leftNode ? leftNode : rightNode;
            }

            TreeNode* parent = root;
            TreeNode* rightMinNode = getRightMinNode(root->right, parent);
            root->val = rightMinNode->val;
            
            if (parent != root) {
                parent->left = deleteNode(parent->left, root->val);
            } else {
                root->right = deleteNode(root->right, root->val);
            }
        }
        return root;
    }
private:
    TreeNode* getRightMinNode(TreeNode* node, TreeNode*& parent) {
        while (node->left) {
            parent = node;
            node = node->left;
        }
        return node;
    }
};
```

