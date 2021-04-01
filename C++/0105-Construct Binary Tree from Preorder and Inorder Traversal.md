https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n = preorder.size();
        if (n == 1) return new TreeNode(preorder[0]);
        return helper(preorder, 0, n - 1, inorder, 0, n - 1);
    }
private:
    TreeNode* helper(const vector<int>& preorder, int pStart, int pEnd,
                     const vector<int>& inorder, int iStart, int iEnd) {
        
        if (iStart > iEnd) return nullptr;
        if (iStart == iEnd) return new TreeNode(preorder[pStart]);
        
        TreeNode* node = new TreeNode(preorder[pStart]);
        int i = iStart;
        for (; i <= iEnd; i++) {
            if (inorder[i] == preorder[pStart]) break;
        }
        
        node->left = helper(preorder, pStart + 1, pStart + i - iStart, inorder, iStart, i - 1);
        node->right = helper(preorder, pStart + i - iStart + 1, pEnd, inorder, i + 1, iEnd);
        
        return node;
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
// use hash to accelerate it
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n = preorder.size();
        if (n == 1) return new TreeNode(preorder[0]);
        unordered_map<int, int> um;
        for (int i = 0; i < n; i++) {
            um[inorder[i]] = i;
        }
        return helper(preorder, 0, n - 1, inorder, 0, n - 1, um);
    }
private:
    TreeNode* helper(const vector<int>& preorder, int pStart, int pEnd,
                     const vector<int>& inorder, int iStart, int iEnd,
                     unordered_map<int, int>& um) {
        
        if (iStart > iEnd) return nullptr;
        if (iStart == iEnd) return new TreeNode(preorder[pStart]);
        
        TreeNode* node = new TreeNode(preorder[pStart]);
        int i = um[preorder[pStart]]; // change before O(n) to now O(1)
        
        node->left = helper(preorder, pStart + 1, pStart + i - iStart, inorder, iStart, i - 1, um);
        node->right = helper(preorder, pStart + i - iStart + 1, pEnd, inorder, i + 1, iEnd, um);
        
        return node;
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
// use hash to accelerate it
// actually we can dont use iEnd as show below
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n = preorder.size();
        if (n == 1) return new TreeNode(preorder[0]);
        unordered_map<int, int> um;
        for (int i = 0; i < n; i++) {
            um[inorder[i]] = i;
        }
        return helper(preorder, 0, n - 1, inorder, 0, um);
    }
private:
    TreeNode* helper(const vector<int>& preorder, int pStart, int pEnd,
                     const vector<int>& inorder, int iStart, unordered_map<int, int>& um) {
        
        if (pStart > pEnd) return nullptr;
        if (pStart == pEnd) return new TreeNode(preorder[pStart]);
        
        TreeNode* node = new TreeNode(preorder[pStart]);
        int i = um[preorder[pStart]]; // change before O(n) to now O(1)
        
        node->left = helper(preorder, pStart + 1, pStart + i - iStart, inorder, iStart, um);
        node->right = helper(preorder, pStart + i - iStart + 1, pEnd, inorder, i + 1, um);
        
        return node;
    }
};
```

