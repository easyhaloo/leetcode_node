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
>最长回文子串，这里使用一个叫`中心扩散法则`的解决方案，以每个字符串为中心同时从左从右双向遍历，当左右两遍相同则前进指针，当出现不同则说明回文串结束，我们与最大的长度的回文子串比较，如果比之前的最大长度大，那么我们更新最大长度，并记录起始位置l+1，因为下标为l的那个位置不是回文串，我们向后移动一位。遍历完毕即可得知最长的回文子串，注意点：因为回文序列可为奇数也可能是偶数，所以我们需要都考虑，所在我们可以同时进行遍历。

- ### 代码：
```java
    int maxLen , start ;
    public String longestPalindrome(String s) {
        if(s.length() < 2) return s;
        for(int i = 0; i< s.length()-1;i++){
            helper(s,i,i);
            helper(s,i,i+1);
        }
        return s.substring(start,maxLen);
    }
    private void helper(String s,int l , int r){
        while(r<s.length()&&l>=0 && s.charAt(l) == s.charAt(r)){
            l--;
            r++;
        }
        if(maxLen < r-l-1){
            maxLen = r-l-1;
            start = l+1;
        }
    }
```
