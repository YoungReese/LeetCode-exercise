https://leetcode.com/problems/integer-to-roman/

```c++
// O(log num)  O(1)
class Solution {
public:
    string intToRoman(int num) {
        string res;
        int cnt;
        if (num >= 1000) {
            cnt = num / 1000;
            solve(cnt, "M", res);
            num %= 1000;
        }
        if (num >= 900) {
            res += "CM";
            num -= 900;
        }
        if (num >= 500) {
            res += "D";
            num -= 500;
        }
        if (num >= 400) {
            res += "CD";
            num -= 400;
        }
        if (num >= 100) {
            cnt = cnt = num / 100;
            solve(cnt, "C", res);
            num %= 100;
        }
        if (num >= 90) {
            res += "XC";
            num -= 90;
        }
        if (num >= 50) {
            res += "L";
            num -= 50;
        }
        if (num >= 40) {
            res += "XL";
            num -= 40;
        }
        if (num >= 10) {
            cnt = cnt = num / 10;
            solve(cnt, "X", res);
            num %= 10;
        }
        if (num >= 9) {
            res += "IX";
            num -= 9;
        }
        if (num >= 5) {
            res += "V";
            num -= 5;
        }
        if (num >= 4) {
            res += "IV";
            num -= 4;
        }
        solve(num, "I", res);
            
        return res;
    }
private:
    void solve(int cnt, string symbol, string& res) {
        while (cnt--) {
            res += symbol;
        }
    }
};
```

