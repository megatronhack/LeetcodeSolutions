# Laicode 642. All Valid Permutations Of Parentheses III

这题和[laicode 179. All Valid Permutations Of Parentheses II](laicode-179-All-Valid-Permutations-Of-Parentheses-II.md)相似，但是这题括号有优先级。只能优先级高的包进优先级低的，优先级高的不能被优先级低的给包括进去，同级也不能互相包括。

针对这个限制，我们压入栈就不能像179题那样压入字符了，而是压入对应的优先级数字。这样我们在压入左括号的时候就不仅检查这个左括号是否还有余额，如果栈为空或者栈顶括号对应的优先级大于当前的优先级，那么当前的左括号才可以压入。压入右括号的时候，检查的情况不变，栈不为空而且栈顶得是对应的左括号方可将此右括号加入搜索。

Time complexity: O(2n^2m) where n is the type of ps and m is the total number of the ps

Space complexity: O(2m)

```java
public class Solution {
  private static final char[] ps = new char[] {'(', ')', '<', '>', '{', '}'};
  public List<String> validParenthesesIII(int l, int m, int n) {
    // use the dfs to solve this problem
    //case 1: when add a new left parenthesis, check the validation by using the stack, 
    //then check the priority, if not in conflict then push it to stack
    //case 2: when add a new right parentheses, check whether it match the top of the stack
    //while traverse the char array, need to record the number of that type of parenthese that can be added
    // need to use the stack to check the validation and know when to offer and when to poll

    //tc: 2n^2m where n is the type of ps and m is the total number of the ps
    //sc: O(2m)
    int[] remain = new int[] {l, l, m, m, n, n};
    StringBuilder sb = new StringBuilder();
    Deque<Integer> stack = new LinkedList<>();
    int totalLevels = 2*l + 2*m + 2*n;
    List<String> result = new ArrayList<>();
    helper(ps, remain, stack, sb, totalLevels, result);
    return result;
  }

  private void helper(char[] ps, int[] remain, Deque<Integer> stack, 
  StringBuilder sb, int totalLevels, List<String> result) {
    //base case
    if (sb.length() == totalLevels) {
      result.add(sb.toString());
      return;
    }
    //dfs rule: for each level how many states we can try
    for (int i = 0; i < ps.length; i++) {
    //if we choose to add left ps
      if (i % 2 == 0) {
        //need to check remain and priority
        if (remain[i] > 0 && (stack.isEmpty() || stack.peekFirst() > i )) {
          stack.offerFirst(i);
          remain[i]--;
          sb.append(ps[i]);
          helper(ps, remain, stack, sb, totalLevels, result);
          stack.pollFirst();
          remain[i]++;
          sb.deleteCharAt(sb.length() - 1);
        } 
      } else {
      // if we choose to add the right ps
      // need to check the remain and peekFirst in the stack whether it is in pair with current one
      if (remain[i] > 0 && !stack.isEmpty() && stack.peekFirst() == i - 1) {
        stack.pollFirst();
        remain[i]--;
        sb.append(ps[i]);
        helper(ps, remain, stack, sb, totalLevels, result);
        stack.offerFirst(i - 1);
        remain[i]++;
        sb.deleteCharAt(sb.length() - 1);
      }
      }
    }
  }
}

```

Get all valid permutations of l pairs of (), m pairs of <> and n pairs of {}, subject to the priority restriction: {} higher than <> higher than ().

**Examples**

  l = 1, m = 1, n = 0, all the valid permutations are ["()<>", "<()>", "<>()"].

  l = 2, m = 0, n = 1, all the valid permutations are [“()(){}”, “(){()}”, “(){}()”, “{()()}”, “{()}()”, “{}()()”].