Given the root node of a binary search tree, return the sum of values of all nodes with value between L and R (inclusive).

The binary search tree is guaranteed to have unique values.



**Example 1:**

```pseudocode
Input: root = [10,5,15,3,7,null,18], L = 7, R = 15
Output: 32
```



**Example 2:**

```pseudocode
Input: root = [10,5,15,3,7,13,18,1,null,6], L = 6, R = 10
Output: 23
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/range-sum-of-bst
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

>  题意为：在二叉搜索树中求给定区间段值的总和。
>
> 根据二叉搜索树的特性克制，left < root < right。中序遍历树可以使元素升序排列。
>
> 我们可以利用这个特性求解:
>
> root.val < L 时  舍去左半部分
>
> root.val > R 时 舍去右半部分
>
> L <= root.val <= R 时，记录结果，然后继续递归。



### 代码

```java

    public int rangeSumBST(TreeNode root, int L, int R) {
      if (root == null) return 0;


      if (root.val < L) {
        return rangeSumBST(root.right, L, R);
      }
      if (root.val > L) {
        return rangeSumBST(root.left, L, R);
      }
      return root.val + rangeSumBST(root.right, L, R) + rangeSumBST(root.left, L, R);
    }
```

