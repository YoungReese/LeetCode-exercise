https://leetcode.com/problems/longest-substring-without-repeating-characters/

```c++
// O(2n) => O(n)  O(1)
// simple slide window, easy to understand
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



```c++
// O(n)  O(1)
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        if (n == 0 || n == 1) return n;
        int index[256] = {0};             // 改变使之成为map的作用,记录该元素的位置，即角标值+1，区分0，0表示没有
        int res = 0, left = 0, right = 0; // [left...right]没有重复子串
        while (right < n) {
            left = max(left, index[s[right]]);
            res = max(res, right - left + 1);
            index[s[right++]] = right + 1;
        }
        return res;
    }
};
```

