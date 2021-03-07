https://leetcode.com/problems/remove-duplicates-from-sorted-array/

```c++
// O(n)  O(1)
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int len = nums.size(); 
        int index = 0;
        for (int i = 1, n = nums.size(); i < n; i++) {
            if (nums[i] == nums[index]) {
                len--;
            } else {
                nums[++index] = nums[i];
            }
        }
        return len;
    }
};
```

