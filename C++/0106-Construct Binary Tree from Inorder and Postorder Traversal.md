https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

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
class Solution { // 左根右      左右根
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = inorder.size();
        if (n == 1) return new TreeNode(postorder[0]);
        unordered_map<int, int> um;
        for (int i = 0; i < n; i++) {
            um[inorder[i]] = i;
        }
        return helper(0, um, postorder, 0, n - 1);
    }
private:
    TreeNode* helper(int iStart, unordered_map<int, int>& um, vector<int>& post, int start, int end) {
        if (start > end) return nullptr;
        if (start == end) return new TreeNode(post[end]);
        
        TreeNode* node = new TreeNode(post[end]);
        int i = um[post[end]];
        int count = i - iStart;
        
        node->left = helper(iStart, um, post, start, start + count - 1);
        node->right = helper(i + 1, um, post, start + count, end - 1);
        
        return node;
    }
};
```

