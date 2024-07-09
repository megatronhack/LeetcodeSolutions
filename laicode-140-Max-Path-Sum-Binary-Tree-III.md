# Laicode 140. Maximum Path Sum Binary Tree III

给定一个二叉树，找出直上直下的路径的最大和。路劲的起点终点不限，只要是直上直下的路径即可。

那么这题和[laicode 639. Max Path Sum From Leaf To Root](laicode-639-Max-Path-Sum-From-Leaf-To-Root.md)很像，不过这题路径起点和终点不限。

所以我们在实现的时候就没有必要非要碰到叶子节点才去试图更新答案，

而是每下一层就去试图更新答案。

然后往下层调用的时候，先把目前为止的路径和与0比较。

如果比0小，那只会拖累路径和的计算，就直接斩断，传0作为下层调用的prefixSum。

如果比0大，那么就可以给路径和做贡献，就传给下层用。

对左右孩子进行调用，一直到最后。这样，我们就可以得到整棵树最大的直上直下路径和。

Time complexity: O(N).

Space complexity: O(H).

```java
public class Solution {
  public int maxPathSum(TreeNode root) {
    // The max sum is from root to one of the leaf nodes
    // use the recursion function to return the max sum from bottom to top
    // tc: O(n) O(height)
    int[] maxSum = new int[] {Integer.MIN_VALUE};
    maxPath(root, maxSum);
    return maxSum[0];
  }

  private int maxPath(TreeNode root, int[] maxSum) {
    //base case
    if (root == null) {
      return 0;
    }
    //subproblem 
    int left = maxPath(root.left, maxSum);
    int right = maxPath(root.right, maxSum);
    //we can decide whether not to add the sum from leaf nodes if it is negative
    left = left < 0 ? 0 : left;
    right = right < 0 ? 0 : right;
    int curSum = Math.max(left, right) + root.key;
    //may need to update the global sum max
    maxSum[0] = Math.max(maxSum[0], curSum);
    //what to return to the parent node
    return Math.max(left, right) + root.key;
  }
}

```

**Examples**

  -5

 /   \

2    11

   /   \

  6   14

​      /

​    -3

The maximum path sum is 11 + 14 = 25