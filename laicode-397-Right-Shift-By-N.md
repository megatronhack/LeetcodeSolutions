# Laicode 397. Right Shift By N Characters

给定一个字符串，循环右移N位。

Clarification:
+ n保证不小于0吗？保证
+ n保证小于字符串长度吗？不保证

假设字符串长度为`l`，如果`n == l`，其实和没有右移一样。所以我们上来先把n % l，来看实际上需要右移多少位。

比如要N == 4,    int k = n % array.length = 我们要真正要移的。 比如说K=2。

我们真的需要右移嘛？不，我们观察一下`abcdefg`右移两位变成`fgabcde`。那么其实我们可以先把整体反转成为`gfedcba`，然后`[0, 1]`和`[2, end)`各自反转一下，就好了。所以其实这里就是整体先反转，然后`[0, n - 1]和[n, end)各自反转，就可以达到右移n位的目的。

Time On

Space On

```java
public class Solution {
  public String rightShift(String input, int n) {
    // Reverse the whole first, then reverse the first part and the second part

    //corner case
    if (input == null || input.length() <= 1 || n ==0){
      return input;
    }

    char[] array = input.toCharArray();
    int k = n % array.length;
    reverse(array, 0, array.length - 1);
    reverse(array, 0 , k -1);
    reverse(array, k, array.length - 1);
    return new String(array);
  }


   private void reverse(char[] array, int left, int right){
    while (left < right){
      char tmp = array[left];
      array[left] = array[right];
      array[right] = tmp;
      left++;
      right--;
    }
  }
}
//Time: O (n) where n is the length of the string
//Space:: O(n)

```