# Laicode 141. Binary Tree Path Sum To Target III

给定一个二叉树，是否存在直上直下的路径和的值与target相等。

我们依然是自顶向下遍历。遍历途中，我们时刻检查是否存在一条以当前节点为终点的路径和为target。

所以我们不仅需要记录当前节点的前缀和，还需要记录当前路径之前各节点对应的前缀和。

这样我们就可以用当前层的前缀和减去target的方法，配合Set来快速检索。

如果不存在的话，那么就继续对左右孩子进行遍历，并且把当前节点的前缀和给放入Set。

如果左右孩子任意传回true，说明他们那里有对应的路径，当前节点也就返回true。如果都没有，就返回false。

需要注意的是，因为Set里可能已经存在当前的前缀和了，比如当前节点为0，所以我们需要记录`add`的返回值。true的话表示Set里没有这个值，添加成功，回头返回的时候也需要移除掉。false的话表示Set里已经有这个值了，添加失败，回头就没必要删掉，上一层会删掉的。

Time complexity: O(N).

Space complexity: O(H).

```java
// Use the recursion function to solve thie question
// Use the prefix sum to keep records of the sum for the path
// Use a set to check if set.contains(curSum - target)
// eg: [5, 11, 6] target 17 prefix sum [5, 16, 22]  check if the set contains (22 - target)
public class Solution {
  public boolean exist(TreeNode root, int target) {
    if (root == null){
      return false;
    }
    Set<Integer> set = new HashSet<>();
    set.add(0);//Need to add 0 in the set, if root.key = target, the set should contains at least 0 to return true
    return helper(root, target, 0, set);
  }

  private boolean helper(TreeNode root, int target, int prevSum, Set<Integer> set) {
    prevSum += root.key;
    if (set.contains(prevSum - target)) {
      return true;
    }
    boolean needRemove = set.add(prevSum);
    if (root.left != null && helper(root.left, target, prevSum, set)) {
      return true;
    }
    if (root.right != null && helper(root.right, target, prevSum, set)) {
      return true;
    }
    if (needRemove) {
      set.remove(prevSum);
    }
    return false;
  }
}
```

**Examples**

  5

 /   \

2    11

   /   \

  6   14

 /

 3

If target = 17, There exists a path 11 + 6, the sum of the path is target.

If target = 20, There exists a path 11 + 6 + 3, the sum of the path is target.

If target = 10, There does not exist any paths sum of which is target.

If target = 11, There exists a path only containing the node 11.