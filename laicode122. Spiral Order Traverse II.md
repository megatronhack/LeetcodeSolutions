## 122. Spiral Order Traverse II

## Iterative Approach

 和 [54. Spiral Matrix](54-Spiral-Matrix.md)相似，那道题是N*N，这个是M*N的matrix

{ {1,  2,  3,  4},

 {5,  6,  7,  8},

 {9, 10, 11, 12} }

the traversal sequence is [1, 2, 3, 4, 8, 12, 11, 10, 9, 5, 6, 7]

那么我们先实现一个辅助方法，给定一个矩阵以及边界范围，旋转输出最外层的数字。这并不难，只要控制好四个循环的边界，就可以将最外层旋转输出。

接着我们就将矩阵的行列边界向内收缩，一层一层的剥开矩阵就可以得到想要的序列了。

给定一个`m * n`的矩阵，将它的元素旋转输出。

//Time: O(M*N)
//Space: O(1)

```java
public class Solution {
  public List<Integer> spiral(int[][] matrix) {
    // Traverse the matrix and put elements in the list and return
    List<Integer> result = new ArrayList<Integer>();
    int m = matrix.length;
    if (m == 0) {
      return result;
    }
    int n = matrix[0].length;
    //define the boundary of the matrix and add elements in order
    int left = 0;
    int right = n - 1;
    int up = 0;
    int down = m - 1;
    while (left < right && up < down) {
      for (int i = left; i <= right; i++) {
        result.add(matrix[up][i]);
      }
      for (int i = up + 1; i <= down - 1; i++) {
        result.add(matrix[i][right]);
      }
      for (int i = right; i >= left; i--) {
        result.add(matrix[down][i]);
      }
      for (int i = down - 1; i >= up + 1; i--) {
        result.add(matrix[i][left]);
      }
      left++;
      right--;
      up++;
      down--;
    }
    //if there is nothing left
    if (left > right || up > down) {
      return result;
    }
   //if there is one column left 
    if (left == right) {
      for (int i = up; i <= down; i++) {
        result.add(matrix[i][left]);
      } 
     }
     //if there is one row left
      else {
      for (int i = left; i <= right; i++) {
        result.add(matrix[up][i]);
      }
    }
    return result;
  }
}
//Time: O(M*N)
//Space: O(1)

```

