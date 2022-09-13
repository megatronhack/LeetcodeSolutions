# 221. Maximal Square

给定一个0/1矩阵，求出里面最大全1正方形的面积。

经典DP题，用maxSq数组来存放子问题的答案，`maxSq[i][j]`表示以`matrix[i][j]`为右下角的全1正方形最大周长。那么`matrix[i][j]`如果为0的话，周长就是0。如果`matrix[i][j]`为1的话，`matrix[i][j]`就来自于`[i - 1][j - 1]`，`[i - 1][j]`和`[i][j - 1]`里面最小的全1正方形边长再加1。但是如果`i`和`j`有一个为0，那么`maxSq[i][j]`就取决于`matrix[i][j]`是否为1。

如此一来，我们可以算出以每个`[i][j]`为右下角的最大全1正方形周长，我们就可以得到整个矩阵里最大的全1正方形的周长，从而计算出面积。

**Examples**

{ {0, 0, 0, 0},

 {1, **1, 1,** 1},

 {0, **1, 1,** 1},

 {1, 0, 1, 1}}

the largest square of 1s has length of 2

Time complexity: O(M * N).

Space complexity: O(M * N).

```java
public class Solution {
  public int largest(int[][] matrix) {
    // Assuptions: the matrix is a binary matrix (only contains 0 or 1 as the values)
    //it is not null and has size n*n
    int n = matrix.length;
    if (n == 0) {
      return 0;
    }
    int result = 0;
    //dp[i][j] means the largest squares of 1's with right bottom
    //cornrt as matrix[i][j]
    int[][] largest = new int[n][n];
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        if (i == 0 || j == 0) {
          largest[i][j] = matrix[i][j] == 1 ? 1:0;
        } else if (matrix[i][j] == 1) {
          largest[i][j] = Math.min(largest[i][j-1] + 1, largest[i-1][j] + 1);
          largest[i][j] = Math.min(largest[i -1][j -1] + 1, largest[i][j]);
        }
        result = Math.max(result, largest[i][j]);
      }
    }
    return result;
  }
}

//Time:O(n*n)
//Space:O(n*n)

```