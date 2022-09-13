# 78 Subsets

给定一个无重复数字的数组，输出它所有的子集。

经典深度优先搜索题，DFS。既然是所有子集，那么数组的每一个元素都有两种情况，计入或者不计入，所以总共会有2^n个答案。

dfs到一层的时候，当前层的元素无非就是进入当前子集，或者不进入当前子集。level到达数组末尾的时候，把当前的子集放入答案，然后返回。注意加入答案时要新建ArrayList，因为java传参的传值，传的是这个子集的地址值。如果不新建ArrayList，已经放入答案的子集会被后续的遍历给修改掉。

![78.Subsets](assets\images\78.Subsets.jpg)

Time complexity: O(2^n)

Space complexity: O(n), because of n level call stack. Also, the size of result is not taken into consideration.

```java
public class Solution {
  public List<String>  subSets(String set) {
    List<String> result = new ArrayList<String>();
    if (set == null){
      return result;
    }
    char[] arraySet = set.toCharArray();
    //record the current subset
    StringBuilder sb = new StringBuilder();
    dfs(arraySet, sb, 0, result);
    return result;
  }
  //at each level, determine the character at the position "index" to be picked or not
  private void dfs(char[] set, StringBuilder sb, int index, List<String> result){
    if (index == set.length){
      result.add(sb.toString());
      return;
    }
    //1. not pick the character at index
    dfs(set, sb, index + 1, result);
    //2. pick the character at index
    dfs(set, sb.append(set[index]), index + 1, result);
    //remember to remove the added character when back tracking to the previous level
    sb.deleteCharAt(sb.length() - 1);
  }
}
```