Given a string, find the length of the longest substring without repeating characters.


`Examples:`
```java
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

- ### 解析
> 这道题的意思是求解无重复字符的最长子串，我们可以借助`hashmap`来存放每一段的不重复子串的起始位置，依次遍历，不断更新最长子串的的长度即可。
>
>使用map记录每个字符出现的第一个位置，当第二次出现的时候证明该子串是不重复的，从Map中取出第一次出现的下标索引，然后用当前的下标索引减去原来的即为此次遍历的子串长度，不断更新最大子串长度的值，循环完毕max即为最大。


- ### 代码
```java
public int lengthOfLongestSubstring(String s) {
    if(s.length()==0){
        return 0;
    }
    int max = 0;
    Map<Character,Integer> map = new HashMap<>();

    //j 存起始位置 i存终止位置
    // 先将第一个字符put到Map中 当出现第二次时将j的置为第二次出现的位置的右侧 更新max
    for(int i=0,j =0,len=s.length();i<len;i++){
        //判断字符是否存在
        if(map.containsKey(s.charAt(i))){

            j  = Math.max(j,map.get(s.charAt(i))+1);
        }

        map.put(s.charAt(i),i);
        max = Math.max(max,i-j+1);
    }
    return max;
}
```
