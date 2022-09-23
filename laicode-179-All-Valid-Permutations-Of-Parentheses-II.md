# Laicode 179. All Valid Permutations Of Parentheses II

给定三种括号，以及各自的对数，枚举所有的组合可能。

这题和[22. Generate Parentheses](22-Generate-Parentheses.md)还是一个思路，只不过括号种类多了。所以我们需要一个数组来盛放三种括号的各自左右括号的剩余个数，三种括号对应的左右括号，以及用一个Stack来记录未被配对的左括号。

枚举三类括号的左右括号，当是左括号时，我们就去检查对应的这个左括号是否还有余额，有的话就加入当前的组合，余额减一，栈顶放入这个左括号然后进入下一层遍历。退出来的时候，记得恢复状态。当是右括号时，先检查当前的右括号是否有余额以及栈顶的左括号是否可以与其配对。如果都满足的话，就加入当前组合，余额减一，栈顶弹出，向下搜索。搜索出来之后记得恢复状态。

参考22的图：![22. Generate Parentheses](C:\Users\Guanyu\Desktop\My github\LeetcodeSolutions\assets\images\22. Generate Parentheses.jpg)

Time complexity: O(x * x!) where x = l + m + n.

Space complexity: O(x) if the result doesn't count.

```java
public class Solution {
  public static final char[] ps = new char[]{'(',')','<','>','{','}'};
  public List<String> validParentheses(int l, int m, int n) {
    // Use the dfs to solve this problem
    // There should be 2(l + m + n) levels in the tree
    // For each level need to choose which ps to add need to try 6 states 
    // For left ps, if the remain of this kind of ps is > 0 then we can add
    // For right ps, need to use a stack to check whether the first one in stack is the right pair of this ps
    // tc: 2n^2m(assume n is the type of the parentheses and m is the total numer of pairs)
    // sc: O(2m)
    List<String> result = new ArrayList<String>();
    int[] remain = new int[] {l, l, m, m, n, n};
    Deque<Character> stack = new LinkedList<>();
    StringBuilder sb = new StringBuilder();
    int targetLen = 2 * l + 2* m + 2*n;
    helper(ps, remain, targetLen, stack, sb, result);
    return result;
  }

  private void helper(char[] array, int[] remain, int targetLen, Deque<Character> stack, StringBuilder sb, List<String> result) {
    //base case
    if (sb.length() == targetLen) {
      result.add(sb.toString());
      return;
    }
    //the states we need to try at each level
    for (int i = 0; i < remain.length; i++) {
      //if we choose to add the left ps: the index should be even and the remain should > 0
      if (i % 2 == 0) {
         if (remain[i] > 0) {
            sb.append(ps[i]);
            stack.offerFirst(ps[i]);
            remain[i]--;
            helper(array, remain, targetLen, stack, sb, result);
            sb.deleteCharAt(sb.length() - 1);
            stack.pollFirst();
            remain[i]++;
         }
      } else {    
        //if we choose to add the right ps: the index should be odd, the remain should > 0 and should match as a pair
        if (remain[i] > 0 && !stack.isEmpty() && stack.peekFirst() == ps[i - 1]) {
            sb.append(ps[i]);
            stack.pollFirst();
            remain[i]--;
            helper(array, remain, targetLen, stack, sb, result);
            sb.deleteCharAt(sb.length() - 1);
            stack.offerFirst(ps[i - 1]);
            remain[i]++;
        }
      }
    }
  }
}

```

Get all valid permutations of l pairs of (), m pairs of <> and n pairs of {}.

**Examples**

l = 1, m = 1, n = 0, all the valid permutations are ["()<>", "(<>)", "<()>", "<>()"]