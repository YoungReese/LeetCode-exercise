https://leetcode.com/problems/binary-search-tree-iterator/

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
class BSTIterator {
public:
    BSTIterator(TreeNode* root) {
        inorder(root);
    }
    
    int next() {
        if (hasNext()) return ordered[index++];
        return -1;
    }
    
    bool hasNext() {
        if (index < ordered.size()) return true;
        return false;
    }
private:
    vector<int> ordered;
    int index = 0;
    void inorder(TreeNode* node) {
        if (node == nullptr) return;
        inorder(node->left);
        ordered.push_back(node->val);
        inorder(node->right);
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```
