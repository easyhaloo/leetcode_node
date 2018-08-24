Given an input string (s) and a pattern (p), implement regular expression matching with support for `'.'` and `'*'`.

```xml
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the entire input string (not partial).

- ### 解析：
> 字符串匹配，这道题的意思是说`*`表示可以代替任意个数的字符,包括前一位，`.`代表任意的字符，可以为空。一般字符串的题目都可用动态规划来求解
>1. 建立dp数组，大小为s.length()-1.，dp[i]维护p可以匹配到s[0,i]这个子串的状态。
>2. 当s[i] == p [i] 或者 p [i] == '.'时都可以成功匹配s[i]
>3. 当p[i] == '\*'时，有些麻烦，因为`*`不仅可以匹配后面的元素，还可以匹配前面的一位元素，p[i]!=s[i]但是只要dp[i-1]为true，dp[i]就可以为true.

通过上述的分析，我们可以建立起状态转移的方程：

当p[j]='*'，我们可以逆向遍历。i = s.length()-1

`dp[i] = d[i] ||  (dp[i+1]&& (p[j-1] == s[i] || p[j-1] == '.')


当p[j]!='*'，我们可以正向遍历。i = 0

dp[i] = d[i+1]&& (p[j]=='.' || p[j] == s[i])


- ### 代码：

```java
 public boolean isMatch(String s, String p) {
   boolean dp[] = new boolean[s.length()+1];
   dp[s.length()] = true;
   for(int pIndex = p.length()-1; pIndex >= 0 ; pIndex--){

    if(p.charAt(pIndex) == '*'){
        for(int sIndex = s.length()-1; sIndex >= 0 ; sIndex--){
            dp[sIndex] = dp[sIndex]
                    || (dp[sIndex+1] && ( p.charAt(pIndex-1) == '.'|| (p.charAt(pIndex-1) == s.charAt(sIndex))));
        }
        pIndex--;
    }else{
        for(int sIndex = 0; sIndex < s.length();sIndex++){
            dp[sIndex] = dp[sIndex+1]&& (p.charAt(pIndex) == '.' || p.charAt(pIndex) == s.charAt(sIndex) );
        }
        dp[s.length()] = false;
    }
  }
  return dp[0];
}
```
