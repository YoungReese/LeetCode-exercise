https://leetcode.com/problems/construct-string-from-binary-tree/

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
// a little optimized compared to solution 2
class Solution {
public:
    string tree2str(TreeNode* t) {
        return helper(t);
    }
private:
    string helper(TreeNode* node) {
        if (node == nullptr) return "";
        
        string leftString = helper(node->left);
        string rightString = helper(node->right);
        
        string res = to_string(node->val);
        if (leftString == "" && rightString == "") return res;  
        if (rightString == "") return res + "(" + leftString + ")";       
        return res + "(" + leftString + ")" + "(" + rightString + ")";
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
    string tree2str(TreeNode* t) {
        if (t == nullptr) return "";
        return helper(t);
    }
private:
    string helper(TreeNode* node) {
        if (node == nullptr) return "()";
        
        string leftString = helper(node->left);
        string rightString = helper(node->right);
        
        if (leftString == "()" && rightString == "()") return to_string(node->val);
        string res = to_string(node->val);
        if (leftString == "()") return res + "()" + "(" + rightString + ")";
        if (rightString == "()") return res + "(" + leftString + ")";
        return res + "(" + leftString + ")" + "(" + rightString + ")";
    }    
};
```



