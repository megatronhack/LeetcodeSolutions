# 1139. Largest 1-Bordered Square

给出一个01二位矩阵，求出最大的以1为边的正方形面积。

这题还是动态规划的思路，针对每个坐标`(i, j)`都求出以它为左上角的最大1边正方形的边长。

建立2个matrix，左>右 matrix   + 上>下matrix 。  

最后看2个matrix里对应的正方形，进行for loop，一圈圈缩小。如果正方形都>=Math.min取到的边长，就证明其是一个正方形，并把边长存下来。用个result来记录/update历史最大边长。

返回边长的平方作为面积。

1st direction (left → right):     	 

{'1', '0', '1', ‘2', '3'},         

 {'1', '2', '3', '4', '5'},                 

 {'1', '2', '0', '1', '0'},         

 {'1', '2', '3', ‘4,’ '5'},         

 {'1', '2', '3', '0', '0'},          

3rd direction (top → bottom): 

 {'1', '0', '1', ‘1', '1'},          

{'2', '1', '2', '2', '2'},                  

{'3', '2', '0', '3', '0'},         

{'4', '3', '1', ‘4,’ '1'},        

 {'5', '4', '2', '0', '0'},  

![1139. Largest 1-Bordered Square](assets\images\1139. Largest 1-Bordered Square.jpg)

Time complexity: O(n^3)

Space complexity: O(M * N)


```java
public class Solution {
  public int largestSquareSurroundedByOne(int[][] matrix) {
    //Assumptions: matrix is not null and size of m*n where m, n >= 0
    int m = matrix.length;
    int n = matrix[0].length;
    int result = 0;
    if (m == 0 || n == 0) {
      return result;
    }
    int[][] left = new int[m+1][n+1];
    int[][] up = new int[m+1][n+1];
    for (int i = 0; i < m; i++) {
      for (int j = 0; j < n; j++) {
        if (matrix[i][j]  == 1) {
          //the longest left arm length ending at each position in the matrix
          //we here apply a trick for ease of later processing:
          //left[i][j] is actually mapped to matrix[i-1][j-1], this will reduce the corner cases
          left[i + 1][j + 1] = left[i + 1][j] + 1;
          up[i + 1][j + 1] = up[i][j + 1] + 1;
          //the maximum length of a surrounded by 1 matrix with rightbottom position at matrix[i][j]
          //is determined by the min value of left[i+1][j+1] adn up[i+1][j+1]
          //we check one by one all the possible lengths if it can provide the actual matrix
          //we only need to check the longest left arm length of the righttop cell 
          //and the longest up arm length of the leftbottom cell
          for (int maxLength = Math.min(left[i+1][j+1], up[i+1][j+1]); maxLength >= 1; maxLength--) {
            if (left[i + 2 - maxLength][j + 1] >= maxLength && up[i + 1][j + 2 - maxLength] >= maxLength) {
              result = Math.max(result, maxLength);
              break;
            }
          }
        }
      }
    }
    return result;
  }
}

//Time: O(n*m*min(n,m))
//Space: O(n*m)

```