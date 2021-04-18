https://leetcode.com/problems/maximum-binary-tree/

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
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        return helper(nums, 0, nums.size() - 1);
    }
private:
    TreeNode* helper(vector<int>& nums, int start, int end) {
        if (start == end) return new TreeNode(nums[start]);
        if (start > end) return nullptr;
        int maxVal = INT_MIN;
        int p;
        for (int i = start; i <= end; i++) {
            if (maxVal < nums[i]) {
                maxVal = nums[i];
                p = i;
            }
        }
        TreeNode* node = new TreeNode(nums[p]);
        node->left = helper(nums, start, p - 1);
        node->right = helper(nums, p + 1, end);
        return node;
    }
};
```



```c++
// All integers in nums are unique.
// 维护一个栈底到栈顶的单调递减栈
class Solution {
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        vector<TreeNode*> stk; // 数组模拟栈
        for (int i = 0, n = nums.size(); i < n; i++) {
            TreeNode* node = new TreeNode(nums[i]);
            while (!stk.empty() && nums[i] > stk.back()->val) {
                node->left = stk.back();                // 保证接到左边最大的
                stk.pop_back();
            }
            if (!stk.empty()) stk.back()->right = node; // 保证接到右边最大的
            stk.push_back(node);
        }
        return stk[0];
    }
};
```

