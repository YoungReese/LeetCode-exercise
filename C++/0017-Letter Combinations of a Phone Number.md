https://leetcode.com/problems/letter-combinations-of-a-phone-number/

```c++
// O(3^n)
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.size() == 0) return {};
        vector<string> res;
        string s = "";
        helper(0, digits, s, res);
        return res;
    }
private:
    vector<string> map = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    void helper(int p, const string& digits, string& s, vector<string>& res) {
        if (p == digits.size()) {
            res.push_back(s);
            return;
        }
        for (auto c : map[digits[p] - '2']) {
            s.push_back(c);
            helper(p + 1, digits, s, res);
            s.pop_back();
        }
    }
};
```

