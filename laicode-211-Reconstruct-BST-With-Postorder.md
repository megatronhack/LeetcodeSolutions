# Laicode 211. Reconstruct Binary Search Tree With Postorder Traversal

给定一个BST的后序遍历数组，重建这个树。

后序遍历的话，那么子树的根节点永远是在最后的。所以我们可以从后往前遍历，然后优先建立右子树，再去建立左子树。全局用一个`rootIndex`来表明当前子树的root所在位置，每次建立之后就把它向前推进一个位置。但是我们如何界定左右子树他们的边界在哪儿呢？我们用一个min来标明。`min`记录了当前子树里允许的最小值，也就是说如果`rootIndex`往前推进的途中遇到了比传进来的`min`还小的节点，那么这时候这个子树就已经结束了，我们需要返回null。

递归调用建立右子树的时候，传入的`min`就是这个子树根的值加1。递归调用建立左子树是，把上层传进来的`min`原封不动的传进去。

Time complexity: O(N).

Space complexity: O(H).

```java
public class Solution {
  public TreeNode reconstruct(int[] post) {
    // Assumptions: post is not null,
    // there is no duplicate in the binary search tree.
    // Traversing position of the post order,
    // we traverse and construct the binary search tree
    // from the postOrder right to left.
    int[] index = new int[] {post.length - 1};
    return helper(post, index, Integer.MIN_VALUE);
  }
  private TreeNode helper(int[] postorder, int[] index, int min) {
    // Since it is a binary search tree,
    // the "min" is actually the root,
    // and we are using the root value to determine the boundary
    // of left/right subtree.    
    if (index[0] < 0 || postorder[index[0]] <= min) {
      return null;
    }
    TreeNode root = new TreeNode(postorder[index[0]--]);
    root.right = helper(postorder, index, root.key);
    root.left = helper(postorder, index, min);
    return root;
  }
}
```