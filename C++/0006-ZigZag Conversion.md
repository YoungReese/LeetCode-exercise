https://leetcode.com/problems/zigzag-conversion/

```c++
// O(n)  O(1)
class Solution {
public:
    string convert(string s, int numRows) {
        if (s.size() < numRows || numRows == 1) return s;
        
        vector<string> tmp(numRows, "");
        bool goingDown = true;
        int row = 0;
        
        for (char c : s) {
            tmp[row] += c;
            row += goingDown ? 1 : -1;
            if (row == numRows - 1 || row == 0) goingDown = !goingDown;
        }
        
        string res = "";
        for (string e : tmp) res += e;
        
        return res;
    }
};
```

