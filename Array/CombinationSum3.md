
- ### 代码

```java

package interview.array;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class CombinationSum3 {
	
	
	    public static void main(String[] args){
	        System.out.println(combinationSum(3,7));
	    }
	
	    public static List<List<Integer>> combinationSum(int k , int n){
	        List<List<Integer>> res = new ArrayList<>();
	        helper(res,new ArrayList<Integer>(),k,n,1);
	        return res;
	    }
	
	
	    private static void helper(List<List<Integer>> res,List<Integer> temp,int k,int n,int start){
	        if(temp.size() ==  k && n == 0){
	            res.add(new ArrayList<Integer>(temp));
	            return ;
	        }
	
	        for(int i = start; i<= 9;i++){
	            temp.add(i);
	            helper(res,temp,k,n-i,i+1);
	            temp.remove(temp.size()-1);
	        }
	    }
	
	}
	

```