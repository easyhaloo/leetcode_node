
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	
	public class PlusOne {
	
	    public static void main(String[] args){
	        PlusOne plusOne = new PlusOne();
	        int[] arr = new int[]{
	               0
	        };
	        for(int i : plusOne.plusOne(arr)){
	            System.out.print(i);
	        }
	    }
	
	
	    public int[] plusOne(int[] digits){
	        int len = digits.length-1;
	        digits[len] += 1 ;
	        for(int i = len-1;i>=0;i--){
	            digits[i] += digits[i+1]/10;
	            digits[i+1] = digits[i+1]%10;
	        }
	        if(digits[0] >= 10){
	            int[] newArr =  new int[len+2];
	            int carry = digits[0]/10;
	            newArr[0] = carry;
	            newArr[1] = digits[0]%10;
	
	            System.arraycopy(digits,1,newArr,2,len);
	            return newArr;
	        }else{
	            return digits;
	        }
	    }
	}
	

```