# Laicode 176. Longest Common Substring

给定两个字符串找出最长公共子串。

双重for循环遍历，最后就可以得到最长的公共子串的长度和末端位置，最后可以得到最长公共子串。

Time complexity: O(m * n)

Space complexity: O(m * n)

```java
public class Solution {
  public String longestCommon(String source, String target) {
    // Write your solution here
    char[] a = source.toCharArray();
    char[] b = target.toCharArray();
    int[][] matrix = new int[a.length][b.length];
    int longest = 0;
    int start = 0;
    for (int i = 0; i < a.length; i++){
      for(int j = 0; j < b.length; j++){
        if (a[i] == b[j]){
          if(i == 0 || j == 0){
              matrix[i][j] = 1;
          }
          else{
            matrix[i][j] = matrix[i-1][j-1] + 1;
          }
            //record start and end
         if(matrix[i][j] > longest){
          longest = matrix[i][j];
          start = i - longest + 1;
          }
        }
      }
    }
    return source.substring(start, start + longest);


    //
  }
  //time o m*n
  //space o m*n
}

```