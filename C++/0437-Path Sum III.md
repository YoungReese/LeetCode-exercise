https://leetcode.com/problems/path-sum-iii/

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
// O(n logn)
class Solution {
public:
    int pathSum(TreeNode* root, int targetSum) {
        if (root == nullptr) return 0;
        return dfs(root, targetSum) 
            + pathSum(root->left, targetSum) 
            + pathSum(root->right, targetSum);
    }
private:
    int dfs(TreeNode* node, int sum) {
        if (node == nullptr) return 0;
        
        return (node->val == sum ? 1 : 0) 
            + dfs(node->left, sum - node->val) 
            + dfs(node->right, sum - node->val);
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
// O(n log n)
class Solution {
public:
    int pathSum(TreeNode* root, int targetSum) {
        if (root == nullptr) return 0;
        vector<int> path;
        int res = 0;
        dfs(root, 0, path, res, targetSum);
        return res;
    }
private:
    void dfs(TreeNode* node, int sum, vector<int>& path, int& res, const int& targetSum) {
        if (node == nullptr) return;
        
        sum += node->val;
        if (sum == targetSum) res++;
        
        path.push_back(node->val);
        int t = sum;
        for (int i = 0; i < path.size() - 1; i++) {
            t -= path[i];
            if (t == targetSum) res++;
        }
        
        dfs(node->left, sum, path, res, targetSum); 
        dfs(node->right, sum, path, res, targetSum);
        
        path.pop_back();
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
// optimiaze
// O(n)
class Solution {
public:
    int pathSum(TreeNode* root, int targetSum) {
        if (root == nullptr) return 0;
        unordered_map<int, int> um;
        um[0] = 1;
        return dfs(root, 0, um, targetSum);
    }
private:
    int dfs(TreeNode* node, int sum, unordered_map<int, int>& um, const int& targetSum) {
        if (node == nullptr) return 0;
        
        sum += node->val;
        int res = um[sum - targetSum];
        um[sum]++;
        
        res += dfs(node->left, sum, um, targetSum) 
            + dfs(node->right, sum, um, targetSum);
        
        um[sum]--;
        return res;
    }
};
```

