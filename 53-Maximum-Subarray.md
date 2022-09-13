# 53. Maximum Subarray

给定一个数组，计算出和最大的子数组。

## DP Approach

经典DP思路，我们用`sum int来存放子问题答案。`sum[i]`表示以`i`下标结尾的子数组最大和是多少。那么显然，`sum[0]`就是`array[0]`。

接着，我们从1开始遍历到最后，那么我们目前的元素可以从之前的子数组获得正数和，那么就计算`i`结尾的最大子数组和`。如果`sum[i]`小于目前的array[i]话，那么之前的子数组只会拖我们后腿，所以`sum[i]`果断就等于`array[i]`。

用一个`maxSubSum`变量来记录全局最大和，得到`sum[i]`之后不断地更新全局最大和，这样我们最后就可以得到最大的子数组之和。

Time complexity: O(N)

Space complexity: O(1)

```java
public class Solution {
  public int largestSum(int[] array) {
    // Use a gloabal max to keep record of the max sum while traversing the array
    // Decide add the current element or not, if sum < 0 then not add
    int sum = array[0];
    int result = array[0];
    for (int i = 1; i < array.length; i++) {
      sum = Math.max(array[i], sum + array[i]);
      result = Math.max(sum, result);
    }
    return result;
  }
}

//tc: O(n)
//sc: O(1)
```

## Greedy Approach

这题还是可以用贪心思想来解决，用`currSum`代表目前已`i`结尾的最大子数组和，用`currMaxSum`来记录答案。那么显然，`currSum`刚开始可以赋值为`nums[0]`，`currMaxSum`也是。

我们从第二个元素开始，如果`currSum`大于0，代表前一个`i`结尾的最大子数组和是大于0的，就可以为我所用，那么`currSum`就可以更新为`currSum + nums[i]`。否则，之前的`currSum`只会拖后腿，那么以当前`i`结尾的最大子数组和就是`nums[i]`，赋值给`currSum`。每轮循环结束时候，更新一下答案。

这样我们最后就可以得到最大子数组和。

Time complexity: O(N)

Space complexity: O(1)

```java
class Solution {
  public int maxSubArray(int[] nums) {
    int currSum = nums[0];
    int currMaxSum = currSum;
    for (int i = 1; i < nums.length; i++) {
      if (currSum > 0) {
        currSum += nums[i];
      } else {
        currSum = nums[i];
      }
      currMaxSum = Math.max(currMaxSum, currSum);
    }
    return currMaxSum;
  }
}
```