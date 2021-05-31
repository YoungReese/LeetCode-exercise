https://leetcode.com/problems/isomorphic-strings/

```c++
// 判断两个字符串是否同构（所有出现的字符都必须替换为另一个字符，同时保留字符的顺序）
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        vector<int> firstIndexInS(128, 0), firstIndexInT(128, 0);
        for (int i = 0, n = s.size(); i < n; ++i) {
            if (firstIndexInS[s[i]] != firstIndexInT[t[i]]) return false;
            firstIndexInS[s[i]] = firstIndexInT[t[i]] = i + 1;
        }
        return true;
    }
};
```

