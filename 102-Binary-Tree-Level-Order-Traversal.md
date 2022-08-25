# 102. Binary Tree Level Order Traversal

对二叉树进行层序遍历，一层一层的输出。

## BFS Approach

这题最直观的就是宽度优先遍历，宽搜的精髓在于维护一个队列，每次从队头取元素，处理元素时把新元素放到队尾。这样就能保证对二叉树或者图进行遍历的时候，是齐头并进，而不是一路先钻到底。

Time complexity: O(N)

Space complexity: O(N), because we have maintain a queue which can hold up to n/2 nodes.

```java
public class Solution {
  public List<List<Integer>> layerByLayer(TreeNode root) {
    // Write your solution here
    List<List<Integer>> list = new ArrayList<List<Integer>>();
    if (root == null){
      return list;
    }

    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.offer(root);
    while (!queue.isEmpty()){
      //the list storing all the nodes on the current level
      List<Integer> curLayer = new ArrayList<Integer>();
      //the size of the current level
      int size = queue.size();
      //traverse all the nodes on the current level and prepare for the next level
      for (int i = 0; i < size; i++){
        TreeNode cur = queue.poll();
        curLayer.add(cur.key);
        if (cur.left != null){
          queue.offer(cur.left);
        }
        if (cur.right != null){
          queue.offer(cur.right);
        }
      }
      list.add(curLayer);
    }
    return list;
  }
}

```