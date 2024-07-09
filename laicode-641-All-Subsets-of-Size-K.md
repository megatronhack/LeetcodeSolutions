# Laicode 641. All Subsets II of Size K

给定一个字符串，求出所有长度为k的子集。

这题结合[laicode 640. All Subsets of Size K](laicode-640-All-Subsets-of-Size-K.md)和[90. Subsets II](90-Subsets-II.md)两个思路，前者用来借鉴求k个元素的子集，后者来借鉴处理重复元素的情况。

Time complexity: O(2^N). N is the length of the string. We have to iterate all subsets and find the subset with k elements to add them into the result list.

Space complexity: O(N). N level call stack.

```java
public class Solution {
  public List<String> subSetsIIOfSizeK(String set, int k) {
    // Use the DFS to solve this question
    // Change the input set into a char array, and sorted this array then traverse all the elements
    // At each layer decide add the current element or not, if not need to dedupliacate
    // tc: O(2^n) sc: O(n)
    List<String> result = new ArrayList<>();
    if (set == null) {
      return result;
    }
    char[] array = set.toCharArray();
    Arrays.sort(array);
    StringBuilder sb = new StringBuilder();
    helper(array, sb, 0, result, k);
    return result;
  }

  private void helper(char[] array, StringBuilder sb, int index, List<String> result, int k) {
    //base case
    if (index == array.length) {
      if (sb.length() == k) {
        result.add(sb.toString());
      }
      return;
    }
    //if choose to add the current element
    helper(array, sb.append(array[index]), index + 1, result, k);
    sb.deleteCharAt(sb.length() - 1);
    //if we choose not to add the current element, need to deduplicate
    while (index + 1 < array.length && array[index] == array[index + 1]) {
      index++;
    }
    helper(array, sb, index + 1, result, k);
  }
}
```

**Examples**

Set = "abc", K = 2, all the subsets are [“ab”, “ac”, “bc”].

Set = "abb", K = 2, all the subsets are [“ab”, “bb”].

Set = "abab", K = 2, all the subsets are [“aa”, “ab”, “bb”].

Set = "", K = 0, all the subsets are [""].

Set = "", K = 1, all the subsets are [].

Set = null, K = 0, all the subsets are [].