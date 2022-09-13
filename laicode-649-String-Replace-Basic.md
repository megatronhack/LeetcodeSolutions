# Laicode 649. String Replace (basic)

给定一个字符串`input`，进行模式匹配和替换。

Clarification:
+ 给定的三个字符串都不为null
+ source不为空

找每个occurence的index。

然后逐一拷贝过去。遇到occurrence了就整个把target拷贝过去。

“input = "appledogappleabc", S = "apple", T = "cat", input becomes "catdogcatabc"

Time complexity: On

Space complexity: On

```java
public class Solution {
  public String replace(String input, String source, String target) {
    // Write your solution here
    StringBuilder sb = new StringBuilder();
    //check if there exists a substring same as Source in the input atarting at fromIndex
    int fromIndex = 0;
    int matchIndex = input.indexOf(source, fromIndex);
    while(matchIndex != -1){
      sb.append(input, fromIndex, matchIndex).append(target);
      //need to check if there are later matches
      fromIndex = matchIndex + source.length();
      matchIndex = input.indexOf(source, fromIndex);
    }
    sb.append(input, fromIndex, input.length());
    return sb.toString();
  }
}
//Time: O (n)
//Space: O(n)

//	indexOf(String str, int fromIndex)
//  Returns the index within this string of the first occurrence of the specified substring, starting at the specified index.


```