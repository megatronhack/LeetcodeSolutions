# Laicode 87. Max Product Of Cutting Rope

- **Assumptions**n >= 2
- **Examples** n = 12, the max product is 3 * 3 * 3 * 3 = 81(cut the rope into 4 pieces with length of each is 3).

给定一个长度为`length`的绳子，将其切割为若干段，使得各段长度乘积最大。

左大段 ＋ 右小段 思想: M[i] represents the maximal product of M[0] * M[1] * ...

经典DP题。我们用`maxProduct[i]`来表示长度为`i`的绳子的最大切割乘积。那么`maxProduct[i]`就有两类切法，
+ 只切一刀，在j处切一刀乘积`j * (i - j)`是最大的。
+ 切多刀，切多刀我们可转化为其中j长度切多刀，剩下来(i-j)额外一刀。那么就是`maxProduct[j] * (i - j)`最大。

根据以上思路，对于每一个子问题`maxProduct[i]`，我们都需要遍历所有它所有的子问题以求出它的答案。所以双重循环，来解决所有子问题，最后就可以得到length的最大切割乘积。

| index | 0       | 1       | 2    | 3    | 4    | 5    |
| ----- | ------- | ------- | ---- | ---- | ---- | ---- |
| M     | invalid | invalid | 1    | 2    | 4    |      |

Time complexity: O(N^2)

Space complexity: O(N)

```java
public class Solution {
  public int maxProduct(int length) {
    // Write your solution here
  int[] array = new int[length + 1];
  array[1] = 0; // emphasize the question that rope needs to be cut one time
  for (int i = 2; i <= length; i++){
     for(int j = 1; j < i; j++){
       array[i] = Math.max(array[i], Math.max(array[j], j) *  (i - j)  );
     }
  } 
  return array[length];
  }
}
//time O n^2
//space o n
```