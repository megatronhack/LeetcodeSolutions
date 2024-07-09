# 105. Construct Binary Tree from Preorder and Inorder Traversal

给定一个二叉树的先序后中序遍历数组，重建这个二叉树。

这题我们可以用递归的方式来解决。

先序遍历的特征就是根节点肯定在最开始，而中序遍历的特征则是根节点被左右子树夹着。那么我们用`pStart`来标记子树的根节点在先序遍历中的位置，`iLeft`和`iRight`分别标记子树再中序遍历下的范围。

很显然，`preorder[pStart]`就是子树的根节点值。我们根据这个值到`inorder[iLeft...iRight]`里面去找到根节点的位置`iRoot`。为了快速查找，我们可以实现建立一个中序遍历下每个节点值对应在哪个下标的Map。

`inorder[iLeft, iRoot - 1]`就是左子树的中序遍历结果，`inorder[iRoot + 1, iRight]`就是右子树的中序遍历结果。同时，我们也就知道左子树到底有多少个节点了。那么在先序遍历里，左子树的根是`preorder[pStart + 1]`，而右子树根的位置则可以通过之前得到的左子树尺寸来推测出来，递归的向下去建立子树。

base case分两种情况，一个是中序缩减到空，那么返回null。另一个则是中序缩减到只有一个元素，那么直接建好节点并返回。

Time complexity: O(N).

Space complexity: O(N). HashMap.

```java
public class Solution {
  public TreeNode reconstruct(int[] inOrder, int[] preOrder) {
    Map<Integer, Integer> inIndex = indexMap(inOrder);
    return helper(preOrder, inIndex, 0, inOrder.length - 1, 0, preOrder.length - 1);
  }
  private Map<Integer, Integer> indexMap(int[] inOrder) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < inOrder.length; i++) {
      map.put(inOrder[i], i);
    }
    return map;
  }
  private TreeNode helper(int[] preOrder, Map<Integer, Integer> inIndex, int inLeft, int inRight, int preLeft,
   int preRight) {
     if (inLeft > inRight) {
       return null;
     }
      TreeNode root = new TreeNode(preOrder[preLeft]);
    // get the position of the root in inOrder sequence, so that we will know
    // the size of left/right subtrees.
     int inMid = inIndex.get(root.key);
     root.left = helper(preOrder, inIndex, inLeft, inMid - 1, preLeft + 1, preLeft + inMid - inLeft);
     root.right = helper(preOrder, inIndex, inMid + 1, inRight, preLeft + inMid - inLeft + 1, preRight);
     return root;
   }
}
//preLeft + 1, preLeft + inMid - inLeft  // inMid - inLeft 是左子树的size
//inRight, preRight + inMid - inRight + 1, preRight 不能直接写 inmid + 1，会stack overflow
//time on
//oh
```