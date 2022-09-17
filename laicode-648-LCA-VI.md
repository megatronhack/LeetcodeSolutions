# Laicode 648. Lowest Common Ancestor VI

给定一个K叉树，和M个节点，找到他们的最近公共祖先。

用一个set来记录。

和找最近公共祖先的其他题目也差不多的思路。只不过是挨个遍历子节点，记录搜寻结果。

如果搜寻结果found != null，说明当前节点是两个节点的最近公共祖先。否则，搜到什么返回什么。

这样最后我们就可以找到他们的最近公共祖先。

Time complexity: O(N)

Space complexity: O(max(H, M)). H is height.

```java
public class Solution {
  public KnaryTreeNode lowestCommonAncestor(KnaryTreeNode root, List<KnaryTreeNode> nodes) {
    // Write your solution here
    Set<KnaryTreeNode> set = new HashSet<KnaryTreeNode>(nodes);
    return helper(root,set);
  }
  private KnaryTreeNode helper(KnaryTreeNode root, Set<KnaryTreeNode> set){
    if (root == null || set.contains(root)) {
      return root;
    }
    KnaryTreeNode found = null;
    for (KnaryTreeNode child : root.children) {
      KnaryTreeNode node = helper(child, set);
      if (node == null) {
        continue;
      }
      if (found == null) {
        found = node;
      } else {
        return root;
      }
    }
   return found; 
  }
}
//time On 
//space on
```

**Examples**

​    5

   /  \

   9  12

  / | \   \

 1 2 3   14



The lowest common ancestor of 2, 3, 14 is 5.

The lowest common ancestor of 2, 3, 9 is 9.