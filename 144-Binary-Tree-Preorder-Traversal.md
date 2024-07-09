# 144. Binary Tree Preorder Traversal

## Recursive Approach

二叉树先序遍历，递归实现。

Time complexity: O(N)

Space complexity: O(H), where H is the height of the binary tree.

```java

public class Solution {
  public List<Integer> preOrder(TreeNode root) {
    // Write your solution here
        //corner
    List<Integer> result = new ArrayList<>();  
    preOrder(root,result);
    return result;
  }

  private void preOrder(TreeNode root, List<Integer> result){
    //base case
    if(root == null){
      return;
    }

    result.add(root.key); 
    preOrder(root.left,result);
    preOrder(root.right,result);
  }
  
}

```

## Iterative Approach

二叉树先序遍历，迭代实现。

由于先序遍历的顺序是根左右这一性质，即为先访问根节点，再访问左子树最后再访问右子树。所以我们需要栈来存储下一个需要访问的节点，每当访问一个节点时先把右子树的根，即右孩子给先压入栈，这样程序就会后处理它。左子树的根，即左孩子后入栈，这样我们会优先处理左孩子。等左子树全都处理完了，栈会弹出右孩子来处理右子树。

Time complexity: O(N)

Space complexity: O(H), where H is the height of binary tree.

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null){
            return res;
        }
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode curr = stack.pop();
            res.add(curr.val);
            if(curr.right != null){
                stack.push(curr.right);
            }
            if(curr.left != null){
                stack.push(curr.left);
            }
        }
        return res;
    }
}
```



## N-ary Tree Preorder Traversal

需要处理children node的排序问题 Collections.reverse(node.children);

注意offerFirst和pollFirst的顺序去处理这个问题。

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<Integer> preorder(Node root) {
        //Need to traverse the tree level by level by using a stack
        //Use the list to add the cur node's value and return
        List<Integer> res = new ArrayList<>();
        Deque<Node> stack = new LinkedList<Node>();
        if (root == null) return res;
        stack.offerFirst(root);
        while(!stack.isEmpty()){
            Node cur = stack.pollFirst();
            res.add(cur.val);
            Collections.reverse(cur.children);
            for (Node child : cur.children){
                stack.offerFirst(child);
            }
        }
        return res;
    }
}
```

