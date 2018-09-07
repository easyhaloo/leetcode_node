
- ### 代码

```java

package interview.array;
	
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class Subsets {
	
	
	    public static void main(String[] args){
	        int[] arr = new int[]{1,2,3};
	        System.out.println(subsets2(arr));
	    }
	
	    public static  List<List<Integer>> subsets(int[] nums){
	        List<List<Integer>> res = new ArrayList<>();
	        res.add(new ArrayList<Integer>());
	
	        for(int i : nums){
	            List<List<Integer>> temp = new ArrayList<>();
	            for(List<Integer> subList:res){
	                List<Integer> a = new ArrayList<>(subList);
	                a.add(i);
	                temp.add(a);
	            }
	            res.addAll(temp);
	         }
	        return res;
	    }
	
	
	    public static List<List<Integer>> subsets2(int[] nums){
	        List<List<Integer>> res=  new ArrayList<>();
	        helper(res,new ArrayList<Integer>(),nums,0);
	        return res;
	    }
	
	    private static void helper(List<List<Integer>> res,List<Integer> temp,int[] nums,int start){
	        res.add(new ArrayList<Integer>(temp));
	        for(int i = start;i< nums.length;i++){
	            temp.add(nums[i]);
	            helper(res,temp,nums,i+1);
	            temp.remove(temp.size()-1);
	        }
	    }
	 }
	

```