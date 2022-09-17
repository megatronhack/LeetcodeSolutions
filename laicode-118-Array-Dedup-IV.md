# Laicode 118. Array Deduplication IV

给定一个有重复元素的数组，不断地去掉所有相邻的重复元素，直到没有相邻的重复元素为止。比如`[1,2,3,3,3,2,2]` -> `[1,2,2,2]` -> `[1]`。

那么这题依然是双指针，`[0, slow)`记录着去重之后的部分，`fast`指向当前要处理的元素。

`array[fast] ！= array[slow - 1]`，slow和fast同时前进。

否则，`array[fast] == array[slow - 1]` 意味着当前元素本身有重复元素，slow退一步，fast前进到到不同的元素

{1, 2, 3, 3, 3, 2, 2} → {1, 2, 2, 2} → {1}, return {1}

Time complexity: O(N)

Space complexity: O(1)，如果答案不算入的话。

```java
public class Solution {
  public int[] dedup(int[] array) {
    // case 1 : if a[f] != a[s - 1], a[s++] = a[f++] 
    // case 2: if a[f] == a[slow - 1] keep traverse fast++ until a[f] != a[slow - 1], then slow--
    //what if slow = 0? should handle this corner case
    if (array == null || array.length <= 1) {
      return array;
    }
    int slow = 1;
    int fast = 1;
    while (fast < array.length) {
      if (slow == 0 || array[fast] != array[slow - 1]){
        array[slow++] = array[fast++];
      } else if(array[fast] == array[slow - 1]) {
        while (fast < array.length && array[fast] == array[slow - 1]) {
          fast++;
        }
        slow--;
      } 
    }
    return Arrays.copyOf(array, slow);
  }
}
//TC: O(n)
//SC: O(1)

```