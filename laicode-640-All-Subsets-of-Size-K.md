# Laicode 640. All Subsets of Size K

这题和普通的求子集略有区别，这题子集最多有k个元素。

那么其实也不难，base caes稍有变化而已。这里base case就是当前子集元素个数达到k的时候直接停止向后遍历并加入答案。另一个base case就是遍历到最后了，但是只返回并不加入答案，因为如果满足的话之前就会加入答案并返回。

Time complexity: O(2^n)

Space complexity: O(n) if the result doesn't count.

![Laicode 640. All Subsets of Size K](assets\images\Laicode 640. All Subsets of Size K.jpg))

```java
public class Solution {
  public List<String> subSetsOfSizeK(String set, int k) {
    List<String> result = new ArrayList<>();
    if (set == null) {
      return result;
    }
    char[] array = set.toCharArray();
    StringBuilder sb = new StringBuilder();
    helper(array, 0, sb, result, k);
    return result;
  }
  private void helper(char[] array, int index, StringBuilder sb, List<String> result, int k) {
    //base case
    if (sb.length() == k) {
      result.add(sb.toString());
      return;
    }
    if (index == array.length) {
      return;
    }
    //if we choose to add current char
    helper(array, index + 1, sb.append(array[index]), result, k);
    //delete the char when the recursion function finished
    sb.deleteCharAt(sb.length() - 1);
    //if we choose not to add the current char
    helper(array, index + 1, sb, result, k);
  }
}
//tc: 0(2^n)
//sc: O(n)

```

**Examples**

Set = "abc", K = 2, all the subsets are [“ab”, “ac”, “bc”].

Set = "", K = 0, all the subsets are [""].

Set = "", K = 1, all the subsets are [].