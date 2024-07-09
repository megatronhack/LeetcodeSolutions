# 90. Subsets II

和[78. Subsets](78-Subsets.md)差不多，但是这里的元素有重复，但是题目要求子集不能有重复。

这里我们好好思考一下，假设数组里里有5个`1`，那么按照78题的思路，每个位置分用和不用两种情况，一定会导致有重复子集。比如第一个1选择用，后面的1选择不用这一情况，会和第二个1选择用，其余的1不用，这个情况重复。这两种情况都只会在子集里出现一个`1`。

当前的1一定会分用和不用这两种情况，用的时候，后面的1可以用，也可以不用。当不用的时候，后面的也一定不可以用，否则就会产生重复。所以当前元素不用的时候，后面所有相同元素也要跳过。其余的就和普通求子集一样了，不过要注意的是这题没说相同元素也会响铃，所以我们需要先sort一下。

Time complexity: O(2^n).

Space complexity: O(n), n level call stack for DFS and sort.

```java
public class Solution {
  public List<String> subSets(String set) {
    //Use the DFS to solve this question
    //Turn the input string into a char array
    //For each layer, decide whether to add that element or not
    //Need to deduplicate for some branched if choose not to add the duplicate element
    List<String> result = new ArrayList<>();
    if (set == null) {
      return result;
    }
    char[] array = set.toCharArray();
    Arrays.sort(array);
    StringBuilder sb = new StringBuilder();
    dfs(array, 0, sb, result);
    return result;
  }

  private void dfs(char[] array, int index, StringBuilder sb, List<String> result) {
    //base case
    if (index == array.length) {
      result.add(sb.toString());
      return;
    }
    //recursion rule
    //choose to add the element at current layer
    dfs(array, index + 1, sb.append(array[index]), result);
    sb.deleteCharAt(sb.length() - 1);
    //need to deduplicate when choose not to add the element and the element is the same with the following one
    while (index + 1 < array.length && array[index] == array[index + 1]) {
      index++;
    }
    //choose not to add the current element
    dfs(array, index + 1, sb, result);
  }
}
//tc: O(2^n)
//sc: O(n)
```

