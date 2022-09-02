# 22. Generate Parentheses

给一个数字，生成所有合理的括号对。

还是用DFS的思路，搜索过程中记录下现有的左括号，右括号数量，当目前左括号的数量还比n小的时候，就可以安插左括号。当前左括号数量比右括号多的时候，就可以安插右括号。当左右括号之和等于2n的时候，一个完整的permutation就生成了，加入答案。

Time complexity: O(n*2^(2n))，因为最后会有2^2n量级的答案。注意是2^2n量级，而不是2^2n个答案，因为不是每个位置都可以放右括号。每加入一个排列，`toString`方法会有n的复杂度，相乘就是这里的复杂度。

Space complexity: O(n)，2n层调用栈，2n长度的StringBuilder来记录排列。

```java
public class Solution {
  public List<String> validParentheses(int n) {
    // Write your solution here
    //char[] ||  StringBuilder || left index ||right index
    List<String> result = new ArrayList<String>();
    StringBuilder sb = new StringBuilder();
    helper(result, 0, 0, sb, n);
    return result;
  }

  private void helper(List<String> result, int left, int right, StringBuilder sb, int n){
    //base case
    if (left == n && right == n){
      result.add(sb.toString());
      return;
    }
    //when to add'('
    if (left < n){
      sb.append('(');
      helper(result,left + 1, right, sb, n);
      sb.deleteCharAt(sb.length() - 1);
    }
    //when to add')'
    if (right < left){
      sb.append(')');
      helper(result, left, right + 1, sb, n);
      sb.deleteCharAt(sb.length() - 1);
    }
  }
}

```