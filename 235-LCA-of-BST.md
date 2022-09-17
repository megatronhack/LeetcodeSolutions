# 235. Lowest Common Ancestor of a Binary Search Tree

给一个二叉搜索树，找出两个节点的最近公共祖先。

二叉搜索树找两个节点的最近公共祖先其实很好找，找到那个比其中一个小以及比另外一个大的节点就行，该节点就是两个节点的最近公共祖先。

Time complexity: O(logN)

Space complexity: O(H), where H is the height.

```java
public class Solution {
  public TreeNode lca(TreeNode root, int p, int q) {
    // Write your solution here
   int small = Math.min(p,q);
   int large = Math.max(p,q);
   while(root != null){
   if (root.key < small){
      root = root.right;
   }
   else if (root.key > large){
     root = root.left;
   }
   else{
    return root;
   }
   
   }  
   return null;   
 }
}
```