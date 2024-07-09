# 124. Binary Tree Maximum Path Sum

给定一个二叉树找到里面最大的路径和。

这题和[laicode 138. Maximum Path Sum Binary Tree I](laicode-138-Maximum-Path-Sum-Binary-Tree-I.md)相似，只不过这题路径起点和终点可以是二叉树内部任意点。那么这题就更简单了！

二叉树上的递归还是三件事情：
+ 我希望左右孩子给我什么？以他们为起点的最大路径和
+ 我当前节点需要做什么？计算经过我的最大路径和，并更新全局答案
+ 我需要向上返回什么？返回以我为起点向下的最大路径和

因为这里的路径起点和终点可以是任意点，所以代码实现上需要注意的就没那么多了。

从左右孩子那里各自拿到以他们为起点向下的最大路径和，先和0比，取大的。

然后计算经过当前节点的最大路径和，并试图更新全局最大路径和。

最后向上返回以当前节点向下的最大路径和。最后我们就可以得到全局最大的路径和。

Time complexity: O(N).

Space complexity: O(H).

```java
public class Solution {
  public int maxPathSum(TreeNode root) {
    // the path can be from any node to any node
    // use the recursion function to solve this question
    // tc: O(n) sc:O(h)
    int[] maxSum = new int[] {Integer.MIN_VALUE};
    maxPathSum(root, maxSum);
    return maxSum[0];
  }
  private int maxPathSum(TreeNode root, int[] maxSum) {
    //base case
    if (root == null) {
      return 0;
    }
    //what to expect from leaf nodes
    int leftSum = maxPathSum(root.left, maxSum);
    int rightSum = maxPathSum(root.right, maxSum);
    //from any node to any node, can decide whether to add or not
    leftSum = leftSum > 0 ? leftSum : 0;
    rightSum = rightSum > 0 ? rightSum : 0;
    int curSum = leftSum + rightSum + root.key;
    //decide whether we need to update the maxSum
    maxSum[0] = Math.max(curSum, maxSum[0]);
    //what to report to parent node
    return Math.max(leftSum, rightSum) + root.key;
  }
}
```

**Examples**

  -1

 /   \

2    11

​     /     \

   6     -14

one example of paths could be -14 -> 11 -> -1 -> 2

another example could be the node 11 itself

The maximum path sum in the above binary tree is 6 + 11 + (-1) + 2 = 18