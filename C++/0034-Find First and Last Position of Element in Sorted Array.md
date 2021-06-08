https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

```c++
// O(log n)  O(1)
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int first = searchFirstPosition(nums, target);
        if (first == -1) return {-1, -1};
        int last = searchLastPosition(nums, target);
        return {first, last};
    }
private:
    int searchFirstPosition(vector<int>& nums, const int& target) {
        int first = -1;
        int left = 0, right = nums.size() - 1, mid;
        while (left <= right) {
            mid = left + (right - left) / 2;
            if (nums[mid] < target) left = mid + 1;
            else {
                first = nums[mid] == target ? mid : first;
                right = mid - 1;
            }
        }
        return first;
    }
    int searchLastPosition(vector<int>& nums, const int& target) {
        int last = -1;
        int left = 0, right = nums.size() - 1, mid;
        while (left <= right) {
            mid = left + (right - left) / 2;
            if (nums[mid] > target) right = mid - 1;
            else {
                last = nums[mid] == target ? mid : last;
                left = mid + 1;
            }
        }
        return last;
    }
};
```

