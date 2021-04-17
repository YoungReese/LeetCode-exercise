https://leetcode.com/problems/two-sum-iv-input-is-a-bst/

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
    bool findTarget(TreeNode* root, int k) {
        vector<int> arr;
        inorder(root, arr);
        int left = 0; int right = arr.size() - 1;
        while (left < right) {
            if (arr[left] + arr[right] == k) return true;
            else if (arr[left] + arr[right] < k) left++;
            else right--;
        }
        return false;
    }
private:
    void inorder(TreeNode* node, vector<int>& arr) {
        if (node == nullptr) return;
        inorder(node->left, arr);
        arr.push_back(node->val);
        inorder(node->right, arr);
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
    bool findTarget(TreeNode* root, int k) {
        unordered_set<int> us;
        return find(root, k, us);
    }
private:
    bool find(TreeNode* node, const int& k, unordered_set<int>& us) {
        if (node == nullptr) return false;
        if (us.count(k - node->val)) return true;
        us.insert(node->val);
        return find(node->left, k, us) || find(node->right, k, us);
    }
};
```

