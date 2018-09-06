- ### 代码

```java
public int maxProfit(int[] prices){
       if(prices == null || prices.length <= 0) return 0;
   int[] global = new int[3];
   int[] local  = new int[3];
   for(int i = 0;i<prices.length-1;i++){
       int diff = prices[i+1] - prices[i];
       for(int j = 2 ; j >=1 ; j--){
           local[j] = Math.max(local[j]+diff,global[j-1]+Math.max(diff,0));
           global[j] = Math.max(global[j],local[j]);
       }
   }

   return global[2];
}
```
