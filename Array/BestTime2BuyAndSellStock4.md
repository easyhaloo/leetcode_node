- ### 代码

```java
public int maxProfit(int k, int[] prices) {
        if(k == 0 || prices.length <= 0) return 0;

        if( k >= prices.length) return helper(prices);
        int[] local = new int[k+1];
        int[] global = new int[k+1];

        for(int i = 0 ; i< prices.length-1;i++){
            int diff = prices[i+1] - prices[i];
            for(int j = k ; j>=1 ;j--){
                local[j] = Math.max(local[j]+diff,global[j-1]+Math.max(0,diff));
                global[j] = Math.max(global[j],local[j]);
            }
        }
        return global[k];
    }

    private int helper(int[] prices){
        int res = 0;
        for(int i = 0 ; i < prices.length-1;i++){
            if(prices[i+1] > prices[i]){
                res += prices[i+1] - prices[i];
            }
        }
        return res;

    }
```
