# 54. Spiral Matrix

## Recursive Approach

**Examples**

{ {1,  2,  3},

 {4,  5,  6},

 {7,  8,  9} }

the traversal sequence is [1, 2, 3, 6, 9, 8, 7, 4, 5]

给定一个`n * n`的矩阵，将它的元素旋转输出。

那么我们先实现一个辅助方法，给定一个矩阵以及边界范围，旋转输出最外层的数字。这并不难，只要控制好四个循环的边界，就可以将最外层旋转输出。

接着我们就将矩阵的行列边界向内收缩，一层一层的剥开矩阵就可以得到想要的序列了。

Time complexity: O(n)

Space complexity: O(min(m, n)), because of the call stack.

```java
public class Solution {
  public List<Integer> spiral(int[][] matrix) {
    // Write your solution here
    List<Integer> result = new ArrayList<Integer>();
    recursiveTraverse(matrix, 0 , matrix.length, result);
    return result;
  }
  private void recursiveTraverse(int[][] matrix, int offset, int size, List<Integer> result) {
    //base case stop
    if (size == 0) {
      return;
    }
    // base case print 5
    if (size == 1) {
      result.add(matrix[offset][offset]);
      return;
    }
    //print 1 2
    for (int i = 0; i < size - 1; i++) {
      result.add(matrix[offset][offset + i]);
    }
    //print 3 6 
    for (int i = 0; i < size - 1; i++) {
      result.add(matrix[offset + i][offset + size - 1]);
    }
    //print 9 8
    for (int i = size - 1; i >= 1; i--){
      result.add(matrix[offset + size - 1][offset + i]);
    }
    //print 7 4  
    for (int i = size - 1; i >= 1; i--) {
      result.add(matrix[offset + i][offset]);
    }
    //recursion to base case
    recursiveTraverse(matrix, offset + 1, size - 2, result);
  }
}
//Time: O(n*n)
//Space: O(n)

```