A valid parentheses string is either empty (""), "(" + A + ")", or A + B, where A and B are valid parentheses strings, and + represents string concatenation.  For example, "", "()", "(())()", and "(()(()))" are all valid parentheses strings.

A valid parentheses string S is primitive if it is nonempty, and there does not exist a way to split it into S = A+B, with A and B nonempty valid parentheses strings.

Given a valid parentheses string S, consider its primitive decomposition: S = P_1 + P_2 + ... + P_k, where P_i are primitive valid parentheses strings.

Return S after removing the outermost parentheses of every primitive string in the primitive decomposition of S.

 

**Example 1:**

```verilog
Input: "(()())(())"
Output: "()()()"
Explanation: 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```

**Example 2:**

```verilog
Input: "(()())(())(()(()))"
Output: "()()()()(())"
Explanation: 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
```

**Example 3:**

```verilog
Input: "()()"
Output: ""
Explanation: 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-outermost-parentheses
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 这题可以使用一个小技巧，先跳过最外的左括号，分别统计左右括号的次数，当l==r时，说明匹配到当前的最右括号，直接跳过，然后重复上述过程。



### 代码

```java
class Solution {
    public String removeOuterParentheses(String S) {
        int l = 1, r = 0;
    StringBuilder sb = new StringBuilder();
    for (int i = l; i < S.length(); i++) {
      if (S.charAt(i) == '(') l++;
      else r++;
      if (l != r) sb.append(S.charAt(i));
      else {
        i++;
        l = 1;
        r = 0;
      }
    }
    return sb.toString(); 
    }
}
```

