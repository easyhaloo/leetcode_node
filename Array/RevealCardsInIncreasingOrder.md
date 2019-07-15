1In a deck of cards, every card has a unique integer.  You can order the deck in any order you want.

Initially, all the cards start face down (unrevealed) in one deck.

Now, you do the following steps repeatedly, until all cards are revealed:

Take the top card of the deck, reveal it, and take it out of the deck.

1. If there are still cards in the deck, put the next top card of the deck at the bottom of the deck
2. If there are still unrevealed cards, go back to step 1.  Otherwise, stop.
3. Return an ordering of the deck that would reveal the cards in increasing order.

The first entry in the answer is considered to be the top of the deck.



**Example 1:**

```verilog
Input: [17,13,11,2,3,5,7]
Output: [2,13,3,11,5,17,7]
Explanation: 
We get the deck in the order [17,13,11,2,3,5,7] (this order doesn't matter), and reorder it.
After reordering, the deck starts as [2,13,3,11,5,17,7], where 2 is the top of the deck.
We reveal 2, and move 13 to the bottom.  The deck is now [3,11,5,17,7,13].
We reveal 3, and move 11 to the bottom.  The deck is now [5,17,7,13,11].
We reveal 5, and move 17 to the bottom.  The deck is now [7,13,11,17].
We reveal 7, and move 13 to the bottom.  The deck is now [11,17,13].
We reveal 11, and move 17 to the bottom.  The deck is now [13,17].
We reveal 13, and move 17 to the bottom.  The deck is now [17].
We reveal 17.
Since all the cards revealed are in increasing order, the answer is correct.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reveal-cards-in-increasing-order
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。







### 解析

> 题目要求，给定一个牌组，希望能够对牌组进行重新排序后，按照如下规则能够产生升序：
>
> 1. 从牌组顶部抽一张牌，显示它，然后将其从牌组中移出。
> 2. 如果牌组中仍有牌，则将下一张处于牌组顶部的牌放在牌组的底部。
> 3. 如果仍有未显示的牌，那么返回步骤 1。否则，停止行动。
>
> 这题，我们可以反过来想。将牌组按照降序排列，返回降序排列之前的序列（这个序列就是倒叙）：
>
> 1. 每次取最大的数，（不显示）添加到新牌组尾部。
> 2. 如果牌组中仍有牌，则将新牌组的首部放在新牌组的底部。
> 3. 如果仍有未显示的牌，那么返回步骤 1。否则，停止行动。（重复1，2）
>
> **第一次，我们选17，[17]->[17]**
> **第二次，我们选13，[17, 13]->[13, 17]**
> **第三次，我们选11，[13, 17, 11]->[17, 11, 13]**
> **第四次，我们选7，[17, 11, 13, 7]->[11, 13, 7, 17]**
> **第五次，我们选5，[11, 13, 7, 17, 5]->[13, 7, 17, 5, 11]**
> **第六次，我们选3，[13, 7, 17, 5, 11, 3]->[7, 17, 5, 11, 3, 13]**
>
> 









### 代码

```java
  public static int[] deckRevealedIncreasing(int[] deck) {
    if (deck == null || deck.length < 2) return deck;

		// 升序排列
    Arrays.sort(deck);
    Queue<Integer> queue = new LinkedList<>();
		
    for (int i = deck.length - 1; i >= 0; i--) {
      queue.add(deck[i]);
      if (i == 0) break;
      queue.add(queue.poll());
    }

    for (int i = deck.length - 1; i >= 0; i--) {
      deck[i] = queue.poll();
    }
    return deck;
  }
```

