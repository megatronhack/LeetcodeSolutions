# 1676. Lowest Common Ancestor of a Binary Tree IV

给定一个二叉树和一个数组的节点，找到他们的最近公共祖先。

其实思路还是一样的，以前是找两个，现在是找多个而已。

用一个Set来存放所有的节点，然后只要当前节点在Set里就直接返回。

如果左右子树都有找到Set里的节点，那么返回当前节点。

否则返回左右子树查询结果里非空的那个，如果都空就返回空。

Time complexity: O(N).

Space complexity: O(H). H is the height.

```java
public class Solution {
  public TreeNode lowestCommonAncestor(TreeNode root, List<TreeNode> nodes) {
    // Need a set to check whether the curren root contains the nodes
    Set<TreeNode> set = new HashSet<TreeNode>(nodes);//why we can initiate like this?
    return helper(root, set);
  }
  private TreeNode helper(TreeNode root, Set<TreeNode> set) {
    //use the recursion function to find the lca
    //base case
    if (root == null) {
      return root;
    }
    if (set.contains(root)) {
      return root;
    }
    TreeNode l = helper(root.left, set);
    TreeNode r = helper(root.right, set);
    if (l != null && r != null) {
      return root;
    }
    return l == null ? r : l;
  }
}
```

**Examples**

​    5

​    /  \

   9   12

  /  \    \

 2   3    14

The lowest common ancestor of 2, 3, 14 is 5

The lowest common ancestor of 2, 3, 9 is 9