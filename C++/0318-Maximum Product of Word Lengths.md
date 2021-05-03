https://leetcode.com/problems/maximum-product-of-word-lengths/

```c++
// words[i] consists only of lowercase English letters.
class Solution {
public:
    int maxProduct(vector<string>& words) {
        unordered_map<int, int> um;
        int res = 0;
        for (const string& word : words) {
            int mask = 0, len = word.size();
            for (const char& c : word) {
                mask |= 1 << (c - 'a');
            }
            um[mask] = max(um[mask], len);  // aa or a or aaa
            for (const auto& [h, l] : um) {
                if (!(mask & h)) res = max(res, len * l);
            }
        }
        return res;
    }
};
```



```c++
class Solution {
public:
    int maxProduct(vector<string>& words) {
        unordered_map<int, int> um;
        int res = 0;
        for (const string& word : words) {
            int mask = 0, len = word.size();
            for (const char& c : word) {
                mask |= 1 << (c - 'a');
            }
            um[mask] = max(um[mask], len);  // aa or a or aaa
            for (auto it = um.begin(); it != um.end(); ++it) {
                if (!(mask & it->first)) res = max(res, len * it->second);
            }
        }
        return res;
    }
};
```

