
- ### 代码

```java

package interview.array;
	
	public class BestTime2BuyAndSellStock {
	
	
	    public int maxProfit(int[] prices){
	
	        if(prices == null || prices.length <= 0 ) return  0;
	
	        int max = 0,  diff = Integer.MAX_VALUE;
	        for(int price : prices){
	            diff = Math.min(price,diff);
	            max = Math.max(price-diff,max);
	        }
	        return max;
	    }
	}
	

```