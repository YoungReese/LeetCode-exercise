https://leetcode.com/problems/search-in-rotated-sorted-array/

```c++
// O(log n)  O(1)
// this way is better
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1, mid;
        while (left <= right) {
            mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            if (nums[left] <= nums[mid]) { // 左区间有序 => left 和 mid 指像同一个位置，也是有序的
                if (nums[left] <= target && target < nums[mid]) right = mid - 1;
                else left = mid + 1;
            } else {                       // 右区间有序
                if (nums[mid] < target && target <= nums[right]) left = mid + 1;
                else right = mid - 1;
            }
        }
        return -1;
    }
};
```



```c++
// O(log n)  O(1)
// 思路：升序部分比较好分析，target不在升序部分就只能在另一部分
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1, mid;
        while (left <= right) {
            // 先判断首尾数字是否是target
            if (nums[left] == target) return left;
            if (nums[right] == target) return right;
            // 判断中间数字是否是target
            mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            // 完全升序
            if (nums[left] < nums[right]) { // left -> mid -> right 升序
                if (nums[mid] > target) right = mid - 1;
                else left = mid + 1;
            }
            // 存在rotate，部分升序
            else if (nums[left] < nums[mid]) { // left -> mid 升序
                if (nums[mid] > target && nums[left] < target) right = mid - 1;
                else left = mid + 1;
            } else {                           // mid -> right 升序
                if (nums[mid] < target && nums[right] > target) left = mid + 1;
                else right = mid - 1;
            }           
        }
        return -1;
    }
};
```



```c++
// O(n)  O(1)
class Solution {
public:
    int search(vector<int>& nums, int target) {
        for (int i = 0, n = nums.size(); i < n; i++) {
            if (nums[i] == target) return i;
        }
        return -1;
    }
};
```

