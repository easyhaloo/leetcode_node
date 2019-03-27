Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

**Example 1:**

```
Input: "abab"
Output: True
Explanation: It's the substring "ab" twice.
```

**Example 2:**

```
Input: "aba"
Output: False
```

**Example 3:**

```
Input: "abcabcabcabc"
Output: True
Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
```

### 解析：

>判断当前字符串是否是重复字符串，代表这个字符串至少需要由两个及以上的相同的子串构成，那么我们可以将这个字符串扩增两倍，然后去掉首尾字符，如果能在组装后的子字符串中匹配到之前的原始串，那么就能说明这个字符串是重复子字符串构成。



**实例：**

aba  = >  abaaba   = > baba = > false

abab => abababab => bababa = > true

#### 题解：

> 在上面的实例中，可以看到如果`aba`是重复的，截取第一个我们可以拿到后面重复的子川，截取最后一个我们前面的重复子川，然后拼接，可以组装成原始的字符串。
>
> 但是当`aba`不是重复的，那么我们截取前后就会拿到不一样的子串

#### 代码：

```go
func repeatedSubstringPattern(s string) bool {
    ret := false
	joins := strings.Join([]string{s,s},"")
	newStr := string([]rune(joins)[1 : len(joins)-1])
	ret = strings.Contains(newStr,s)
	return ret
}
```

