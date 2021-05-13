https://leetcode.com/problems/kth-largest-element-in-an-array/

```c++
// 最好情况：O(n)  最坏情况：O(n ^ 2)  =>  40ms
// 使用快排性质：每次 partition 位置就是其最终位置
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        bool find = false;
        qSort(nums, 0, nums.size() - 1, nums.size() - k, find);
        return nums[nums.size() - k];
    }
private:
    void qSort(vector<int>& nums, int left, int right, int partition, bool& find) {
        if (right - left + 1 < 2 || find) return;
        int pivot = nums[left];        // 将区间中的第一个元素作为 pivot
        swap(nums[left], nums[right]); // 将 pivot 藏在 right 位置
        int i = left - 1, j = right;   // 可以安全的对 [left, right - 1] 进行比较操作了
        while (i < j) {                // 采用前置 ++ 和 -- 可以避免在 if 中再次进行比较
            while (i < right && nums[++i] < pivot) {}
            while (j > 0 && nums[--j] > pivot) {}
            if (i < j) swap(nums[i], nums[j]);
        }
        swap(nums[i], nums[right]);
		if (i == partition) {
            find = true;
            return;
        }
        if (i > partition) qSort(nums, left, i - 1, partition, find);
        else qSort(nums, i + 1, right, partition, find);
    }
};
```



```java
// O(n logk)  =>  4ms
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> pq; // 维护一个 k 个元素的小顶堆，堆顶就是答案
        for (int& num : nums) {
            if (pq.size() < k) pq.push(num);
            else if (pq.top() < num) {
                pq.pop();
                pq.push(num);
            }
        }
        return pq.top();
    }
};
```

