# Laicode 643. All Permutations of Subsets

给定一个字符串，打印出所有的排列的子集且不能重复。比如`abc`的子集有个`bc`，`bca`的子集也有一个`bc`，但是答案里只能有一个`bc`。

其实和all permutation差不多，我们依然按照求全排列的方法去做，只是我们沿途记录下每一层递归时候已经排列好的部分就可以。因为已经排列好的部分肯定是后续所有衍生的全排列所共有的子集，所以记录下这个就可以保证子集不会重复。

Just modify the base case to print all internal nodes of the tree.

![Laicode 643. All Permutations of Subsets1663792224669](assets\images\Laicode 643. All Permutations of Subsets1663792224669.jpg)

Time complexity: O(N * N!)

Space complexity: O(N)

```java
public class Solution {
  public List<String> allPermutationsOfSubsets(String set) {
    // The given string with no duplicate and need to return a list with all subsets
    // Use DFS to solve this question
    // tc: O(n!) sc:O(n)
    List<String> result = new ArrayList<>();
    if (set == null) {
      return result;
    }
    char[] array = set.toCharArray();
    helper(array, 0, result);
    return result;
  }
  private void helper(char[] array, int index, List<String> result) {
    //base case: add the result at each level
    result.add(new String(array, 0, index));
    //dfs rule
    for (int i = index; i < array.length; i++) {
      swap(array, index, i);
      helper(array, index + 1, result);
      swap(array, index, i);
    }
  }

  private void swap(char[] array, int left, int right) {
    char tmp = array[left];
    array[left] = array[right];
    array[right] = tmp;
  }
}

```

**Examples**

Set = “abc”, all permutations are [“”, “a”, “ab”, “abc”, “ac”, “acb”, “b”, “ba”, “bac”, “bc”, “bca”, “c”, “cb”, “cba”, “ca”, “cab”].

Set = “”, all permutations are [“”].

Set = null, all permutations are [].