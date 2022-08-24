# 145. Binary Tree Postorder Traversal

## Recursive Approach

二叉树后序遍历，递归实现版本。后序遍历，处理顺序就是先左子树，再右子树，最后再处理根节点。

Time complexity: O(N)

Space complexity: O(H), where H is the height.

```java
public class Solution {
  public List<Integer> postOrder(TreeNode root) {
    // Write your solution here
    List<Integer> result = new ArrayList<Integer>();
    postOrder(root,result);
    return result;
  }
  public void postOrder(TreeNode root, List<Integer> result){
    if(root == null){
      return;
    }
    postOrder(root.left,result);
    postOrder(root.right,result);
    result.add(root.key);
  }
}
```

## Iterative Approach

递归方法会产生与树高同量级的调用栈，迭代法可以避免这额外的空间复杂度。迭代也有两种方法，一种比较常见的是反后序遍历，即`根右左`这样遍历一下，最后得到的答案reverse一下。

```java
public List<Integer> postOrder(TreeNode root) {
// Write your solution here
if (root == null){
  return new ArrayList<>();
}
List<Integer> result = new ArrayList<>();
Deque<TreeNode> stack = new ArrayDeque<>();
stack.push(root);
while(!stack.isEmpty()){
  root = stack.pop();
  result.add(root.key);
  if(root.left != null){
    stack.push(root.left);
  }
  if(root.right != null){
    stack.push(root.right);
  }
}

Collections.reverse(result);
return result;
}
```