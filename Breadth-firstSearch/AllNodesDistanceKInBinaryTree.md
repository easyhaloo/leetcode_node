We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.



**Example 1:**

```java
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation: 
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.
```



![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/06/28/sketch0.png)

Note that the inputs "root" and "target" are actually TreeNodes.
The descriptions of the inputs above are just serializations of these objects.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/all-nodes-distance-k-in-binary-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 求二叉树中，距离给定目标节点为k的邻居节点。
>
> 首先，我们可以使用一个Map来保存每个节点的父子引用关系。
>
> 然后，使用一个Set集合来存放访问过的节点。
>
> 最后，可以使用一个queue来保存距离目标节点为k的节点。
>
> 第一次从root节点开始广度优先遍历，建立节点的父子引用关系。
>
> 然后开始从target开始，广度遍历，即从左右父亲开始遍历，每次遍历k的层级减少1点，直至k=0.



### 代码

```java
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        List<Integer> res = new ArrayList<>();

        if(target == null || root == null) return res;
        //父子节点映射关系
        Map<TreeNode,TreeNode> parents = new HashMap<>();
        Set<TreeNode> visited = new HashSet<>();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while(!queue.isEmpty()){
            TreeNode parent = queue.poll();
            if(parent.left!=null) {
                queue.add(parent.left);
                parents.put(parent.left,parent);
            }

            if(parent.right != null){
                queue.add(parent.right);
                parents.put(parent.right,parent);
            }
        }

        queue.clear();
        queue.add(target);
        visited.add(target);


        while(K-- >0){
            int size = queue.size();
            for(int i = 0 ; i<size ; i++){
                TreeNode node = queue.poll();
                if(node.left != null && visited.add(node.left)) queue.add(node.left);
                if(node.right != null && visited.add(node.right)) queue.add(node.right);
                if(parents.get(node) != null && visited.add(parents.get(node))) queue.add(parents.get(node));
            }
        }


        while(!queue.isEmpty()){
            res.add(queue.poll().val);
        }
        return res;
    }
}
```

