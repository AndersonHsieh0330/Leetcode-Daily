# 121. Best Time to Buy and Sell Stock

[link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```
public int maxProfit(int[] prices) {
    if(prices.length < 2) {
    return 0;
    }

    int left = 0; // lowest
    int right = 1; // traverse index
    int maxProfit = 0;
        
    while (right < prices.length) {
        if (prices[right] < prices[left]) {
              left = right;
          }else {
              int curProfit = (prices[right] - prices[left]);
              if (curProfit > maxProfit) {
                    maxProfit = curProfit;
              }
          }
          right++;
        }
        return maxProfit;
    }
 ```


```
public int maxProfit(int[] prices) {
            int minVal = prices[0];
            int maxProf = 0;
            
            for(int i = 0 ; i < prices.length ; i++){
                minVal = prices[i] < minVal ? prices[i] : minVal;
                maxProf = (prices[i] - minVal) > maxProf ? (prices[i] - minVal) : maxProf;
            }
            
            return maxProf;
        }


```



