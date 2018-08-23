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
> 这题的意思是求出集合的所有子元素，就是求解所有子集。我们直接直观的进行遍历累加。在原来有子集合的基础上进行添加元素。

拿`[1,2,3]`为例，我们可以进行如下的操作，第一次的时候加入一个空集合

`第一次：[] 空集合`

`第二次：[1] 加入1`

`第三次：[2] ,[1,2] 加入2`

`第四次：[3], [2,3] ,[1,3] ,[1,2,3] 加入3`

最终的结果就是`[],[1],[2],[1,2],[3],[3],[2,3],[1,3],[1,2,3]`，刚好8中情况。


- #### 代码：

```java
    public List<List<Integer>> subsets(int[] nums) {
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
```
