 A positive integer is magical if it is divisible by either A or B.

Return the N-th magical number.  Since the answer may be very large, return it modulo 10^9 + 7.



**Example 1:**

```java
Input: N = 1, A = 2, B = 3
Output: 2
```

**Example 2:**

```java
Input: N = 4, A = 2, B = 3
Output: 6
```

**Example 3:**

```java
Input: N = 5, A = 2, B = 4
Output: 10
```

**Example 4:**

```java
Input: N = 3, A = 6, B = 4
Output: 8
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/nth-magical-number
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 使用二分搜索，从边界值开始遍历，
>
> 需要求出A,B的最小公倍数。 A*B / gcd(A,B) 可以求出最小公倍数。
>
> X/A + X/B - X/lcm = N可以求出X。
>
> 为什么要减去最小公倍数呢？ 因为X/A 和X/B 实质上在公倍数的位置求了两次，重叠了



### 代码

```java
 public int nthMagicalNumber(int N, int A, int B) {
    long lcm = (A * B) / gcd(A, B);
    long mod = (long) 1e9 + 7;
    long left = 2;
    long right = (long) 1e14;
    while (left < right) {
      long mid = (left + right) / 2;
      if (mid / A + mid / B - mid /lcm < N) left = mid + 1;
      else right = mid;
    }
    return (int) (left % mod);
  }

  long gcd(long a, long b) {
    if (b == 0) return a;
    else return gcd(b, a % b);
  }
```

