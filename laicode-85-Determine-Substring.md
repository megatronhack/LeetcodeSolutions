# Laicode 85. Determine If One String Is Another's Substring

给定两个字符串，`large`和`small` 判断第二个是否是第一个的子串。

Clarification:
+ 两个输入为null怎么办？题目保证不为null
+ small是空串怎么办？返回0



2个forloop，检查substring是否在largestring里。

Time complexity: O(M + N) as expected, O(MN)*n in worst case 

Space:O1

```java
public class Solution {
  public int strstr(String large, String small) {
    // Write your solution here
    if (large.length() < small.length()){
      return -1;
    }
    if(small.length() == 0){
      return 0;
    }

    for (int i = 0; i <= large.length() - small.length(); i++){
      if (equals(large, i, small)){
        return i;
      }
    }
    return -1;
  }
  
  public boolean equals(String large, int start, String small){
    for (int i = 0; i < small.length(); i++){
      if (large.charAt(i + start) != small.charAt(i)){
        return false;
      }
    }
    return true;
  }
  //time  (m-n) *n
  //space o1
}

```