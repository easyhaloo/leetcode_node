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
> 这题的意思是求出集合的所有子元素，就是求解所有子集。题目设置的tag是位运算，那么我们可以构建一个表格来进行位处理。拿题目的例子来说：【1，2，3】

1，2，3分别代表二进制中的111，0~111刚好八种情况，也就意味着每一种情况分别对应一个自己的子集，构建如下表格：

  |  1 |  2 |  3 | subset
--|---|---|---|--
0  |  F | F  | F  | []
1  |  F | F | T  | [3]
2  |  F | T  | F  | [2]
3  |  F |  T | T  | [2,3]
4  |  T | F  |  F | [1]
5  |  T | F  |  T | [1,3]
6  |  T | T  | T  | [1,2]
7  |  T | T  | T  | [1,2,3]


通过上述的构建，很快的就可以发现规律，T位置上数组索引的元素即是我们所需要的。我们可以根据位运算来判断每一位的T或F,当为T时加入子集合即可。

- #### 代码：

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    int k = (1 << nums.length);
    for(int i = 0 ; i < k ; i++){
        List<Integer> temp = bitMap(nums,i);
        res.add(temp);
    }
    return res;
}


private List<Integer> bitMap(int[] nums, int k){
    List<Integer> res = new ArrayList<>();
    int idx = 0 ;
    for(int i = k ; i>0 ; i>>=1){
        if((i&1) == 1) res.add(nums[idx]);
        idx++;
    }
    return res;
}
```
