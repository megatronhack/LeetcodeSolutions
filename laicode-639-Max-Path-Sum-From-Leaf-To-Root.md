# Laicode 639. Max Path Sum From Leaf To Root

这题计算从root到叶子节点的最大路径和。

这次我们不再采用从底向上的返回形式了，而是采用自上而下的遍历形式。

途中我们要记录目前为止从root到上一层节点的路径和，并且传入当前层作为参数以供调用。

当前节点是叶子节点时候，就尝试更新答案。如果不是叶子节点，那就对左右子树进行相同的调用直到碰到叶子节点为止。

Time complexity: O(N).

Space complexity: O(H).

```java
public class Solution {
  public int maxPathSumLeafToRoot(TreeNode root) {
    // how to use the recursive function to solve this?
    //base case
     if (root.left == null && root.right == null) {
       return root.key;
     }
     if (root.left == null) {
       return maxPathSumLeafToRoot(root.right) + root.key;
     }
     if (root.right == null) {
       return maxPathSumLeafToRoot(root.left) + root.key;
     }
     int leftSum = maxPathSumLeafToRoot(root.left);
     int rightSum = maxPathSumLeafToRoot(root.right);
    return root.key + Math.max(leftSum, rightSum);
  }
}
//Time: O(n)
//Space: O (height)
```

**Examples**



​     10

​    /   \

  -2    7

 /   \

8   -4

The maximum path sum is 10 + 7 = 17.