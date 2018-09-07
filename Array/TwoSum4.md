
- ### 代码

```java

package interview.array;
	
	import interview.linklist.TreeNode;
	
	import java.util.ArrayList;
	import java.util.HashSet;
	import java.util.List;
	import java.util.Set;
	
	public class TwoSum4 {
	
	    public boolean findTarget(TreeNode root,int k){
	        List<Integer> res = new ArrayList<>();
	        inOrder(root,res);
	        for(int i = 0 , j = res.size()-1;i<j;){
	            if(res.get(i) + res.get(j) == k) return true;
	            if(res.get(i) + res.get(j) < k)i++;
	            else j--;
	        }
	        return false;
	    }
	
	
	    private void inOrder(TreeNode root,List<Integer> res){
	        if(root != null){
	            res.add(root.val);
	            inOrder(root.left,res);
	            inOrder(root.right,res);
	        }
	    }
	
	
	
	
	
	    public boolean findTarget2(TreeNode root,int k){
	        Set<Integer> set = new HashSet<>();
	        return dfs(root,set,k);
	    }
	    private boolean dfs(TreeNode root,Set<Integer> set,int k){
	        if(root == null) return false;
	        if(set.contains(root.val - k)) return true;
	        set.add(root.val);
	        return dfs(root.left,set,k) || dfs(root.right,set,k);
	    }
	
	
	
	    public boolean findTarget3(TreeNode root, int k ){
	        return dfs(root,root,k);
	    }
	
	
	    private boolean dfs(TreeNode root,TreeNode cur, int k){
	        if(cur == null) return false;
	        return search(root,cur,k-cur.val) || dfs(root,cur.left,k) || dfs(root,cur.right,k);
	    }
	
	
	    private boolean search(TreeNode root , TreeNode cur, int value){
	        if(root  == null ) return false;
	        return (root.val == value)&&(root != cur)
	                || (root.val < value) && search(root.right,cur,value)
	                || (root.val > value) && search(root.left,cur,value);
	    }
	}
	

```