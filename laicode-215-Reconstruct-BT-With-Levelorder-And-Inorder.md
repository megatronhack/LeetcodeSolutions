# Laicode 215. Reconstruct Binary Tree With Levelorder And Inorder

给定一个二叉树的中序遍历和层级遍历，建立这棵树。

给定层级遍历建立一个二叉树的话，那么这个数组的首个元素一定就是根节点。但是剩下来的节点，谁在左子树谁在右子树怎么区分呢？我们需要中序遍历下每个节点到其下标的映射来帮助我们完成这一任务。

首先我们得到根节点在中序遍历下的位置，然后我们再遍历剩下的元素得到他们中序遍历下的位置并和根节点的位置对比。在左边，就在左子树。在右边，就在右子树。为了方便我们调用，我们用List来盛放层级遍历。所以，左子树的层级遍历和右子树的层级遍历各自放入两个List，然后调用的时候直接使用就好。

Time complexity: O(NH).

Space complexity: O(H + N).

```java
public class Solution {
  public TreeNode reconstruct(int[] inOrder, int[] levelOrder) {
    // Write your solution here
    //Level is not null
    // no duplicates in the binary tree
    Map<Integer,Integer> inOrderMap = new HashMap<Integer,Integer>();
    for (int i = 0; i < inOrder.length; i++){
           inOrderMap.put(inOrder[i],i);
    } 
    List<Integer> lList = new ArrayList<>();
    for (int num: levelOrder){
        lList.add(num);        
    }
    return helper(lList,inOrderMap);
  }

  private TreeNode helper(List<Integer> level, Map<Integer,Integer> inOrderMap){
   //basecase
   if(level.isEmpty()){
    return null; 
   }
   //
   TreeNode root = new TreeNode(level.remove(0));
   List<Integer> left = new ArrayList<>();
   List<Integer> right = new ArrayList<>();
   for (int num : level){
       if (inOrderMap.get(num) < inOrderMap.get(root.key)){
             left.add(num);
         }
         else{
           right.add(num);
         }     
   }
   root.left = helper(left,inOrderMap);
   root.right = helper(right, inOrderMap);
   return root;
  }
}
```