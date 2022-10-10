# Laicode 133. Merge K Sorted Array

讲真，这题和[23. Merge k Sorted Lists](23-Merge-K-Sorted-Lists.md)差不多，一个思路。只是这题是二维数组，所以实现小顶堆的`Comparator`的时候略有区别，其他要做的事情是一样的。

2D array要遍历完。

时空复杂度也是一样的。

```java
public class Solution {
    public int[] merge(int[][] arrayOfArrays) {
    // Assumptions: arrayOfArrays is not null, none of the array is null either.
    PriorityQueue<Entry> minHeap = new PriorityQueue<Entry>(11, new MyComparator());
    int length = 0;
    for (int i = 0; i < arrayOfArrays.length; i++) {
      int[] array = arrayOfArrays[i];
      length += array.length;
      if (array.length != 0) {
        // We use two index to record the position of each element:
        // the index of the array in the arrayOfArrays,
        // the index of the element in the array.
        minHeap.offer(new Entry(i, 0, array[0]));
      }
    }
    int[] result = new int[length];
    int cur = 0;
    while (!minHeap.isEmpty()) {
      Entry tmp = minHeap.poll();
      result[cur++] = tmp.value;
      //travse all elements in 2D array
      if (tmp.y + 1 < arrayOfArrays[tmp.x].length) {
        // reuse the same Entry object but advance the index by 1.
        tmp.y++;
        tmp.value = arrayOfArrays[tmp.x][tmp.y];
        minHeap.offer(tmp);
      }
    }
    return result;
  }

  static class MyComparator implements Comparator<Entry> {
    @Override
    public int compare(Entry e1, Entry e2) {
      if (e1.value == e2.value) {
        return 0;
      }
      return e1.value < e2.value ? -1 : 1;
    }
  }

  static class Entry {
    // The row number.
    int x;
    // The column number.
    int y;
    // The corresponding value.
    int value;

    Entry(int x, int y, int value) {
      this.x = x;
      this.y = y;
      this.value = value;
    }
  }
}

```

or other comparator version

```java
public class Solution {
    public int[] merge(int[][] arrayOfArrays) {
    // Assumptions: arrayOfArrays is not null, none of the array is null either.
    PriorityQueue<Entry> minHeap = new PriorityQueue<Entry>(11, new MyComparator());
    int length = 0;
    for (int i = 0; i < arrayOfArrays.length; i++) {
      int[] array = arrayOfArrays[i];
      length += array.length;
      if (array.length != 0) {
        // We use two index to record the position of each element:
        // the index of the array in the arrayOfArrays,
        // the index of the element in the array.
        minHeap.offer(new Entry(i, 0, array[0]));
      }
    }
    int[] result = new int[length];
    int cur = 0;
    while (!minHeap.isEmpty()) {
      Entry tmp = minHeap.poll();
      result[cur++] = tmp.value;
      if (tmp.y + 1 < arrayOfArrays[tmp.x].length) {
        // reuse the same Entry object but advance the index by 1.
        tmp.y++;
        tmp.value = arrayOfArrays[tmp.x][tmp.y];
        minHeap.offer(tmp);
      }
    }
    return result;
  }

  static class MyComparator implements Comparator<Entry> {
    @Override
    public int compare(Entry e1, Entry e2) {
      if (e1.value == e2.value) {
        return 0;
      }
      return e1.value < e2.value ? -1 : 1;
    }
  }

  static class Entry {
    // The row number.
    int x;
    // The column number.
    int y;
    // The corresponding value.
    int value;

    Entry(int x, int y, int value) {
      this.x = x;
      this.y = y;
      this.value = value;
    }
  }
}

```

