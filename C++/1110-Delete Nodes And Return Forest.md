https://leetcode.com/problems/delete-nodes-and-return-forest/

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
class Solution { // each node in the tree has a distinct value
public:
    vector<TreeNode*> delNodes(TreeNode* root, vector<int>& to_delete) {
        unordered_set<int> del(to_delete.begin(), to_delete.end());
        vector<TreeNode*> forest;
        if (root && !del.count(root->val)) forest.push_back(root);
        deleteNodes(root, del, forest);
        return forest;
    }
private:    
    void deleteNodes(TreeNode*& node, unordered_set<int>& del, vector<TreeNode*>& forest) {
        if (node == nullptr) return;
        deleteNodes(node->left, del, forest);
        deleteNodes(node->right, del, forest);
        if (del.count(node->val)) {
            if (node->left) forest.push_back(node->left);
            if (node->right) forest.push_back(node->right);
            node = nullptr;
        }
    }
};
```


