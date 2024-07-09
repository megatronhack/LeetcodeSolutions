# 114. Flatten Binary Tree to Linked List

给定一个二叉树，以先序遍历的顺序把它in-place铺平为链表。

那这题就是把原来的二叉树完全变成只有右孩子的一个二叉树，让它看起来像是链表一样。

At each layer, change the root.right and set the root.left = null in Preorder

Time complexity: O(N).

Space complexity: O(H).

```java
public class Solution {
  public TreeNode flatten(TreeNode root) {
    // Use the recursion function to solve this
    // At each layer, change the root.right and set the root.left = null in preorder
    // Use an array to keep record of the previous root node
    TreeNode[] prev = new TreeNode[1];
    helper(root, prev);
    return root;
  }

  private void helper(TreeNode root, TreeNode[] prev) {
    if (root == null) {
      return;
    }
    TreeNode leftNode = root.left;
    TreeNode rightNode = root.right;
    if (prev[0] != null) {
      prev[0].right = root;
    }
    root.left = null;
    prev[0] = root;
    helper(leftNode, prev);
    helper(rightNode, prev);
  }
}
```