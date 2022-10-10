# Laicode 193. Kth Smallest With Only 3, 5, 7 As Factors

找到第K小的由3、5和7作为因数的数。

这题和[laicode 27. Kth Smallest Sum In Two Sorted Arrays](laicode-27-Kth-Smallest-Sum-In-Two-Sorted-Arrays.md)和[378. Kth Smallest Element in a Sorted Matrix](378-Kth-Smallest-Element-Sorted-Matrix.md)也都差不多思想，BFS + Min Heap。

无非就是控制3、5和7作为因数的个数，那么其实就是对一个三维的空间进行BFS。

Time complexity: O(klogk)

Space complexity: O(k^3)

```java
public class Solution {
  // Method 1: BFS
  public long kth(int K) {
    // Assumptions: K >= 1.
    PriorityQueue<Long> minHeap = new PriorityQueue<>(K);
    Set<Long> visited = new HashSet<>();
    // we use the actual product value to represent the states
    // <x,y,z>, the value is 3^x * 5^y * 7^z, and the initial
    // state is <1,1,1>.
    minHeap.offer(3 * 5 * 7L);
    visited.add(3 * 5 * 7L);
    while (K > 1) {
      long current = minHeap.poll();
      // for the state <x+1,y,z>, the actual value is *3.
      if (visited.add(3 * current)) {
        minHeap.offer(3 * current);
      }
      // for the state <x,y+1,z>, the actual value is *5.
      if (visited.add(5 * current)) {
        minHeap.offer(5 * current);
      }
      // for the state <x,y,z+1>, the actual value is *7.
      if (visited.add(7 * current)) {
        minHeap.offer(7 * current);
      }
      K--;
    }
    return minHeap.peek();
  }
}
//time k logk                log2k
//space Ok
```