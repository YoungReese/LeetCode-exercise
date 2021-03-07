https://leetcode.com/problems/remove-element/

```c++
// O(n)  O(1)
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int len = nums.size();
        int index = 0;
        for (int i = 0, n = nums.size(); i < n; i++) {
            if (nums[i] == val) {
                len--;
            } else {
                nums[index++] = nums[i];
            }
        }
        return len;
    }
};
```

