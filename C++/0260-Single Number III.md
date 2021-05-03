https://leetcode.com/problems/single-number-iii/

```c++
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        if (nums.size() == 2) return nums;
        long long temp = 0;
        for (int& num : nums) temp ^= num;
        int rm = temp & (-temp);      // rightmost 1 bit in temp
        int one = 0, another = 0;
        for (int& num : nums) {
            if (rm & num) one ^= num;
            else another ^= num;
        }
        return {one, another};
    }
};
```

