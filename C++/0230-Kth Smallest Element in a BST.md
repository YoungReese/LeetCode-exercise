https://leetcode.com/problems/kth-smallest-element-in-a-bst/

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
// recursive
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        int res = -1;
        inorder(root, k, res);
        return res;
    }
private:
    void inorder(TreeNode* node, int& k, int& res) {
        if (node == nullptr || k < 0) return;  
        inorder(node->left, k, res);
        if ((--k) == 0) {
            res = node->val;
            return;
        }
        inorder(node->right, k, res);
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
// iteration
// 1 <= k <= n <= 10^4, so the outside while can be replaced by while (1)
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        stack<TreeNode*> stk;
        while (1) { // while (!stk.empty() || root)
            while (root) {
                stk.push(root);
                root = root->left;
            }
            root = stk.top(); stk.pop();
            if ((--k) == 0) return root->val;
            root = root->right;
        }
        return -1;
    }
};
```

