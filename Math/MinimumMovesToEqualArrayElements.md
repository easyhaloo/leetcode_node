Given a **non-empty** integer array of size *n*, find the minimum number of moves required to make all array elements equal, where a move is incrementing *n* - 1 elements by 1.

**Example:**

```
Input:
[1,2,3]

Output:
3

Explanation:
Only three moves are needed (remember each move increments two elements):

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```



### 解析：

> 每次移动，除移动外的所有元素+1，当数组中的元素全部相等，需要移动的次数。
>
> 每次移动其他元素+1，也就意味着自己移动的那个元素-1。
>
> 要想移动的次数最少，那么也就是意味着，必须要移动最大元素，让小的元素去递增，当最小的元素也最大的相等了，那么就代表结束。
>
> 成功转换为：
>
> 求解最小元素与其他元素差的和



#### 代码：

```go
func minMoves(nums []int) int {
    min := math.MaxInt32
	for _,value := range nums {
		if min > value {
			min = value
		}
	}

	ret := 0
	for _,value := range nums {
		ret += value - min
	}
	return ret
}
```

