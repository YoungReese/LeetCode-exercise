https://leetcode.com/problems/most-frequent-subtree-sum/

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
    vector<int> findFrequentTreeSum(TreeNode* root) {
        int count = 0;
        unordered_map<int, int> um;
        calculateTreeSum(root, count, um);
        vector<int> res;
        for (auto& pair : um) {
            if (pair.second == count) res.push_back(pair.first);
        }
        return res;
    }
private:
    int calculateTreeSum(TreeNode* node, int& count, unordered_map<int, int>& um) {
        if (node == nullptr) return 0;
        int sum = node->val + calculateTreeSum(node->left, count, um) 
                            + calculateTreeSum(node->right, count, um);
        count = max(count, ++um[sum]);
        return sum;
    }   
};
```

