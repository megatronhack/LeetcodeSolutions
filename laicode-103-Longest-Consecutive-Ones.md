# Laicode 103. Longest Consecutive 1s

给定一个只有01的数组，求出最长全1子数组的长度。

## DP Approach

简单的动态规划，`max`存放子问题的答案，`result`的意义是最长全1子数组长度。

Time complexity: O(N)

Space complexity: O(1)

```java
public class Solution {
  public int longest(int[] array) {
    // Write your solution here
    int max = 0;
    int result = 0;
    for (int i = 0; i <array.length; i++){
      if (array[i] == 0){
        max = 0;
      }
      else{
        max = max + 1;
        result = Math.max(result, max);
      }     
    } 
    //return
    return result;
  }
}
//time on
//space o1
```

## Greedy Approach

贪心思想来解决，`st`记录当前全1子数组的起始下标，初始化为`-1`。`i`从头开始向后遍历，如果`array[i]`是0，那么`st`必然不可能是`i`，至少得从后一个开始。如果`array[i]`是1，那么先看看`st`是否还是`-1`，如果是的话，说明这是数组里第一个1，我们要对`st`进行赋值。然后再去计算最长的全1子数组长度。

Time complexity: O(N)

Space complexity: O(1)

```java
public class Solution {
  public int longest(int[] array) {
    if (array == null || array.length == 0) {
      return 0;
    }
    int n = array.length;
    int st = -1;
    int res = 0;
    for (int i = 0; i < n; i++) {
      if (array[i] == 0) {
        st = i + 1;
      } else {
        if (st == -1) {
          st = i;
        }
        res = Math.max(res, i - st + 1);
      }
    }
    return res;
  }
}
```