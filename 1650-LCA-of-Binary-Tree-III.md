# 1650. Lowest Common Ancestor of a Binary Tree III

这题也是找LCA，但是二叉树每个节点都知道自己的父节点。所以我们可以先找到one和twol各自的深度，然后从较深的那个开始出发到和较浅的那个齐平。齐平之后，两个点同时出发向上走直至相遇，就是他们最近的公共祖先。

**Examples**

​    5

​    /  \

   9   12

  /  \    \

 2   3    14

The lowest common ancestor of 2 and 14 is 5

The lowest common ancestor of 2 and 9 is 9

The lowest common ancestor of 2 and 8 is null (8 is not in the tree)

Time complexity: O(H). H is height.

Space complexity: O(1).

```java
/**
 * public class TreeNodeP {
 *   public int key;
 *   public TreeNodeP left;
 *   public TreeNodeP right;
 *   public TreeNodeP parent;
 *   public TreeNodeP(int key, TreeNodeP parent) {
 *     this.key = key;
 *     this.parent = parent;
 *   }
 * }
 */
public class Solution {
  public TreeNodeP lowestCommonAncestor(TreeNodeP one, TreeNodeP two) {
    // The two nodes are not guaranteed in the binary tree
    // Need to get the height of the node then move the two nodes at the same height and find the LCA
    // Need to think  which node is lower then move that node to the same level as another
    int oneHeight = getHeight(one);
    int twoHeight = getHeight(two);
    if (oneHeight > twoHeight) {
      return lowestCommonAncestor(one, two, oneHeight - twoHeight);
    } else {
      return lowestCommonAncestor(two, one, twoHeight - oneHeight);
    }
  }

  private int getHeight(TreeNodeP one) {
    int height = 0;
    while(one.parent != null) {
      height += 1;
      one = one.parent;
    }
    return height;
  }

  private TreeNodeP lowestCommonAncestor(TreeNodeP one, TreeNodeP two, int diff) {
    //one's height is bigger than two then need to remove one to the same layer as two
    while (diff > 0) {
      one = one.parent;
      diff--;
    }

    while (one != two) {
      one = one.parent;
      two = two.parent;
    }
    return one;
  }
}
// TC : O(height)
// SC: O(1) 
```