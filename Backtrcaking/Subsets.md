Given a set of `distinct` integers, nums, return all possible subsets (the power set).

`Note: The solution set must not contain duplicate subsets.`

`Example:`
```java
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

- #### 题解：
> 这题的意思是求出集合的所有子元素，就是求解所有子集。直接DFS遍历+回溯。
每次加入一个元素到结果中，然后拿出来，换其他的元素。直至遍历结束。需要注意的是，我们不能包含重复元素，虽有每次递归的起始位置是i+1，不能是index+1.

- #### 代码：

```java
 public static List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res=  new ArrayList<>();
        dfs(res,new ArrayList<>(),nums,0);
        return res;
    }


private static void dfs(List<List<Integer>> res,List<Integer> temp,int[] nums,int start){
    res.add(new ArrayList<>(temp));
    for(int i = start; i < nums.length;i++){
        temp.add(nums[i]);
        dfs(res,temp,nums,i+1);
        temp.remove(temp.size()-1);
    }
}
```
