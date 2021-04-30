https://leetcode.com/problems/hamming-distance/

```c++
class Solution {
public:
    int hammingDistance(int x, int y) {
        int diff = x ^ y, res = 0;
        while (diff) {
            if (diff & 1) res++;
            diff = diff >> 1;
        }
        return res;
    }
};
```

