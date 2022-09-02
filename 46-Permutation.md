# 46. Permutations

给定一个无重复元素的数组，得到它的全排列。这题也是经典的DFS题目，我们针对每个位置进行枚举，既然是全排列，那么按照我们以前高中学全排列的思路，第一个位置可以放n个元素，后面可以放剩下的n-1个，直到最后。

体现在代码里就是，当前位置可以和包括自己在内的后面所有元素进行交换，然后继续枚举下一个位置。当枚举到数组结尾时，我们就把目前的排列给加入答案。那么其实就是，0号位置可以放n个元素，1号位置可以放n-1个元素，直到最后的位置。和全排列的语义是一样的，所以最后我们可以枚举所有的全排列并加入答案。

Time complexity: O(N! * N), `N!`是全排列的答案个数，N是元素个数。因为添加答案的时候，需要逐个添加，所以会耗费额外的N复杂度。

Space complexity: O(N), N层调用栈。

```java
public class Solution {
  public List<String> permutations(String input) {
    List<String> result = new ArrayList<String>();
    if (input == null){
      return result;
    }
    char[] array = input.toCharArray();
    helper(array, 0, result);
    return result;
  }
  //choose the character to be at the positio of 'index'
  //all the already chosen positions are (0, idnex - 1)
  //all the candicate characters can be at position "index"
  //are in the subarray of (index, array.length - 1)
  private void helper(char[] array, int index, List<String> result){
    //terminate condition:
    //only when we have already chosen the characters for all the position
    //we can have a complete permutation
    if (index == array.length){
      result.add(new String(array));
      return;
    }
    //all the possible characters coule be placed at index are
    //the characters in the subarray(index, array.length - 1);
    for (int i = index; i < array.length; i++){
      swap(array,index, i);
      helper(array, index + 1, result);
      //remember to swap back when back track to previous level
      swap(array, index, i);
    }
  }

  private void swap(char[] array, int left, int right){
    char tmp = array[left];
    array[left] = array[right];
    array[right] = tmp;
  }
}

//Time: O(n!)
//Space:O(n)

```