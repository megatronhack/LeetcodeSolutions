# Laicode 82. Remove Adjacent Repeated Characters IV

给定一个字符串，不断地删去连续重复的字符，不保留任何连续的字符。大概类似于祖玛游戏那样，`abba`先删去中间的`bb`，删完之后`aa`相邻了，就接着删`aa`。

双指针同时从0出发，fast代表当前要处理的位置，[0, slow)记录着已经处理好的没有连续重复字符的子串。
+ 如果slow > 0 且 fast和fast + 1位置的字符一样的话，说明`fast`及其相邻的重复字符需要需要消。
+ 如果slow < 0，就老老实实把fast加入已经处理好的子串，slow后移。

相当于如果我们每个字符段都是至少把它首个字符压入[0, slow)，如果这个字符段只有一个字符，那么就成功压入。如果这个字符段不止一个字符，那么下一步会跳过后面所有的并且弹出一开始压入的首个字符。

Time complexity: O(n). Why? Because we only process each character once.

Space complexity: O(n), because of the extra char array.

```java
public class Solution {
  public String deDup(String input) {
    // Write your solution here
    if (input == null || input.length() <= 1)
    return input;
    //convert the string to char[], and traverse and replace it in-place
    char[] array = input.toCharArray();
     //the first element in the array
    int slow = 0;
    for(int fast = 1; fast < array.length; fast++){
       if(slow == -1 || array[fast] != array[slow]){
          array[++slow] = array[fast];
       }
       else{
         slow--;
         while( fast + 1 < array.length && array[fast] == array[fast + 1]){
           fast++;
         }
       }
    }
    return new String(array,0,slow + 1);
  }
}

```