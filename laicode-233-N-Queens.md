# Laicode 233. N Queens

N皇后问题，要求每一行、每一列和每一个斜对角线只能有一个皇后。

经典DFS题目了，这里我们可以用boolean valid function来快速判断皇后是否可以放在一个位置。

dfs for loop列出columns，check 每个columns对应的row是否能放。

假设该位置坐标是`(row, col)`，那么该列就只能有这一个皇后，所以`cur.get(i) == column `不能为true。该对角线也只能有一个皇后，根据观察，我们知道一个对角线上的坐标和是相同的，即`x1 + y1 == x2 + y2`。所以对应的`Math.abs(cur.get(i) - column) == row - i`也不能为true。另一个反对角线上也只能有一个皇后，根据观察我们知道同一个反对角线上坐标之差是相同的，即`x1 - y1 == x2 - y2`。之前的math.abs解决了这个问题



一行一行的尝试，对于每一列的位置，按照以上方法判断当前位置是否可以放置皇后。如果可以，就加入`rowQueens`作为答案备选，并且mark该列以及两个对角线以防止以后新的皇后与它冲突。并向下一层继续搜索，直到搜完所有的行，再把所有的N皇后位置放入最终的答案组合。

Time complexity: O(n * n!)

Space complexity: O(n), because we need extra space to mark and n level call stack.


```java
public class Solution {
  public List<List<Integer>> nqueens(int n) {
    // Get all possible solutions: DFS, think about the tree
    // Think what is a valid solution
    // What is the result to return
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    List<Integer> cur = new ArrayList<Integer>();
    helper(result, cur, n);
    return result;
  }

  private void helper(List<List<Integer>> result, List<Integer> cur, int n) {
    //base case: when for all the rows we know whre the queen is positioned
    if (cur.size() == n) {
      result.add(new ArrayList<Integer>(cur));
      return;
    }

    for (int i = 0; i < n; i++) {
    //check if putting a queen at column i at the current row is valid
      if (valid(cur, i)) {
        cur.add(i);
        helper(result, cur, n);
        cur.remove(cur.size() - 1);
      }
    }
  }

  private boolean valid(List<Integer> cur, int column) {
    int row = cur.size();  // exa: {0,3] , travered 2 rows,
    // i is row checking
    for (int i = 0; i < row; i++) {
                                 //check columns and current columne   ==       //current row and check row    // x2 -x1 == y2-y1
      if (cur.get(i) == column || Math.abs(cur.get(i) - column) == row - i) {
        return false;
      }
    }
    return true;
  }
}

//Time: O(n!*n) 
//Space: O(n)

```