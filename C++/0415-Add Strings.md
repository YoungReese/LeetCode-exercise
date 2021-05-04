https://leetcode.com/problems/add-strings/

```c++
class Solution {
public:
    string addStrings(string num1, string num2) {
        if (num1 == "0") return num2;
        if (num2 == "0") return num1;
        
        int i = num1.size() - 1, j = num2.size() - 1;
        int carry = 0;
        string sum = ""; 
        while (i >= 0 || j >= 0) {
            int x = i >= 0 ? num1[i--] - '0' : 0;
            int y = j >= 0 ? num2[j--] - '0' : 0;
            int curSum = x + y + carry;
            sum = to_string(curSum % 10) + sum;
            carry = curSum / 10;
        }
        if (carry) sum = to_string(carry) + sum;
        
        return sum;
    }
};
```

