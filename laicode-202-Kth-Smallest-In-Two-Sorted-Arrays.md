# Laicode 202. Kth Smallest In Two Sorted Arrays

这题采用而二分的思想。把`a`数组和`b`数组的各自前`k/2`个比较，达到每次删除k/2的效果。A[k/2 - 1]和B[k/2 - 1]谁小就删谁的前k/2，因为第k小肯定不在那个范围里，该范围里面都是比第k小还小的数。我们只要在剩下的的范围里寻找`k - k/2`小就好。

Time complexity: O(logk)

Space complexity: O(logk) because of logk level call stack.

```java
public class Solution {
  public int kth(int[] a, int[] b, int k) {
    // Assumptions: a, b is not null, at least one of them
    // is not empty, k <= a.length + b.length, k >=1.
    return kth(a, 0, b, 0, k);
  }
  // in the subarray of a starting from index aleft, and
  // subarray of b starting from index bleft, find the kth smallest
  // element among these two subarrays.
  private int kth(int[] a, int aleft, int[] b, int bleft, int k) {
    // three base cases:
    // 1. we already eliminate all the elements in a.
    // 2. we already eliminate all the elements in b.
    // 3. when k is reduced to 1, don't miss this base case.
    // The reason why we have this as base case is in the following
    // logic we need k >= 2 to make it work.
   if (aleft >= a.length) {
     return b[bleft + k - 1];
   }
   if (bleft >= b.length) {
     return a[aleft + k - 1];
   }
   if (k == 1) {
     return Math.min(a[aleft], b[bleft]);
   }
    // we compare the k/2 th element in a's subarray.
    // and the k/2 th element in b's subarray.
    // to determine which k/2 partition can be surely included
    // in the smallest k elements.
  int amid = aleft + k/2 - 1;
  int bmid = bleft + k/2 - 1;
  int aval = amid >= a.length ? Integer.MAX_VALUE : a[amid];
  int bval = bmid >= b.length ? Integer.MAX_VALUE : b[bmid];
  if (aval < bval) {
    return kth(a, amid + 1, b, bleft, k - k / 2);
  } else {
    return kth(a, aleft, b, bmid + 1, k - k / 2);
  }
  }
}

//tc : O(logk)
//sc: O(1)

```