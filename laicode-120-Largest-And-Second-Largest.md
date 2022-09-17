# Laicode 120. Largest And Second Largest

给定一个无序数组，用最少的比较次数找到最大值和次大值。

- {2, 1, 5, 4, 3}, the largest number is 5 and 2nd largest number is 4.

```java
public class Solution {
  public int[] largestAndSecond(int[] array) {
    //
    for (int i = 0; i < array.length; i++) {
      //int max = array[i];
      for (int j = i + 1; j < array.length; j++) {
        if (array[j] > array[i]) {
          swap(array, i, j);
        }
      }
    }
    return Arrays.copyOf(array, 2);
  }
  private void swap(int[] array, int left, int right) {
    int tmp = array[left];
    array[left] = array[right];
    array[right] = tmp;
  }
}
```