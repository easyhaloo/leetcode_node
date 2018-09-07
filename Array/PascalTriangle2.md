
- ### 代码

```java

package interview.array;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class PascalTriangle2 {
	
	
	    public static void main(String[] args){
	        System.out.println(getRow(3));
	    }
	    public static List<Integer> getRow(int rowIndex){
	
	        List<Integer> res = new ArrayList<>();
	        for(int i = 0;i<rowIndex+1;i++){
	            res.add(0,1);
	            for(int j = 1;j < res.size()-1;j++){
	                res.set(j,res.get(j)+res.get(j+1));
	            }
	        }
	        return res;
	    }
	}
	

```