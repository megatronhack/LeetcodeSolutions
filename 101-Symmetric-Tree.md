# 101. Symmetric Tree

判断一个二叉树是否对称。

这里我们需要一个辅助方法，`isSymmetric(TreeNode p1, TreeNode p2)`来判断以`p1`和`p2`为根节点的二叉树是否镜像对称。判断的时候分下面三种情况，
+ `one`和`two`都是`null`的话，当然对称。
+ `one`和`two`有且只有一个是`null`的话，那当然不对称了。
+ 当`one`和`two`都不为`null`的时候，就比较他们的值是否一样。
  + 一样的话，就继续向下看看他们的子树是否互相镜像对称。镜像对称的话，其实就是p1的左孩子和p2的右孩子，以及p1的右孩子和p2的左孩子比较，看看是否满足镜像对称的条件。


Time complexity: O(N)

Space complexity: O(H), where H is the height.

```java
public class Solution {
  public boolean isSymmetric(TreeNode root) {
    // Write your solution hereo  
    if(root == null){
      return true;
    }
   
    return isSymmetric(root.left,root.right);
  }

  public boolean isSymmetric(TreeNode one, TreeNode two){
    //base case
    if (one == null && two == null){
        return true;
    }
    else if( one == null || two == null) {
        return false;
    }
    else if(one.key != two.key) {
        return false;
    }


    return isSymmetric(one.left,two.right) && isSymmetric(one.right,two.left);
  }
}
```

