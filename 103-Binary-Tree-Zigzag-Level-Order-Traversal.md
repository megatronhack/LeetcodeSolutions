# 103. Binary Tree Zigzag Level Order Traversal

这个二叉树Zigzag的遍历，需要用到dequeue双队列，以及一个layer记录奇偶层。

我们用`layer = 0 或1`， 奇数层或偶数层时候来表示当前层是poll元素的方向出，然后用一个双端队列来存放每一层的元素。存放顺序都是从左到右，只不过分情况讨论，
+ 如果`layer = 0`的话。表示向左输出,那么我们就不断地从队尾pollLast拿取元素放入当前层的list里，**左右**非空孩子依次放入队前offerFirst。
+ 如果`layer = 1`的话，表示向右输出。那么我们就不断地从队头pollFirst拿取元素放入当前层的list里，**右左**非空孩子依次放入队尾offerLast。

每层结束之后，把当前层的list放入答案，并且改变方向。最后就可以得到zigzag level order。

**Examples**

​    5

   /   \

  3     8

 /  \     \

 1   4     11

the result is [5, 3, 8, 11, 4, 1]

Time complexity: O(N)

Space complexity: O(N), because the deque size could be up to N/2.

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
  public List<Integer> zigZag(TreeNode root) {
    if (root == null) {
      return new LinkedList<Integer>();
    }
    //Need to travers the tree layer by layer by using a queue and return the result as a list
    List<Integer> result = new ArrayList<Integer>();
    int layer = 0;  //Odd layer from left to right even layer from right to left
    Deque<TreeNode> dequeue = new LinkedList<TreeNode>();//because we need to polllast or pollfirst
    dequeue.offer(root);
    while (!dequeue.isEmpty()) {
      int size = dequeue.size();//get the current layer's size first
      for (int i = 0; i < size; i++){
        if (layer == 0) {//check the layer number and decide which direction to poll. if even layer
          TreeNode cur = dequeue.pollLast();
          result.add(cur.key);
          if (cur.right != null) {  
            dequeue.offerFirst(cur.right);
          }
          if (cur.left != null) {
            dequeue.offerFirst(cur.left);
          }
        } else {//odd layer like 1 from left to right
          TreeNode cur = dequeue.pollFirst();
          result.add(cur.key);
          if (cur.left != null) {
            dequeue.offerLast(cur.left);
          }
          if (cur.right != null) {
            dequeue.offerLast(cur.right);
          }
        }
    }
    layer = 1 - layer;
  }
  return result;
}
}

//TC: O(n)
//SC: O(n)

// deque   3  8  5  result 5 3 8
// deque  1 4 11              
```