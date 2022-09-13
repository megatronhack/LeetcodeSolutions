# 674. Longest Continuous Increasing Subsequence

**Examples**

- {7, 2, 3, 1, 5, 8, 9, 6}, longest ascending subarray is {1, 5, 8, 9}, length is 4.
- {1, 2, 3, 3, 4, 4, 5}, longest ascending subarray is {1, 2, 3}, length is 3.

给定一个数组，找到最长升序子数组的长度并返回。

非常简单的动态规划题。我们可以计算出给定任意一个下标`i`，以它结尾的升序子数组长度是多少，放在`lis[i]`里。那么`lis[i]`其实某种程度上来说就是取决于`lis[i-1]`。

如果array[i] <= array[i-1]，count ++。如果array[i] 不比 array[i - 1]大的话，count 重置为 1, 重新计算。如此维护循环不变量。

用 max = Math.max(cur, max)来放答案，初始化为1，然后从下标1开始遍历到最后，途中不断计算`max`并更新lisLength。最后，我们就可以得到答案。

Time complexity: O(N)

Space complexity: O(1)

```java
public class Solution {
  public int longest(int[] array) {
    // Initiate the length and use a max to update the value
    if (array.length == 0) {
      return 0;
    }
    int cur = 1;
    int max = 1;
    for (int i = 1; i < array.length; i++) {
      //compare the value of the two elements
      if (array[i] > array[i -1]) {
        cur++;
        max = Math.max(cur, max);
      } else {
        cur = 1;
      }
    }
    return max;
  }
}
//Time: O(n)
//Space: 0(1)

```