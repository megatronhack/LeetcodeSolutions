# 958. Check Completeness of a Binary Tree

验证给定的二叉树是否是完全二叉树。完全二叉树的定义是，除了最后一层其它层全是满的，且最后一层所有的节点都是靠左的。

那么我们用BFS的思想，一层一层搜。处理当前节点的时候，如果它有孩子为null，那么同一层之后所有的节点都不能有孩子。不仅仅是同一层，队列剩余的节点以及以后新加的节点都不可以有孩子，不然就不是完全二叉树了。

Time complexity: O(N)

Space complexity: O(N)

```java
public class Solution {
  public boolean isCompleted(TreeNode root) {
    // Write your solution 
    if (root == null) {
      return true;
  }
  Queue<TreeNode> queue = new LinkedList<TreeNode>();
  //if the flag us set true, there should not be any child nodes afterwards
  boolean flag = false;
  queue.offer(root);
  while (!queue.isEmpty()){
    TreeNode cur = queue.poll();
    //if any of the child is not present, set the flag to true
    if (cur.left == null){
      flag = true;
    } else if (flag){
      //if flag is set but we still see cur has a left child, the binary tree is not a completed one
      return false;
    } else {
      //if flag is not set and the left child is present
      queue.offer(cur.left);
    }
    //same logic applied to the right child
    if (cur.right == null){
      flag = true;
    } else if (flag){
      return false;
    } else {
      queue.offer(cur.right);
    }
  }
  return true;
}
}

//Time : O(n)
//Space: O(n)
```