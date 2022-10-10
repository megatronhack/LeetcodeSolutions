# 407. Trapping Rain Water II

给定一个高度数组，求出它能盛放多少水。

这题相当于是2维版的[42. Trapping Rain Water](42-Trapping-Rain-Water.md)，但是解法大不相同。这题我们需要用到优先队列来把所有的边界上的点压入，排序标准就是高度。接着，我们开始向内收缩，进行BFS。

当优先队列不为空的时候做以下几件事：
+ 从队列中取出最矮的点，遍历它的未访问过的相邻点。
+ 如果相邻点比它矮，那么该点可以盛他们之间高度差体积的水。如果相邻点不比它矮，那就盛不了水。
+ 把相邻点压入队列。如果相邻点比当前点高的话，那就取相邻点的高度。如果矮的话，就取当前点的高度，因为当前点是短板。

重复上述步骤直至队列为空，我们就可以求出到底能盛放多少水。


```java
public class Solution {
  public int maxTrapped(int[][] matrix) {
   // Assumptions: matrix is not null, has size of M * N,
   // M > 0 & N > 0, all the values are non-negative integers.
    int rows = matrix.length;
    int cols = matrix[0].length;
    if (rows < 3 || cols < 3) {
      return 0;
    }
    // Best-First-Search, minHeap maintains all the border cells
    // of the "closed area" and we always find the one with lowest
    // height to see if any of its neighbors can trap any water.
    PriorityQueue<Pair> minHeap = new PriorityQueue<Pair>();
    boolean[][] visited = new boolean[rows][cols];
    // put all the border cells of the matrix at the beginning
    processBorder(matrix, visited, minHeap, rows, cols);
    int result = 0;
    while (!minHeap.isEmpty()) {
      Pair cur = minHeap.poll();
      List<Pair> neighbors = allNeighbors(cur, matrix, visited);
      for (Pair nei : neighbors) {
        if (visited[nei.x][nei.y]) {
          continue;
        }
        // adjust the neighbor cell's height to the current water level
        // if necessary, mark the neighbor cell as visited, and put the
        // neighbor cell into the min heap.
        visited[nei.x][nei.y] = true;
        // how much water can be trapped at the neighbor cell.
        // the maximum water level currently is controlled by the cur cell.
        result += Math.max(cur.height - nei.height, 0);
        nei.height = Math.max(cur.height, nei.height);
        minHeap.offer(nei);
      }
    }
    return result;
  }
  // put all the border cells into the min heap at the very beginning,
  // these are the start points of the whole BFS process.
  private void processBorder(int[][] matrix, boolean[][] visited, PriorityQueue<Pair> minHeap, int rows, int cols) {
    for (int j = 0; j < cols; j++) {
      minHeap.offer(new Pair(0, j, matrix[0][j]));
      minHeap.offer(new Pair(rows - 1, j, matrix[rows - 1][j]));
      visited[0][j] = true;
      visited[rows - 1][j] = true;
    }
    for (int i = 1; i < rows - 1; i++) {
      minHeap.offer(new Pair(i, 0, matrix[i][0]));
      minHeap.offer(new Pair(i, cols - 1, matrix[i][cols - 1]));
      visited[i][0] = true;
      visited[i][cols - 1] = true;
    }
  }
    private List<Pair> allNeighbors(Pair cur, int[][] matrix, boolean[][] visited) {
    List<Pair> neis = new ArrayList<>();
    if (cur.x + 1 < matrix.length) {
      neis.add(new Pair(cur.x + 1, cur.y, matrix[cur.x + 1][cur.y]));
    }
    if (cur.x - 1 >= 0) {
      neis.add(new Pair(cur.x - 1, cur.y, matrix[cur.x - 1][cur.y]));
    }
    if (cur.y + 1 < matrix[0].length) {
      neis.add(new Pair(cur.x, cur.y + 1, matrix[cur.x][cur.y + 1]));
    }
    if (cur.y - 1 >= 0) {
      neis.add(new Pair(cur.x, cur.y - 1, matrix[cur.x][cur.y - 1]));
    }
    return neis;
  }

  static class Pair implements Comparable<Pair> {
    int x; // row index.
    int y; // column index.
    int height; // height of the cell in the original matrix.

    Pair(int x, int y, int height) {
      this.x = x;
      this.y = y;
      this.height = height;
    }

    @Override
    public int compareTo(Pair another) {
      if (this.height == another.height) {
        return 0;
      }
      return this.height < another.height ? -1 : 1;
    }
  } 
}

//Time: O(mnlog(m+n)) 
//Space: O(mn)


```

**Examples**

{ { 2, 3, 4, 2 },

 { 3, **1, 2,** 3 },

 { 4, 3, 5, 4 } }

the amount of water can be trapped is 3, 

at position (1, 1) there is 2 units of water trapped,

at position (1, 2) there is 1 unit of water trapped.