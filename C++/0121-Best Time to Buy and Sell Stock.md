https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

```c++
// buy  => 表示当天持有股票的最大收益
// sell => 表示当天不持有股票的最大收益
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n < 2) return 0;
        int buy = INT_MIN, sell = 0;
        for (int i = 0; i < n; ++i) {
            buy = max(buy, -prices[i]);
            sell = max(sell, buy + prices[i]);
        }
        return sell;
    }
};
```



```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        if (n < 2) return 0;
        int buy = Integer.MIN_VALUE / 2, sell = 0;
        for (int i = 0; i < n; ++i) {
            buy = Math.max(buy, -prices[i]);
            sell = Math.max(sell, buy + prices[i]);
        }
        return sell;
    }
}
```

