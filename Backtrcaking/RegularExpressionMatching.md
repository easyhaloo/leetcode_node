Given an input string (s) and a pattern (p), implement regular expression matching with support for `'.'` and `'*'`.

```xml
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the entire input string (not partial).

- ### 解析：
> 字符串匹配，这道题的意思是说`*`表示可以代替任意个数的字符,包括前一位，`.`代表任意的字符，可以为空。那么我们可以用递归来求解：
> -  若p为空，若s也为空，直接true，反之false
> -  若p的长度为1，若s长度也为1，p[0]==s[0]或是p为'.'则返回true，反之false
> -  若p的第二个字符不为*，若此时s为空返回false，否则判断首字符是否匹配，且从各自的第二个字符开始调用递归函数匹配
> -  若p的第二个字符为*，若s不为空且字符匹配，调用递归函数匹配s和去掉前两个字符的p，若匹配返回true，否则s去掉首字母
> -  递归匹配s和去掉前两个字符的p

- ### 代码：

```java
public boolean isMatch(String s, String p) {
    if(p.isEmpty())
        return s.isEmpty();

    if(p.length()==1){
        return s.length()==1&&(p.charAt(0)==s.charAt(0)||p.charAt(0)=='.');
    }

    if(p.charAt(1)!='*'){
        if(s.isEmpty())
            return false;
        return (p.charAt(0)==s.charAt(0)||p.charAt(0)=='.')&&isMatch(s.substring(1),p.substring(1));
    }

    while(!s.isEmpty()&&(p.charAt(0)==s.charAt(0)||p.charAt(0)=='.')){
        if(isMatch(s,p.substring(2)))
            return true;
        s = s.substring(1);
    }
    return isMatch(s,p.substring(2));
}
```
