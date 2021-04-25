https://leetcode.com/problems/range-sum-of-bst/

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
// any kind of traversal is fine
class Solution {
public:
    int rangeSumBST(TreeNode* root, int low, int high) {
        if (root == nullptr) return 0;
        int res = 0;
        if (root->val > low) res += rangeSumBST(root->left, low, high);
        if (root->val >= low && root->val <= high) res += root->val;
        if (root->val < high) res += rangeSumBST(root->right, low, high);
        return res;
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
    int rangeSumBST(TreeNode* root, int& low, int& high) {
        if (root == nullptr) return 0;
        int res = 0;
        if (root->val >= low && root->val <= high) res = root->val;
        res += rangeSumBST(root->left, low, high);
        res += rangeSumBST(root->right, low, high);
        return res;
    }
};
```

