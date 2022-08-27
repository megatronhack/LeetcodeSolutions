# 378. Kth Smallest Element in a Sorted Matrix

题目给定一个横竖都有序的矩阵，要求找到第K小的数。

这题典型的BFS搜索，配合堆的使用，这次我们用`Java`的`PriorityQueue`来替代手写堆。这里堆里存坐标，但是是根据坐标对应在矩阵里面的值进行排序，所以我们实现优先队列的时候需要自定义一个`Comparator`。此外，我们还需要一个同等大小的vis矩阵来记录当前坐标是否被访问过，以防止重复访问。

从(0, 0)开始BFS搜索，每次把堆顶的坐标(x, y)弹出来，将它未访问过的(x + 1, y)和(x, y + 1)邻居放入队列，并把他们标记为已访问。如此循环`k-1`次，那么此时堆顶的坐标就是这个矩阵里第`k`小的元素了。

Time complexity: O(klogk)，因为会重复k-1次，堆最多不到2k个元素，所以offer操作需要logk的复杂度。

Space complexity: O(k + mn)，堆里会有不到2k个元素，额外的需要一个和矩阵同等大小mn的vis数组来记录访问情况。

```java
public class Solution {
  public int kthSmallest(int[][] matrix, int k) {
    // Write your solution here
    int rows = matrix.length;
    int column = matrix[0].length;
    //BFS, need a minheap on the value of each cells
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(k, new Comparator<Cell>(){
      @Override
      public int compare (Cell c1, Cell c2){
        if (c1.value == c2.value){
          return 0;
        }
        return c1.value < c2.value ? -1 : 1;
      }
    });
    //all the generated cells will be marked true, to avid being generated more than once
    boolean[][] visited = new boolean[rows][column];
    minHeap.offer(new Cell(0, 0, matrix[0][0]));
    visited[0][0] = true;
    //iterate k-1 rounds, and BFS the smallest k-1 cells
    for (int i = 0; i < k -1; i++){
      Cell cur = minHeap.poll();
      //the neighbor cell will be inserted back to the minheap only if 
      //1. it is not out of boundary
      //2. it has not been generated before
      //Because for each cell it could be generated twice
      if (cur.row +1 < rows && !visited[cur.row + 1][cur.column]){
        minHeap.offer(new Cell(cur.row +1, cur.column, matrix[cur.row + 1][cur.column]));
        visited[cur.row + 1][cur.column] = true;
      }
      if (cur.column +1 < column && !visited[cur.row][cur.column +1]){
        minHeap.offer(new Cell(cur.row, cur.column+1, matrix[cur.row][cur.column + 1]));
        visited[cur.row][cur.column +1] = true;
      }
    }
    return minHeap.peek().value;
  }
  static class Cell{
    int row;
    int column;
    int value;
    Cell(int row, int column, int value){
      this.row = row;
      this.column = column;
      this.value = value;
    }
  }

}

//Time: O(klogk)
//Space: O(mn + k) where m is the row of matrix, n is the column of the matrix
```