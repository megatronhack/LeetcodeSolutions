# 1004. Max Consecutive Ones III

给定一个只有0和1组成的数组，允许你最多把K个0变成1，找到最长的连续1子数组长度。

允许最多把K个0变成1，那也其实就是说找到最长的连续1的子数组，它里面最多可以有K个0。那么这题其实还是滑动窗口的问题。

**Example 1: **input: array = [1,1,0,0,1,1,1,0,0,0], k = 2

traverse这个array，count用来记录已经翻转的次数flip chance, 通过fast和slow指针记录当前的sliding window。

如果当前array[i]的数值为 1， 则需移动fast指针并update longest的值。

如果当前array[i]的数值不为1, 2个case

case 1: 如果还有翻转次数的话（flip chance < k）, 则使用翻转机会, 并且记录次数(count++) , update longest 的值。 

case 2: 如果没有翻转次数，则移动slow指针。并判断当前slow指针array[slow]是否为0，翻转次数-1（count--）。 这么做的目的是，如果fast指针停滞，fast - slow之间的移动窗口我需要保证移动窗口向前走，并同时记录longest的值。

Time complexity: O(N), we access each character at most twice.

Space complexity: O(1).

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
    // Use a sliding window to move and update the longest value
    int slow = 0;
    int fast = 0;
    int longest = 0;
    int count = 0;//need a count to keep track of the flip count
    while (fast < nums.length) {
      if (nums[fast] == 1) {
        fast++;
        longest = Math.max(longest, fast - slow);
      } else if (count < k) {//when mums[fast] != 1 and we still have flip chances to change 0 to 1
        count++;
        fast++;
        longest = Math.max(longest, fast - slow);
      } else if (nums[slow++] == 0){
        //put num[slow++] in the condition which means whether nums[slow] == 0 or not slow++
        //if the nums[slow] == 0 which means we get one more flip chance
        count--;
        }
      }
     return longest;
  }
}
```