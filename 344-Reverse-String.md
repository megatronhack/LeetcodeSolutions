# 344. Reverse String

给定一个字符数组形式的字符串，把字符串reverse一下。

第一个和最后一个换，第二个和倒数二个etc

Time ON

Space On

```java
public class Solution {
  public String reverse(String input) {
    // Write your solution here
    if (input == null || input.length() <= 1){
      return input;
    }
    //rec
    char[] array = input.toCharArray();
    reverHelper(array,0,array.length -1);
    return new String(array);
  }
  private void reverHelper(char[] array, int left,int right){
    if (left >= right){
      return;
    }
    swap(array,left,right);
    reverHelper(array,left + 1, right -1);
  }
  
  private void swap(char[] array, int left, int right){
    char temp = array[left];
    array[left] = array[right];
    array[right] = temp;
  }
  //time on
  //space on
}

```