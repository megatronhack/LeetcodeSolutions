# Laicode 681. Seven Puzzle

给定一个2X4的棋盘，和对应的棋子摆放。只能移动0，问最少多少步可以把棋子移动成规定的样子。如果怎么也不可能变成规定的样子，就返回-1。

这题就是BFS不断地搜索所有可能的状态，比如`10234567`中的0可以向左、右和下各自走一步，下一个状态分别对应`012345678`、`12034567`和`15234067`。`01234567`是我们需要达到的状态，所以我们知道走一步就到了。

所以这题的大题思想就是，先找到0所在的位置，然后让0向所有可能的地方走。用一个Set来记录目前为止所有遇到的棋盘状态，如果挪动0之后产生的是没有遇过的新状态，就加入Set。如果这个状态以前遇到过，那就不动。这样，我们可以知道0走1步可以得到哪些状态，2步可以得到哪些状态，3步、4步……。棋盘的状态数量肯定是有限的，如果能搜到那肯定能找到所需步数，如果搜不到就返回-1就行。

这题有很多可以优化的地方：
+ 题目输入的是一个数组，但是对比数组相同需要自己实现，而且Set里面放`int[]`达不到我们要的效果。因此，我们把输入的数组序列化为字符串，方便使用。
+ 每次都要找到0所在的位置可能会带来额外时间，所以我用了一个内部类`State`来记录目前的棋盘状态和它里面0所在的位置。
+ 对于每一个位置来说，它能走的地方其实是有限的。所以我们直接hardcode所有位置能走的所有地方，直接调用就好。

```java
public class Solution {
  static class Board {
    public final static int R = 2;
    public final static int C = 4;

    public Board() {
    }
  
  public Board(int[] values) {
    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        board[i][j] = values[i*C + j];
      }
    }
  }

  public void swap (int i1, int j1, int i2, int j2) {
    int tmp = board[i1][j1];
    board[i1][j1] = board[i2][j2];
    board[i2][j2] = tmp;
  }

  public int[] findZero() {
    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        if (board[i][j] == 0) {
          return new int[] {i, j};
        }
      }
    }
    return null;
  }

  public boolean outOfBound(int i, int j) {
    return i < 0 || i >= R || j < 0 || j >= C;
  }

  @Override
  public int hashCode() {
    int code = 0;
    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        code = code * 10 + board[i][j];
      }
    }
    return code;
  }

  @Override
  public boolean equals(Object o) {
    if (!(o instanceof Board)) {
      return false;
    }
    Board b = (Board) o;
    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        if (board[i][j] != b.board[i][j]) {
          return false;
        }
      }
    }
    return true;
  }

  @Override
  public Board clone() {
    Board c = new Board();
    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        c.board[i][j] = board[i][j];
      }
    }
    return c;
  }
  private int[][] board = new int[R][C];
}

final static int[][] DIRS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

  public int numOfSteps(int[] values) {
    Queue<Board> queue = new ArrayDeque<>();
    Map<Board, Integer> boardStep = new HashMap<>();

    Board start = new Board(new int[] {0, 1, 2, 3, 4, 5, 6, 7});
    queue.offer(start);
    boardStep.put(start, 0);

    while (!queue.isEmpty()) {
      Board board = queue.poll();
      int step = boardStep.get(board);

      int[] zeroPos = board.findZero();
      int zeroI = zeroPos[0];
      int zeroJ = zeroPos[1];

      for (int[] dir : DIRS) {
        int i = zeroI + dir[0];
        int j = zeroJ + dir[1];
        if (!board.outOfBound(i, j)) {
          board.swap(zeroI, zeroJ, i, j);
          if (!boardStep.containsKey(board)) {
            Board newBoard = board.clone();
            queue.offer(newBoard);
            boardStep.put(newBoard, step + 1);
          }
          board.swap(zeroI, zeroJ, i, j);
        }
      }
    }
    return boardStep.getOrDefault(new Board(values), -1);
  }
}
// assuming the board is always 2 by 4
//Time: O(|number of unique boards|)
//Space: O(|number of unique boards| * 8)

```