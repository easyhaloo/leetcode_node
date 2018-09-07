
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	import java.util.HashMap;
	import java.util.Map;
	
	public class PreInCreateTree {
	
	
	    public static void main(String[] args) {
	
	        int[] preorder = new int[]{3, 9, 20, 15, 7};
	        int[] inorder = new int[]{9,3,15,20,7};
	        TreeNode root = buildTree2(preorder,inorder);
	        preOrder(root);
	    }
	
	
	    public static TreeNode buildTree(int[] preorder, int[] inorder) {
	        if(preorder.length == 0 || inorder.length == 0){
	            return null;
	        }
	        TreeNode root = null;
	        int idx = 0;
	        root = new TreeNode(preorder[0]);
	        for (int i = 0; i < inorder.length; i++) {
	            if (preorder[0] == inorder[i]){
	                idx = i;
	                root.left = buildTree(
	                        Arrays.copyOfRange(preorder, 1, idx + 1),
	                        Arrays.copyOfRange(inorder, 0, idx)
	                );
	
	                root.right = buildTree(
	                        Arrays.copyOfRange(preorder, idx + 1, preorder.length),
	                        Arrays.copyOfRange(inorder, idx + 1, inorder.length)
	                );
	            }
	
	        }
	
	        return root;
	    }
	
	
	
	
	    public static TreeNode buildTree2(int[] preOrder,int[] inOrder){
	        Map<Integer,Integer> cacheMap = new HashMap<>();
	
	        for(int i=0;i<inOrder.length;i++){
	            cacheMap.put(inOrder[i],i);
	        }
	        TreeNode root = buildTree(preOrder,0,preOrder.length-1,inOrder,0,inOrder.length-1,cacheMap);
	        return root;
	    }
	
	    private static TreeNode buildTree(int[] preOrder,int preStart,int preEnd,int[] inOrder,int inStart,int inEnd,Map<Integer,Integer> cache){
	        if(preStart > preEnd || inStart > preEnd) return null;
	
	        TreeNode root = new TreeNode(preOrder[preStart]);
	        int inRoot = cache.get(root.val);
	        int numsLeft = inRoot - inStart;
	        root.left = buildTree(preOrder,preStart+1,preStart+numsLeft,inOrder,inStart,inRoot-1,cache);
	        root.right = buildTree(preOrder,preStart+numsLeft+1,preEnd,inOrder,inRoot+1,inEnd,cache);
	        return root;
	    }
	
	    public static void preOrder(TreeNode root) {
	        if (root != null) {
	            System.out.println(root.val);
	            preOrder(root.left);
	            preOrder(root.right);
	        }
	    }
	
	    static class TreeNode {
	        int val;
	
	        TreeNode(int val) {
	            this.val = val;
	        }
	
	        TreeNode left;
	        TreeNode right;
	    }
	}
	
	
	

```