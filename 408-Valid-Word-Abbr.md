# 408. Valid Word Abbreviation

**Examples:**

- pattern “s11d” matches input “sophisticated” since “11” matches eleven chars “ophisticate”.

给定一个字符串和对应的缩略写法，判断是否匹配。

根据题意，一个字符串有很多种缩写，所以这里我们要仔细处理。采用双指针的形式，

`si`来遍历字符串。

t`i`来遍历缩写。

当`ti`遇到字符时，就看看`si`和`ti`指向的字符是否一致。一致的话，各自走一步。不一致的话，立刻返回false。

当`ti遇到数字时，就得到后面整个数字count，然后让si`对应地往后移动count位。这样只要最后他俩同时遍历结束，就可以说字符串你和缩写匹配得上。

不过这题有个比较烦人的地方，就是数字不可以有leading zero，所以在判断`ti`是否是数字的时候还需要判断是否是0。是0的话，就直接忽略，这样最后我们就可以返回false。

Time complexity: O(n)

Space complexity: O(1)

```java
public class Solution {
  public boolean match(String input, String pattern) {
    //Iterative way
    //case 1: if the char is a character compare whether they are equal
    //case 2: if the char is a digit, move the pointer in string input by count positions
    //Having traverse all the elements, then compare whether the two pointers reached the end of the input and pattern
    int si = 0; //
    int ti = 0;
    while (si < input.length() && ti < pattern.length()){
      if (pattern.charAt(ti) < '0' || pattern.charAt(ti) > '9') {
        if (input.charAt(si) != pattern.charAt(ti)) {
          return false;
        }
        si++;
        ti++;
      } else {
        int count = 0;
        while (ti < pattern.length() && pattern.charAt(ti) >= '0' && pattern.charAt(ti) <= '9') {
          count = count * 10 + (pattern.charAt(ti) - '0');
          ti++;
        }
        si += count;
      }
    }
    return si == input.length() && ti == pattern.length();
  }
}
//Time:O(n)
//Space:O(1)

```