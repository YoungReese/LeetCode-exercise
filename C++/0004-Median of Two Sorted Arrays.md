https://leetcode.com/problems/median-of-two-sorted-arrays/

```c++
// O(log(min(m, n)))  O(1)
// m1 n1 m2 n2 (m1和m2位置可互换，n1和n2位置可互换)
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size(); int n = nums2.size();
        if (m > n) return findMedianSortedArrays(nums2, nums1);
        
        int half = (m + n + 1) >> 1;
        int left = 0, right = m - 1;
        int cutA, cutB;                      // 对应切分后数字的个数
        int m1, m2, n1, n2;                  // 对应数组的中间数字 
        while(left <= right + 1) {           // left == right时还需要在计算一次cutA、cutB、m1、m2、n1、n2
            cutA = (left + right + 1) >> 1;  // 从数组1取的元素个数
            cutB = half - cutA;              // 从数组2取的元素个数
            
            m1 = (cutA == 0 ? INT_MIN : nums1[cutA - 1]);
            m2 = (cutA == m ? INT_MAX : nums1[cutA]);
            n1 = (cutB == 0 ? INT_MIN : nums2[cutB - 1]);
            n2 = (cutB == n ? INT_MAX : nums2[cutB]);
            
            if (m1 > n2) {
                right = cutA - 1;
            } else if (n1 > m2) {
                left = cutA + 1;
            } else {
                if ((m + n) & 1) return max(m1, n1);
                else return ((max(m1, n1)) + (min(m2, n2))) / 2.0;
            }
        }
        
        return -1.0;
    }
};
```

