# 55. Jump Game

给定一个数组的数字，每个下标的数字代表这个下标的地方能往后走几步。问从0开始，是否能走到最后一个下标。

**Examples**

- {1, 3, 2, 0, 3}, we are able to reach the end of array(jump to index 1 then reach the end of the array)
- {2, 1, 1, 0, 2}, we are not able to reach the end of array

## DP Approach

这题可以用动态规划的思想来解决，用`reachEnd`数组来存放子问题答案。`reachEnd[i]`表示`i`是否可以走到最后一个下标，`true`就是可以，`false`就是不可以。

`reachEnd[len - 1]`肯定是true，它自己就是最后一个下标。

我们从倒数第二个下标开始往前推，每到一个下标为`i`的地方，就看看`[i + array[i]`自己的index到end index这个范围里有没有能走到最后的下标，如果有的话就代表`i`可以走到最后。

如果没有，就说明`i`不可以走到最后。就查询目前我们能不能跳到之前已经推算过的地方，如果有跳到之前任意为true的地方，我们就设为true。 直到最后，我们就可以知道它到底可不可以走到最后。

Time complexity: O(N^2)

Space complexity: O(N)

```java
public class Solution {
  public boolean canJump(int[] array) {
    // canJump[i] means from index i can jump to index array.length - 1
    //Assumptions: array is not null and is not empty
    if (array.length == 1) {
      return true;
    }
    boolean[] canJump = new boolean[array.length];
    for (int i = array.length - 2; i >= 0; i--) {
      //if from index i, it is already possible to jump to the end of the array
      if (i + array[i] >= array.length - 1) {
        canJump[i] = true;
      } else {
      //if any of the reachable indeices from index i is reachable to the end of the array
      for (int j = array[i]; j >= 1; j--) {
        if (canJump[j + i]) {
          canJump[i] = true;
          //break;
        }
      }
      }
    }
    return canJump[0];
  }
}
//Time: O(n^2)
//Space: O(n)

```

## Greedy Approach

这题也可以用贪心思想来解决，不过需要注意的是不是所有的动态规划都可以用贪心思想来做。满足贪心思想方法的动态规划需要满足几个条件，在这里不赘述，算法导论里有讲。

我们用`currReachable`代表目前走过的下标最远可以到达哪个下标。那么既然是从0出发，那么一开始currReachable自然初始化为0。如果当前`i`已经超过了`currReachable`说明之前所有的下标都没有办法走到这里，也就自然无法到达最后。否则，我们时刻更新currReachable，取它自己和`i + nums[i]`里的大的那一个。

只要循环能顺利结束，就说明可以走到最后。

Time complexity: O(N)

Space complexity: O(1)

```java
class Solution {
  public boolean canJump(int[] nums) {
    int currReachable = 0;
    for (int i = 0; i < nums.length; i++) {
      if (i > currReachable) {
        return false;
      }
      currReachable = Math.max(currReachable, i + nums[i]);
    }
    return true;
  }
}
```