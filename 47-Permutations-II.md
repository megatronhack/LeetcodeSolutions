# 47. Permutations II

和[46 Permutations](46-Permutation.md)差不多，但是这次给的数组里面会有重复元素，要求给出的全排列是无重复的。

有重复元素的话，依然是dfs深搜。当前位置和后面每个位置交换，得到一种唯一的排列。但是这次要注意的是，我们用一个`Set`来记录当前位置已经放过哪些数字了。如果已经放过一个数字，再次遇见同样的数字时就跳过，这样就可以避免重复的全排列。

![46. Permutations](assets\images\46. Permutations.jpg)

Time complexity: O(n! * n)，最多有`n!`个全排列，每记录一个排列需要`n`的复杂度。

Space complexity: (n^2)，n层递归树，虽然每一层的Set元素个数会逐渐变小，但基本遵循等差数列求和。故O(n^2)。

```java
public class Solution {
  public List<String> permutations(String input) {
    // Write your solution here
    
    //input: String
    //outputL list of all permutations
    List<String> result = new ArrayList<String> ();
    if (input == null){
      return result;
    }
    //turn the input into a char array and use DFS to traverse all the combinations 
    char[] array = input.toCharArray();
    //use the dfs function to call and then return the result
    dfs(array,0,result);
    return result;
  }

  private void dfs(char[] array, int index, List<String> result){
    //base case
    if (index == array.length){
      result.add(new String(array));
      return;
    }
    //use a hashset to keep records of the elements that has been used
    Set<Character> used = new HashSet<Character>();
    for (int i = index; i < array.length; i++){
      if(used.add(array[i])){
        //the hashset will return false if this element has been used
        swap(array,i,index);
        dfs(array, index + 1, result);
        swap(array, i, index);
      }
    }
  }

  private void swap(char[] array, int left, int right){
    char tmp = array[left];
    array[left] = array[right];
    array[right] = tmp;
  }
}

```