# Laicode 119. Largest And Smallest

给定一个无序数组，用最小的比较次数找出最大和最小值。

看到这题，找最大最小很简单.

- {2, 1, 5, 4, 3}, the largest number is 5 and smallest number is 1. return [5, 1].

Time complexity: O(N)

Space complexity: O(1)

```java
public class Solution {
  public int[] largestAndSmallest(int[] array) {
    // Write your solution here
  int max = array[0];
  int min = array[0];
    for (int i = 0; i < array.length; i++){
      if (array[i] > max){
        max = Math.max(max, array[i]);
      }
      if (array[i] < max){
        min = Math.min(min, array[i]);
      }
    }
  return new int[] {max,min};
  }
}
//time on
//space o1
```