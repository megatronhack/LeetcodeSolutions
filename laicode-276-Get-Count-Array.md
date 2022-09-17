# Laicode 276. Get Count Array

给定一个无序数组，返回每个元素右边比它小的元素个数。这题有点难，不想做可以跳过。

所以直接暴力解。

Time complexity: O(N^2)

Space complexity: O(N)

```java
public class Solution {
  public int[] countArray(int[] array) {
    // Write your solution here
    //暴力解
    int[] newArray = new int[array.length];
    for(int i = 0; i < array.length; i++){
      int count = 0;
      for(int j = i + 1; j < array.length; j ++){
        if (array[j] < array[i]){
         count++;
        }
      }
    newArray[i] = count;  
    }
  return newArray;
  }
}
//time on^2
//space on
```

- A = { 4, 1, 3, 2 }, we should get B = { 3, 0, 1, 0 }.