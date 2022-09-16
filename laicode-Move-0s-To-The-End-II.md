# Laicode 259. Move 0s To The End II

这题和[laicode 258. Move 0s To The End I](laicode-258-Move-0s-To-The-End.md)类似，但是这题要求把0移到后面之后其他非0元素的相对位置不能变。

这题的要求看似更难，其实实现起来特别容易。其实就是把所有非0元素移到前面，最后剩下的部分全部置为0就好。

Time complexity: O(N)

Space complexity: O(1)，如果答案不算入的话。

```java
public class Solution {
  public int[] moveZero(int[] array) {
    // Write your solution here
    if (array.length <= 1) {
      return array;
    }
    int slow = 0;
    for (int fast = 0; fast < array.length; fast++) {
      if(array[fast] != 0) {
        array[slow++] = array[fast];
      }
    }
    //fill in the right part with 0
    for (int i = slow; i < array.length; i++) {
      array[i] = 0;
    }
    return array;
  }
}
//Time: O(n)
//Space: O(1)
```