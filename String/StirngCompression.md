Given an array of characters, compress it [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm).

The length after compression must always be smaller than or equal to the original array.

Every element of the array should be a **character** (not int) of length 1.

After you are done **modifying the input array in-place**, return the new length of the array.

 

**Follow up:**
Could you solve it using only O(1) extra space?

 

**Example 1:**

```
Input:
["a","a","b","b","c","c","c"]

Output:
Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]

Explanation:
"aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".
```

 

**Example 2:**

```
Input:
["a"]

Output:
Return 1, and the first 1 characters of the input array should be: ["a"]

Explanation:
Nothing is replaced.
```

 

**Example 3:**

```
Input:
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

Output:
Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].

Explanation:
Since the character "a" does not repeat, it is not compressed. "bbbbbbbbbbbb" is replaced by "b12".
Notice each digit has it's own entry in the array.
```

- ### 解析

> 要求使用`原地压缩算法`，大概意思是让一个字符串中，每个字符后面重复的字符使用数字代替个数，如果是一个的话就直接省略，每个数字占用一个字符，也就是说`12`是代表两个字符。

- #### 题解一

> 锚点法： anchor每个不同字符的下标，ret记录新串的长度
>
> 1、 初始化锚点位置为0
>
> 2、 循环迭代，判断当前值与后一位是否一样
>
> - 如果不一样代表出现锚点，
>
>   - 首先要计算出当前索引距离上一次锚点的距离，代表代表上一次锚点出现的次数
>   - `num = index-anchor+1`，需要使用`strconv.Itoa()`,返回的是一个字符串
>   - 每当出现锚点与计算锚点出现次数时，都需要ret++
>   - 更新anchor值， anchor=index+1
>
>   

- #### 代码

- ```go
  func comperss(chars []byte) int {
  	ret, anchor, len := 0, 0, len(chars)
  	for index, value := range chars {
  		if index == len-1 || value != chars[index+1] {
  			chars[ret] = chars[anchor]
  			ret++
  			if index > anchor {
                  // 记录出现的次数
  				for _, v := range strconv.Itoa(index - anchor + 1) {
  					chars[ret] = byte(v)
  					ret++
  				}
  			}
  			anchor = index + 1
  		}
  	}
  
  	return ret
  }
  ```

  

