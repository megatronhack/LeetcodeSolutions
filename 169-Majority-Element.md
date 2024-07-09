# 169. Majority Element

给定一个无序数组，找到其中占多数的数。这里多数的定义是，这个数出现的次数超过一半。如果是8个数，超过4次。如果是9个数，超过4次。

Assumption:
+ 输入不为空
+ 一定存在这么一个数

那么我们其实可以用voting algorithm来计算这里的majority element。用candidate来记录当前的候选数字，初始化为首个元素。count来记录当前候选数字出现的次数，初始化为1。从下标1开始遍历到最后，每轮做如下处理：
+ 如果count为0的话，重置候选数字为当前数字，count设置为1
+ 如果count不为0，那么候选数字和当前数字是否一致。一致的话，count自增。不一致，count自减。

这样我们最后就可以找到这个超过半数的数字。因为这个出现了超过一半的数，最后肯定count不会被置为0。途中count有可能被置0，但是最后这个数一定是存在candidate里，并且count > 0。因为其他数加起来的次数都没有它多。

Time complexity: O(n)

Space complexity: O(1)

```java
public class Solution {
  public int majority(int[] array) {
    // Assumptions: array is not null and is not empty.
    // majority number guarantees to exist.
    int candidate = array[0];
    int count = 1;
    for (int i = 1; i < array.length; i++) {
      if (count == 0) {
        count++;
        candidate = array[i];
      } else if (candidate == array[i]) {
        count++;
      } else {
        count--;
      }
    }
    return candidate;
  }
}
//tc: O(n)
//sc: O(1)

```

**Examples**

- A = {1, 2, 1, 2, 1}, return 1