# Laicode 194. Kth Closest Point To <0,0,0>

给定三个有序数组，求出由他们各出一个数组成的三维坐标里离原点第K近的数。

和[laicode 27. Kth Smallest Sum In Two Sorted Arrays](laicode-27-Kth-Smallest-Sum-In-Two-Sorted-Arrays.md)差不多，只不过前者是求和，这题是求与原点之间的欧几里得距离。那么其实就是三维空间的BFS配合小顶堆，实现上没什么区别。

Time complexity: O(klogk)

Space complexity: O(k^3)

```java
public class Solution {
  public List<Integer> closest(final int[] a, final int[] b, final int[] c, int k) {
    // Assumptions: a, b, c are not null, length >= 1,
    // k >= 1 && k <= a.length * b.length * c.length.
    // we will need a min heap, with comparator to compare the distance.
    // Note that we are using the index in a,b,c as values in the List<Integer>.
    PriorityQueue<List<Integer>> minHeap = new PriorityQueue<>(2 * k, new Comparator<List<Integer>>() {
      @Override
      public int compare(List<Integer> o1, List<Integer> o2) {
        long d1 = distance(o1, a, b, c);
        long d2 = distance(o2, a, b, c);
        if (d1 == d2) {
          return 0;
        }
        return d1 < d2 ? -1 : 1;
      }
    });
    // Note that List's equals() method has been already overridden,
    // and it is comparing the actual elements in the List.
    Set<List<Integer>> visited = new HashSet<>();
    // The initial state is <0,0,0>, meaning picking the smallest elements
    // from the three arrays.
    List<Integer> cur = Arrays.asList(0, 0, 0);
    visited.add(cur);
    minHeap.offer(cur);
    while (k > 0) {
      cur = minHeap.poll();
      List<Integer> n = Arrays.asList(cur.get(0) + 1, cur.get(1), cur.get(2));
      if (n.get(0) < a.length && visited.add(n)) {
        minHeap.offer(n);
      }
      n = Arrays.asList(cur.get(0), cur.get(1) + 1, cur.get(2));
      if (n.get(1) < b.length && visited.add(n)) {
        minHeap.offer(n);
      }
      n = Arrays.asList(cur.get(0), cur.get(1), cur.get(2) + 1);
      if (n.get(2) < c.length && visited.add(n)) {
        minHeap.offer(n);
      }
      k--;
    }
    // at last, we replace the index with actual values in a, b, c.
    cur.set(0, a[cur.get(0)]);
    cur.set(1, b[cur.get(1)]);
    cur.set(2, c[cur.get(2)]);
    return cur;
  }

  private long distance(List<Integer> point, int[] a, int[] b, int[] c) {
    long dis = 0;
    dis += a[point.get(0)] * a[point.get(0)];
    dis += b[point.get(1)] * b[point.get(1)];
    dis += c[point.get(2)] * c[point.get(2)];
    return dis;
  }

}
//Time:O(klogk)
//Space: O(k)

```