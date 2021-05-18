https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/

```c++
// 这里使用了降维
// buy[j]  => 表示当天进行的是第 j 次交易持有股票时的收益
// sell[j] => 表示当天进行的是第 j 次交易不持有股票时的收益
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        if (n < 2) return 0;
        if ((n >> 1) <= k) return maxProfitByGreedy(prices);
        vector<int> buy(k + 1, INT_MIN / 2);
        vector<int> sell(k + 1, 0);
        
        for (int i = 1; i <= n; ++i) {
            for (int j = 1; j <= k; ++j) {
                buy[j] = max(buy[j], sell[j - 1] - prices[i - 1]);
                sell[j] = max(sell[j], buy[j] + prices[i - 1]);
            }
        }
        return sell[k];
    }
private:
    int maxProfitByGreedy(vector<int>& prices) {
        int res = 0;
        for (int i = 1, n = prices.size(); i < n; ++i) {
            if (prices[i] > prices[i - 1]) res += (prices[i] - prices[i - 1]);
        }
        return res;
    }
};
```

