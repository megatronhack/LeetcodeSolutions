# 156. Binary Tree Upside Down

按照题目给的指示对二叉树进行转向。

根据题意，我们可以看出来，转向过后左孩子变成了根节点，右孩子变成了左节点，而根节点变成了右孩子。根据这一变化，我们可以递归的去改变这个这个二叉树。

为了进行此番变动，我们需要一个辅助方法，而且需要子树的根节点和其父节点作为参数。我们需要不断地向左延伸，直到最左下的那个节点为止，它就是改变过后整个树的新根节点。找到该节点之后，以后每层都得返回这个节点，直至最开始的调用，使得它真正成为整棵树的新节点。

返回新的根节点的途中顺带对树进行操作，把当前root的父节点变成root的左孩子，父节点如果有右孩子的话就变成root的右孩子。但是注意，返回的永远是同样的newRoot，即原来整棵树最左下的那个节点。

**Examples**

​    1

   /   \

  2    5

 /  \

3    4

is reversed to

​    3

   /   \

  2    4

 /  \

1    5

Time complexity: O(N) because we still have to traverse all nodes.

Space complexity: O(H) where H is the height.

## recursion

```java
public class Solution {
  public TreeNode reverse(TreeNode root) {
    // Write your solution here
    if (root == null || root.left == null){
      return root;
    }
    TreeNode newRoot = reverse(root.left);
    root.left.right = root.right;
    root.left.left = root;
    root.left = null;
    root.right = null;
    return newRoot;
  }
}

```

## Iterative

```java
public class Solution {
  public TreeNode reverse(TreeNode root) {
    // Write your solution here
    TreeNode prev = null;
    TreeNode preRight = null;
    while (root != null){
      TreeNode next = root.left;
      TreeNode right = root.right;
      root.left = prev;
      root.right = preRight;
      preRight = right;
      prev = root;;
      root = next;


    }
    //return
    return prev;
  }
  // time ON
  //space O1
}
```

