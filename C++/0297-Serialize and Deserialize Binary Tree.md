https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
// original => [1,-21,3,null,null,4,5]
// encode   => 1,-21,##3,4,##5,##
// decode   => [1,-21,3,null,null,4,5]
class Codec {
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string s = "";
        encodeDfs(root, s);
        cout << s << endl;
        return s;
    }
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        int index = 0;
        return decodeDfs(data, index);
    }  
private:
    void encodeDfs(TreeNode* node, string& s) {
        if (node == nullptr) {
            s += "#";
            return;
        }
        s += to_string(node->val) + ",";
        encodeDfs(node->left, s);
        encodeDfs(node->right, s);
    }
    
    TreeNode* decodeDfs(const string& s, int& index) {
        if (s[index] == '#') {
            index++;
            return nullptr;
        }
        
        int flag = 1;
        int val = 0;
        for (int n = s.size(); index < n; index++) {
            if (s[index] == '-') {
                flag = -1;
                continue;
            }
            if (s[index] != ',') {
                val = val * 10 + s[index] - '0';
            } else {
                index++;
                break;
            }
        }
        
        TreeNode* node = new TreeNode(val * flag);
        node->left = decodeDfs(s, index);
        node->right = decodeDfs(s, index);
        
        return node;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```

