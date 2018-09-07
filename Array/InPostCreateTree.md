
- ### 代码

```java

package interview.array;
	
	import java.util.HashMap;
	import java.util.Map;
	
	public class InPostCreateTree {
	    public static void main(String[] args) {
	
	        int[] preorder = new int[]{3, 9, 20, 15, 7};
	        int[] inorder = new int[]{9,15,7,20,3};
	        TreeNode root = buildTree(preorder,inorder);
	        preOrder(root);
	    }
	
	    public static TreeNode buildTree(int[] inorder,int[] postorder){
	
	        Map<Integer,Integer> inMap = new HashMap<>();
	        for(int i = 0; i< inorder.length;i++){
	            inMap.put(inorder[i],i);
	        }
	
	        return buildTree(inorder,0,inorder.length-1,postorder,0,postorder.length-1,inMap);
	    }
	
	
	    private static TreeNode buildTree(int[] inorder,int inStart,int inEnd,int[] postorder,int postStart,int postEnd,Map<Integer,Integer> inMap){
	        if(inStart > inEnd || postStart > postEnd) return null;
	        TreeNode root = new TreeNode(postorder[postEnd]);
	        int inOrder = inMap.get(root.val);
	        int leftNums = inOrder - inStart;
	        root.left = buildTree(inorder,inStart,inOrder-1,postorder,postStart,postStart+leftNums-1,inMap);
	        root.right = buildTree(inorder,inOrder+1,inEnd,postorder,postStart+leftNums,postEnd-1,inMap);
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