# 272. Closest Binary Search Tree Value II

给定一个BST，找到离`target`最近的`k`个值，返回List。

我们思考一下，BST有什么性质？中序遍历是升序。这样我们就可以中序遍历整个BST，在遍历途中记录用一个Queue来记录我们遇到的元素，

那么这个Queue队顶到队尾是升序的。

如果当前Queue的元素个数不到`k`，那么就持续把当前节点值加入Queue。如果已经有k个了，那么我们就把当前元素和队列顶部的元素比较看谁离target比较近。

如果当前元素比较近，那就把队列顶部弹出，当前元素入队尾。如果队列顶部比较近，那么也就没有继续中序遍历的必要了，因为后面元素只会越来越远。

这里我们在调用的时候可以用一个`LinkedList`来传给Queue，返回的时候也返回它，因为它同时实现了Queue和List这两个接口。

Time complexity: O(N)

Space complexity: O(max(k, H)). H is height.

```java
/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */
public class Solution {
  public int[] closestKValues(TreeNode root, double target, int k) {
    //use a in order to traverse the tree
    // use an array with size k to store the closest k values
    // use a sliding window to compare the diff 
    if (root == null || k <= 0) {
        return new int[0];
    }
    Queue<TreeNode> queue = new ArrayDeque<TreeNode>();
    inOrder(root, target, k, queue);
    int[] array = queueToArray(queue);
    return array;
  }
  private void inOrder(TreeNode root, double target, int k, Queue<TreeNode> queue) {
    //use the bfs method to traverse
    //use a queue to keep records of the closest n TreeNode
    //base case
    if (root == null) {
      return;
    }
    inOrder(root.left, target, k, queue);
    if (queue.size() < k) {
      queue.offer(root);
    } else if (Math.abs(root.key - target) < Math.abs(target - queue.peek().key)) {
      queue.poll();
      queue.offer(root);
    }
    inOrder(root.right, target, k, queue);
  }

  private int[] queueToArray(Queue<TreeNode> queue) {
    int[] array  = new int[queue.size()];
    int i = 0;
    while (!queue.isEmpty()) {
      array[i] = queue.poll().key;
      i++;
    }
    return array;
  }
}
//TC: O(n)
//SC: O(height)

```

**Examples:**

   5

 /   \

2    11

   /   \

  6   14

closest number to 4 is 5

closest number to 10 is 11

closest number to 6 is 6