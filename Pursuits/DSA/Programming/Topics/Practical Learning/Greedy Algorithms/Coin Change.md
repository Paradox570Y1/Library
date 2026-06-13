For toned down version of this  question which can be solved with greedy: [GFG](https://takeuforward.org/data-structure/find-minimum-number-of-coins/)

```java
import java.util.*;
public class Main {
  public static void main(String[] args) {

    int V = 49;
    ArrayList < Integer > ans = new ArrayList < > ();
    int coins[] = {1, 2, 5, 10, 20, 50, 100, 500, 1000};
    int n = coins.length;
    for (int i = n - 1; i >= 0; i--) {
      while (V >= coins[i]) {
        V -= coins[i];
        ans.add(coins[i]);
      }
    }
    System.out.println("The minimum number of coins is "+ans.size());
    System.out.println("The coins are ");
    for (int i = 0; i < ans.size(); i++) {
      System.out.print(" " + ans.get(i));
    }

  }
}
```


[322. Coin Change](https://leetcode.com/problems/coin-change/)

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

**Input:** coins = [1,2,5], amount = 11
**Output:** 3
**Explanation:** 11 = 5 + 5 + 1

**Example 2:**

**Input:** coins = [2], amount = 3
**Output:** -1

**Example 3:**

**Input:** coins = [1], amount = 0
**Output:** 0

**Constraints:**

- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 231 - 1`
- `0 <= amount <= 104`


```java

```