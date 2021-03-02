```c++
// 123 => 321
// 3,12
// 32,1
// 321,0
// INT_MIN = -2147483648
// INT_MAX =  2147483647
// 因为INT_MIN和INT_MAX的个位8和7都不能作为反转数字的高位，
// 所以可以忽略这种反转后可能的数字越界问题，统一变成正数来计算
// O(n)  O(1)
class Solution {
public:
    int reverse(int x) {
        if (x == 0 || x == INT_MIN) return 0;
        if (x < 0) return reverse(-1 * x) * -1;

        int res = 0;
        const int LIMIT = INT_MAX / 10;
        
        int body;  // 个位以上（不包含个位）
        int digit; // 个位
        while (x != 0) {
            if (res > LIMIT) return 0;
            if ((body = res * 10) > INT_MAX - (digit = x % 10)) return 0;
            res = body + digit;
            x /= 10;   
        }
        
        return res;
    }
};
```

