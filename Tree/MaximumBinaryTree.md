Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:

1. The root is the maximum number in the array.
2. The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
3. The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.

Construct the maximum tree by the given array and output the root node of this tree.



Example 1:
Input: [3,2,1,6,0,5]
Output: return the tree root node representing the following tree:

      6
    /   \
   3     5
    \    / 
     2  0   
       \
        1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-binary-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 构建最大二叉树，直接递归求接。
>
> - 第一次遍历全部，求出root节点，然后进行左右递归
> - 需要前置判断，当left< right 时代表没有元素可用，直接返回即可



### 代码

```java
public TreeNode constructMaximumBinaryTree(int[] nums) {
    return build(nums, 0, nums.length - 1);
  }

  private TreeNode build(int[] nums, int left, int right) {
    if (left > right) return null;
    int max = nums[left];
    int index = left;
    for (int i = left; i <= right; i++) {
      if (max < nums[i]) {
        max = nums[i];
        index = i;
      }
    }
    TreeNode node = new TreeNode(max);
    node.left = build(nums, left, index - 1);
    node.right = build(nums, index + 1, right);
    return node;
  }
```



### 解析二

> 非递归，借助stack来求解。
>
> 将数组的每个元素构建为TreeNode，然后压栈，每次遍历过程中，拿出栈中节点进行比较。
>
> - 当都都小于新节点的时候，代表当前节点为临时Root，可以将之前的root节点挂载在新节点左侧。
> - 当存在节点大于新节点时，需要将新节点挂载在临时root节点的右侧，再把之前的刚才小于自己的节点挂载再自己左侧

### 代码

```java
 public TreeNode constructMaximumBinaryTreeWithStack(int[] nums) {
    // 前置判断
    if (nums == null || nums.length == 0) return null;

    Stack<TreeNode> stack = new Stack<>();
    TreeNode last = new TreeNode(nums[0]);
    TreeNode root = last;
    stack.push(last);
    for (int i = 1; i < nums.length - 1; i++) {
      TreeNode t = new TreeNode(nums[i]);
      // 寻找root节点
      if (t.val > root.val) {
        root = t;
      }
      last = stack.peek();
      //
      if (t.val > last.val) {
        // 以当前节点为中心，寻找第一个大于自己的节点
        while (!stack.isEmpty() && stack.peek().val < t.val) {
          last = stack.pop();
        }

        if (stack.isEmpty()) {
          t.left = last;
        } else {
          stack.peek().right = t;
          t.left = last;
        }
      } else {
        stack.peek().right = t;
      }
      stack.push(t);
    }
    return root;
  }
```

