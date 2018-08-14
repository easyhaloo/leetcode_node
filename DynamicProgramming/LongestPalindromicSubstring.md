Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

`Example 1:`
```java
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
`Example 2:`
```java
Input: "cbbd"
Output: "bb"
```
- ### 分析：
>最长回文子串，`动态规划`解决方案：定义dp[j][i],表示从字符串的j到i位置是否为回文，递推关系式如下：
> - dp[j][i] = 1                            when  i=j
> - dp[j][i]        = s[i] == [j]                    if i = j+1
> - dp[j][i]    = s[i] == s[j] && dp[j+1][i-1]   if i > j + 1
>
当i=j时，只有一个字符一定为true，如果i=j+1，则证明两个字符相邻，只要证明两者相等即可，当i > j + 1时，除了判断s[i]和s[j]相等之外，dp[j + 1][i - 1]若为真，就是回文串。


- ### 代码：
```java
public static String longestPalindrome(String s) {

    boolean[][] dp = new boolean[s.length()][s.length()];
    int start = 0 ,  len = 0;
    for(int i = 0 ; i< s.length();i++){
        for(int j = 0 ; j <=i;j++){
            dp[j][i] = (s.charAt(i) == s.charAt(j) && (i-j < 2 || dp[j+1][i-1]));
            if(dp[j][i]&& len < i-j+1){
                len = i-j+1;
                start = j;
            }
        }
        dp[i][i] = true;
    }
    return s.substring(start,start+len);
}
```
