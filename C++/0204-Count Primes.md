https://leetcode.com/problems/count-primes/

```c++
// Count the number of prime numbers less than a non-negative number, n.
class Solution {
public:
    int countPrimes(int n) {
        if (n <= 2) return 0;
        
        vector<bool> prime(n, true);
        int count = n - 2;  // 去掉1
        for (int i = 2, k = sqrt(n); i <= k; ++i) {
            if (prime[i]) {
                for (int j = i * i; j < n; j += i) {
                    if (prime[j]) {
                        prime[j] = false;
                        --count;
                    }
                }
            }
        }
        
        return count;
    }
};
```

