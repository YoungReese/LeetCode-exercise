https://leetcode.com/problems/implement-strstr/

```c++
// O(m + n)  KMP
class Solution {
public:
    int strStr(string haystack, string needle) {
        if (needle == "") return 0;
        return indexOf(haystack, needle);
    }
private:
    int indexOf(string txt, string pat) {
        int n = txt.size(), m = pat.size();
        if (n < m) return -1;
        vector<int> next = buildNext(pat, m);
        return search(txt, pat, next);
    }
    
    vector<int> buildNext(const string& pat, const int& m) {
        vector<int> next(m, -1);
        for (int j = 1, k; j < m; j++) {
            k = next[j - 1];
            while (k >= 0 && pat[k + 1] != pat[j]) {
                k = next[k];
            }
            if (pat[k + 1] == pat[j]) {
                next[j] = k + 1;
            }
        }
        return next;
    }
    
    int search(string txt, string pat, vector<int> next) {
        int n = txt.size(), m = pat.size();
        int i = 0, j = 0;
        while (i < n && j < m) {
            if (txt[i] == pat[j]) {
                i++; j++;
            } else if (j > 0) {
                j = next[j - 1] + 1;
            } else {
                i++;
            }
        }
        return j == m ? i - m : -1;
    }
};
```

