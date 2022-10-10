# 239. Sliding Window Maximum

给定一个数组，和一个长度为k的sliding window在数组里从左滑到右。求出滑动过程中，sliding window所有的最大值。

这题我们用一个双端队列，来依次存放滑动窗口里所有元素的下标。当`i`和`j`同时在窗口时，如果`i < j && nums[i] <= nums[j]`，那么`i`其实就没有必要在窗口里，因为当前窗口的最大值怎么也轮不到它。所以每当sliding window向右滑动，新的元素进来的时候，把双端队列右部所有小于等于新元素的下标都清除，保持双端队列里面从头到尾下标对应的元素呈降序。滑动窗口里的最大值的下标就是双端队列里的头部元素。当然，滑动之后也要看看队列头部的那些下标是否还在窗口里，不在的话就要踢出去。

Time complexity: O(n) because each index is pushed and popped at most once.

Space complexity: O(k)

```java
public class Solution {
  public List<Integer> maxWindows(int[] array, int k) {
    // Assumptions: array is not null or not empty,
    // k >= 1 and k <= a.length.
    List<Integer> max = new ArrayList<Integer>();
    // use a descending deque to solve this problem,
    // we store the index instead of the actual value in the deque,
    // and we make sure:
    // 1. the deque only contains index in the current sliding window.
    // 2. for any index, the previous index with smaller value is
    // discarded from the deque.
    Deque<Integer> deque = new LinkedList<Integer>();
    for (int i = 0; i < array.length; i++) {
      // discard any index with smaller value than index i.
      while (!deque.isEmpty() && array[deque.peekLast()] <= array[i]) {
        deque.pollLast();
      }
      // it is possible the head element is out of the current
      // sliding window so we might need to discard it as well.
      // remove all indexes out of left boundary
      if (!deque.isEmpty() && deque.peekFirst() <= i - k) {
        deque.pollFirst();
      }
      deque.offerLast(i);
      //add element in the list of max when the current index is equal or bigger than k - 1
      if (i >= k - 1) {
        max.add(array[deque.peekFirst()]);
      }
    }
    return max;
  }
}
//tc: O(n)
//sc: O(n)
```

**Examples**

A = {1, 2, 3, 2, 4, 2, 1}, K = 3, the windows are {{1,2,3}, {2,3,2}, {3,2,4}, {2,4,2}, {4,2,1}},

and the maximum values of each K-sized sliding window are [3, 3, 4, 4, 4]