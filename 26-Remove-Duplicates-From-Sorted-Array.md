# 26. Remove Duplicates from Sorted Array

给定一个升序数组，在原数组内部清除所有重复元素，返回清除后还剩多少个元素。

这个其实和[laicode 79. Remove Adjacent Repeated Characters I](laicode-79-Remove-Adjacent-Repeated-Chars-I.md)差不多思路，也是快慢指针。`[0, slow)`记录着`[0, i)`去重之后的元素，如果目前`i`对应的元素和`slow - 1`对应的元素不一样的话，就加入，否则就跳过。

Time complexity: O(N)

Space complexity: O(1)

```java
class Solution {
  public int removeDuplicates(int[] nums) {
    if (nums.length <= 1) {
      return nums.length;
    }
    int slow = 1;
    for (int i = 1; i < nums.length; i++) {
      if (nums[i] != nums[slow - 1]) {
        nums[slow++] = nums[i];
      }
    }
    return slow;
  }
}
```

xxxxxxxxxx public class Solution {  public List<String> validParentheses(int n) {    // Write your solution here    //char[] ||  StringBuilder || left index ||right index    List<String> result = new ArrayList<String>();    StringBuilder sb = new StringBuilder();    helper(result, 0, 0, sb, n);    return result;  }​  private void helper(List<String> result, int left, int right, StringBuilder sb, int n){    //base case    if (left == n && right == n){      result.add(sb.toString());      return;    }    //when to add'('    if (left < n){      sb.append('(');      helper(result,left + 1, right, sb, n);      sb.deleteCharAt(sb.length() - 1);    }    //when to add')'    if (right < left){      sb.append(')');      helper(result, left, right + 1, sb, n);      sb.deleteCharAt(sb.length() - 1);    }  }}​java

On

o1

```
public class Solution {
  public int[] dedup(int[] array) {
    // Write your solution here
    if (array.length <= 1){
      return array;
    }
    int slow = 1;
    for (int i = 1; i < array.length; i++){
      if (array[i] != array[slow - 1] )
       array[slow++] =  array[i];
      }

   return Arrays.copyOf(array,slow);
  }
}
```

