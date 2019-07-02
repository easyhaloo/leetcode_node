You're now a baseball game point recorder.

Given a list of strings, each string can be one of the 4 following types:

Integer (one round's score): Directly represents the number of points you get in this round.
"+" (one round's score): Represents that the points you get in this round are the sum of the last two valid round's points.
"D" (one round's score): Represents that the points you get in this round are the doubled data of the last valid round's points.
"C" (an operation, which isn't a round's score): Represents the last valid round's points you get were invalid and should be removed.



Each round's operation is permanent and could have an impact on the round before and the round after.

You need to return the sum of the points you could get in all the rounds.



Example 1:
Input: ["5","2","C","D","+"]
Output: 30
Explanation: 
Round 1: You could get 5 points. The sum is: 5.
Round 2: You could get 2 points. The sum is: 7.
Operation 1: The round 2's data was invalid. The sum is: 5.  
Round 3: You could get 10 points (the round 2's data has been removed). The sum is: 15.
Round 4: You could get 5 + 10 = 15 points. The sum is: 30.



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/baseball-game
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



###  解析

>  本题可以使用Stack来做，Stack中记录每次操作完的结果。
>
> - 如果为数字直接入栈
> - 是`c`弹出stack顶点元素，其余不做任何处理
> - 是`d`取stack顶点元素，不弹出。然后*2入栈
> - 如果是`+`，这里是实际要做的操作是覆盖顶点前面的元素，然后把新元素入栈。



### 代码

```java
 public int calPoints(String[] ops) {
        if (ops == null || ops.length == 0) return 0;
        Stack<Integer> stack = new Stack<>();
        int res = 0;
        for (String op : ops) {
            if (op.equals("+")) {
                int num1 = stack.pop();
                int num2 = num1 + stack.peek();
                stack.push(num1);
                stack.push(num2);
            } else if (op.equals("C")) {
                stack.pop();
            } else if (op.equals("D")) {
                stack.push(stack.peek() * 2);
            } else {
                stack.push(Integer.valueOf(op));
            }
        }
        for (Integer integer : stack) {
            res += integer;
        }
        return res;
    }
```

