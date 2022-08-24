# Laicode 55. Get Keys In Binary Search Tree In Given Range

给定一个BST，返回给定范围内所有的节点，按照升序排列。

对BST进行Inorder遍历，就可以升序访问，途中遇到满足条件的就放进列表。这里有个优化的地方，就是当前节点值如果小于等于min的话，就没必要继续遍历左孩子了，因为左子树里面所有的值肯定都小于这个值，也就小于min。同理，如果当前节点值大于等于max的话，也就没必要访问右子树。



Time complexity: O(N)

Space complexity: O(H), H is height.

```java
public class Solution {
  public List<Integer> getRange(TreeNode root, int min, int max) {
    // Write your solution here
    List<Integer> result = new ArrayList<>();
    getRange(root,min,max,result);
    return result;
  }
  public void getRange(TreeNode root, int min, int max, List<Integer> result){
    //base case
    if(root == null){
      return;
    }
    if(root.key > min ){
      getRange(root.left,min,max,result);
    }
    
    if(root.key >= min && root.key <= max){
      result.add(root.key);
    }
    
    if(root.key < max ){
      getRange(root.right,min,max,result);
    }
  }
}

```