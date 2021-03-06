https://leetcode.com/problems/roman-to-integer/

```c++
// O(n)  O(1)
class Solution {
public:
    int romanToInt(string s) {
        int res = 0;
        int num1, num2;
        for (int i = s.size() - 1; i >= 0; i--) {
            num1 = charToNum(s[i]);
            num2 = (i > 0) ? charToNum(s[i - 1]) : 0;
            if (num1 > num2) {
                res += num1 - num2;
                i--;
            } else {
                res += num1;
            }
        }
        return res;
    }   
private:
    int charToNum(char c) {
        if (c == 'I') return 1;
        if (c == 'V') return 5;
        if (c == 'X') return 10;
        if (c == 'L') return 50;
        if (c == 'C') return 100;
        if (c == 'D') return 500;
        return 1000; // c == 'M'
    }
};
```

