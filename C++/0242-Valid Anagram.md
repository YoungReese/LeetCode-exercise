https://leetcode.com/problems/valid-anagram/

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int> freq(26, 0);
        for (char& c : s) ++freq[c - 'a'];
        for (char& c : t) --freq[c - 'a'];
        for (int& e : freq) {
            if (e != 0) return false;
        }
        return true;
    }
};
```



```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) return false;
        vector<int> freq(26, 0);
        for (int i = 0, n = s.size(); i < n; ++i) {
            ++freq[s[i] - 'a'];
            --freq[t[i] - 'a'];
        }
        for (int& e : freq) {
            if (e != 0) return false;
        }
        return true;
    }
};
```

