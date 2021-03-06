https://leetcode.com/problems/longest-common-prefix/

```c++
// O(nm)  O(1)
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 0) return "";
        string res = "";
        int n = strs.size();
        for (int j = 0, len = strs[0].size(); j < len; j++) {
            for (int i = 1; i < n; i++) {
                if (j >= strs[i].size() || strs[0][j] != strs[i][j]) return res;
            }
            res += strs[0][j];
        }
        return res;
    }
};
```

