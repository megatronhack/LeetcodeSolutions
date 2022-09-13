# Laicode 104. Longest Cross Of 1s

给定一个01二位矩阵，找出其中最大的全1十字架的尺寸。全1十字架是四边是等长的，如果不等长则取最短的那个边的长度作为该十字架的尺寸。

这题也依然可以用动态规划来解决，对于每个坐标`(i, j)`我们可以提前计算出`(i, j)`上下左右包括它自己在内各自有多少个1。有了这些数据之后，我们就可以计算以每个坐标为中心的十字架尺寸，从而可以得到最长的十字架尺寸。

左方和上方的`1`长度可以一起计算，我们可以从左上遍历到右下，这样子左方和上方就可以一起计算。同理，我们再从右下遍历到左上，那么下方和右方也可以一起计算。当然了，左方和上方可以合并到一起，右方和下方也可以合并到一起，取短边的长度就好。最后我们把左上和右下接着取短边合并到一起，就可以得到四边里面最短的，那么也就得到了以每个坐标为中心的十字架尺寸。

最后，我们就可以得到最大的十字架尺寸。

Time complexity: O(M * N)

Space complexity: O(M * N)

```java
public class Solution {
  public int largest(int[][] matrix) {
    //Assumptions: matrix is not null and has size of N*M where N >= 0 and M >= 0
    //create a matrix to keep records of the size of the cross at M[i][j]
    //return the global max
    int n = matrix.length;
    int m = matrix[0].length;
    if (n == 0 || m == 0) {
      return 0;
    }
    //leftup records the longest possible length for left and up arms ending at each cells in the matrix
    int[][] leftUp = leftUp(matrix,n,m);
    //rightdown records the longest possible length for right and down arms ending at each cells in the matrix
    int[][] rightDown = rightDown(matrix,n,m);
    return merge(leftUp, rightDown, n, m);
  }

  //Use a merge function to get the minvalue of the corresponding cells in the two matrix
  //Update the global max value among all the cells in the merged function
  private int merge(int[][] leftUp, int[][] rightDown, int n, int m) {
    int result = 0;
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        leftUp[i][j] = Math.min(leftUp[i][j], rightDown[i][j]);
        result = Math.max(result, leftUp[i][j]);
      }
    }
    return result;
  }
  //calculate the max possible length of left and up arms for each of the cells in the matrix
  private int[][] leftUp(int[][] matrix, int n, int m) {
    int[][] left = new int[n][m];
    int[][] up = new int[n][m];
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        if (matrix[i][j] == 1) {
          if (i == 0 && j == 0) {
            up[i][j] = 1;
            left[i][j] = 1;
          } else if (i == 0) {
            up[i][j] = 1;
            left[i][j] = left[i][j-1] + 1;
          } else if (j == 0) {
            up[i][j] = up[i-1][j] + 1;
            left[i][j] = 1;
          } else {
            up[i][j] = up[i-1][j] + 1;
            left[i][j] = left[i][j-1] + 1;
          }
        }
      }
    }
    //merge left and up return the merges matrix
    merge(left, up, n, m);
    return left;
  }

  private int[][] rightDown(int[][] matrix, int n, int m) {
    int[][] right = new int[n][m];
    int[][] down = new int[n][m];
    for (int i = n-1; i >= 0; i--) {
      for (int j = m-1; j >= 0; j--) {
        if (matrix[i][j] == 1) {
          if (i == n - 1 && j == m - 1) {
            right[i][j] = 1;
            down[i][j] = 1;
          } else if (i == n - 1) {
            right[i][j]  = right[i][j+1] + 1;
            down[i][j]  = 1;
          } else if (j == m - 1) {
            right[i][j]  = 1;
            down[i][j]  = down[i+1][j] + 1;
          } else {
            right[i][j] = right[i][j+1] + 1;
            down[i][j] = down[i+1][j] + 1;
          }
        }
      }
    }
    merge(right, down, n, m);
    return right;
  }
}
//Time:O(n*m)
//Space:O(n*m)

```