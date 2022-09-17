# Laicode 647. Lowest Common Ancestor V

给定一个K叉树，和两个节点，找到他们的最近公共祖先。

和找最近公共祖先的其他题目也差不多的思路。只不过是挨个遍历子节点，记录搜寻结果。

如果搜寻结果found != null，说明当前节点是两个节点的最近公共祖先。否则，搜到什么返回什么。

这样最后我们就可以找到他们的最近公共祖先。

Time complexity: O(N)

Space complexity: O(H). H is height.

```java
/**
 * public class KnaryTreeNode {
 *     int key;
 *     List<KnaryTreeNode> children;
 *     public KnaryTreeNode(int key) {
 *         this.key = key;
 *         this.children = new ArrayList<>();
 *     }
 * }
 */
public class Solution {
  public KnaryTreeNode lowestCommonAncestor(KnaryTreeNode root, KnaryTreeNode a, KnaryTreeNode b) {
    // Write your solution here
    if (root == null || root == a || root == b){
      return root;
    }
    KnaryTreeNode found = null;
    for (KnaryTreeNode child : root.children){
      KnaryTreeNode node = lowestCommonAncestor(child,a,b);
      if( node == null) {
        continue;
      }

      if(found == null){
        found = node;
      }
      else{
        return root;
      }
    }
    return found;
  }
}
//time on
//space space height
```