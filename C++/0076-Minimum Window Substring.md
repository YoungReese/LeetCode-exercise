https://leetcode.com/problems/minimum-window-substring/

```c++
class Solution {
public:
    string minWindow(string s, string t) {
        vector<bool> exist(128, false);
        vector<int> count(128, 0);
        // 先统计 t 中的字符情况
        for (char e : t) {
            exist[e] = true;
            ++count[e];
        }
        // 移动滑动窗口，不断更改统计数据
        int left = 0, cnt = 0, minLen = s.size() + 1, minLenLeft = 0;
        for (int right = 0, n = s.size(); right < n; ++right) {
            if (exist[s[right]]) {
                if (--count[s[right]] >= 0) ++cnt;
                // 若目前滑动窗口已包含T中全部字符，则尝试将 left 右移，在不影响结果的情况下获得最短子字符串
                while (cnt == t.size()) {
                    if (right - left + 1 < minLen) {
                        minLenLeft = left;
                        minLen = right - left + 1;
                    }
                    if (exist[s[left]] && ++count[s[left]] > 0) --cnt;
                    ++left;
                }
            }
        }
        
        return minLen > s.size() ? "" : s.substr(minLenLeft, minLen);
    }
};
```

