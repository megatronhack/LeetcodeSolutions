# Laicode 106. Largest SubMatrix Sum

给定一个二维数组，找出和最大的子矩阵。

这题可算是非常经典的动态规划题了，难度比较大。我们可以针对每一列来计算他们的prefix sum，这样我们就可以快速计算指定列的任意行范围的和，即`a[top][j] + a[top + 1][j] + ... + a[bottom][j]`。

有了这个之后，我们可以用双重for循环遍历所有的top行和bottom行的搭配。对于每个搭配，我们求出每一列对应的`[top, bottom]`行的和，得到一个一维数组。这样我们只要求出这个一维数组的最大子数组和，就可以知道对于top行和bottom行夹着的部分，最大子矩阵和是多少。等我们遍历的所有的`top`和`bottom`搭配之后，我们就知道整个矩阵里最大子矩阵和是多少了。

Time complexity: O(M * M * N)

Space complexity: O(M * N)

```java
public class Solution {
  public int largest(int[][] matrix) {
    int n = matrix.length;
    int m = matrix[0].length;
    int result = Integer.MIN_VALUE;
    for (int i = 0; i < n; i++) {
      int[] cur = new int[m];
      for (int j = i; j < n; j++) {
        //for each row i, we add the rows one by one for row j
        // to make sure each time we only introduce o(n) time
        add(cur,matrix[j]);
        //for each possible pair of rows i, j
        //we would like to know what is the largest submatrix sum 
        //using top row as row i and bottom row as row j
        //we "flatten" these area to a one dimensional array
        result = Math.max(result,max(cur));
      }
    }
    return result;
  }

  private void add(int[] cur, int[] add) {
    for (int i = 0; i < cur.length; i++) {
      cur[i] += add[i];
    }
  }

  private int max(int[] cur) {
    int result = cur[0];
    int tmp = cur[0];
    for (int i = 1; i < cur.length; i++) {
      tmp = Math.max(tmp + cur[i], cur[i]);
      result = Math.max(result, tmp);
    }
    return result;
  }
}
//Time: O(n*m*m)
//Space: O(n*m)

```