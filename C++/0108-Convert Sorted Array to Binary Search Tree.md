https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return dfs(nums, 0, nums.size() - 1);
    }
private:
    TreeNode* dfs(const vector<int>& nums, int start, int end) {
        if (start > end) return nullptr;
        if (start == end) return new TreeNode(nums[start]);
        
        int mid = start + ((end - start) >> 1);
        TreeNode* node = new TreeNode(nums[mid]);
        
        node->left = dfs(nums, start, mid - 1);
        node->right = dfs(nums, mid + 1, end);
        
        return node;
    }
};
```

