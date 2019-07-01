Find the smallest prime palindrome greater than or equal to N.

Recall that a number is prime if it's only divisors are 1 and itself, and it is greater than 1. 

For example, 2,3,5,7,11 and 13 are primes.

Recall that a number is a palindrome if it reads the same from left to right as it does from right to left. 

For example, 12321 is a palindrome.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/prime-palindrome
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



**Example 1:**

```java
Input: 6
Output: 7
```

**Example 2:**

```java
Input: 8
Output: 11
```

**Example 3:**

```java
Input: 13
Output: 101
```





### 解析

>  求回文数字，比N大的最小回文数字。
>
> 需要理解两个数学规律：
>
> - 长度为偶数的回文数都可以被11整除
> - 除2，3外的所有素数都可以用`6x+1` or `6x-1`(6x+5)来表示



[证明一](https://www.zybang.com/question/cabb7b9c3e7dd2f48b0e6db5ad135f2f.html)

为了方便先处理不超过11的数。

现在我们需要寻找素数增长的步长，可以使用`N%6`来表示。

为什么需要这样计算，因为上面的**定律2**，所有素数都可以表示为`6x+1` or `6x-1`，因此在寻找素数时，不必要挨个增长，只需要增上的幅度满足上述要求即可。增长的大小满足`6x+1`or`6x-1`.

当我们求出步长为偶数后，我们需要跳过所有的偶数，因为根据`定理1`，长度为偶数的回文数都可以被11整除。

所以我们不管它现在是不是回文数，都需要舍弃，如果是回文那么必定不是素数。

跳过的方法为`pow(10,len)+1`。

**举个例子：**

如果出现的是123321,那么此时我们直接取1000001.

直接舍弃`100000~999999`

### 代码

```java
// 数学定理：
  //  - 除了11外， 如果回文数的长度为偶数，则一定能被11整除。
  //  - 除2，3外，所有的素数分布在 6x+1  or 6x-1
  public int primePalindrome(int N) {

    if (N <= 11) {
      if (N <= 2) return 2;
      if (N <= 3) return 3;
      if (N <= 5) return 5;
      if (N <= 7) return 7;
      return 11;
    }

    int step = N % 6;
    switch (step) {
      case 0:
        N++;
      case 1:
        step = 1;
        break;
      case 2:
        N++;
      case 3:
        N++;
      case 4:
        N++;
      case 5:
        step = 5;
        break;
    }
		// 结果不会超过10位数字 2 * 10^8
    int[] nums = new int[10];
    for (; ; ) {
      int len = length(N, nums);
      if ((len & 1) == 0) {
        // 假定长度为偶数回文数，需要/11
        N = (int) Math.pow(10, len) + 1;
        step = 5;
        continue;
      }

      if (isPalindrome(nums, len) && isPrime(N)) {
        return N;
      }

      // 6x+1
      if (step == 1) {
        N += 4;
        step = 5;
      } else {
        // 6x -1
        N += 2;
        step = 1;
      }
    }
  }

  private boolean isPrime(int N) {
    int sqrt = (int) Math.sqrt(N);
    for (int i = 5; i <= sqrt; i += 6) {
      if (N % i == 0 || N % (i + 2) == 0) return false;
    }
    return true;
  }


  private boolean isPalindrome(int[] nums, int length) {
    for (int i = 0; i < length / 2; i++) {
      if (nums[i] != nums[length - i - 1]) return false;
    }
    return true;
  }

  private int length(int N, int[] nums) {
    int len = 0;
    while (N > 0) {
      nums[len++] = N % 10;
      N /= 10;
    }
    return len;
  }
```



