https://leetcode.com/problems/single-number-ii/

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for (int i = 0; i < 32; ++i) {
            int bit = 1 << i;
            int cnt = 0;          // count the 1 in bit location
            for (int& num : nums) cnt += (num & bit ? 1 : 0);
            if (cnt % 3) res |= bit;
        }
        return res;
    }
};
```

