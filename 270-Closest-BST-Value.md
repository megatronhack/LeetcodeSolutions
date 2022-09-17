# 270. Closest Binary Search Tree Value

给定一个BST和一个target值，找到离`target`最近的值。

在二叉树里找`target`，如果能找到那就返回这个值。

如果找不到，在途中记录离`target`最近的值最后返回就好。

Time complexity: O(H). H is the height.

Space complexity: O(1).

```java
public class Solution {
  public int closest(TreeNode root, int target) {
    // Write your solution here
    int result = root.key;
    while (root != null){
      if (root.key == target){
        return root.key;
      }
      else{
        if (Math.abs(root.key - target) < Math.abs(result - target)){
          result = root.key;  
        }
        if (root.key < target){
       root = root.right;
        }
        else{
       root = root.left;
        }
      }
    }
   return result;
  }
}

//time logn   worse case on
//space o1
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