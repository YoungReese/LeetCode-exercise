https://leetcode.com/problems/longest-substring-without-repeating-characters/

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        if (n == 0 || n == 1) return n;
        int um[256] = {0};
        int res = 0, left = 0, right = 0;
        while (right < n) {
            if (um[s[right]] == 0) {
                res = max(res, right - left + 1);
                um[s[right++]]++;
            } else {
                while (left <= right && um[s[right]] > 0) {
                    um[s[left++]]--;
                }
            }   
        }
        return res;
    }
};
```

