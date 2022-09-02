# Laicode 281. Remove Spaces

去除字符串里的leading, trailing and duplicated space，单词之间只留下1个空格。

那么依然还是双指针的思路，slow指针的含义是[0, slow)记录着当前删去指定空格之后的字符串。分类讨论，
+ 当前sc[i]字符是空格的话
  + write为0的话，说明正式的字符串还没开始，所以这是leading空格，跳过
  + write不为0，但是array[i - 1]为空格的话，说明这是个连续的空格，跳过
  + 如果不满足以上两个条件，说明这是个单词之间的首个空格，放到write，write后移
+ 当前array[i]字符不是空格的话，放到write，write后移

以上流程做完以后，我们只能保证字符串头部没有多余的空格，以及每个单词后面最多只有1个空格。但是根据题意，最后一个单词后面不能跟空格，所以最后检查一下`write - 1`的位置是不是空格，是的话就去掉。

Time complexity: O(n)

Space complexity: O(n)

```java
public class Solution {
  public String removeSpaces(String input) {
    // Write your solution here
    if (input.isEmpty()){
      return input;
    }
    char[] array = input.toCharArray();
    int write = 0;
    for (int i = 0; i < array.length; i++){
      if (array[i] == ' ' && (i == 0 || array[i-1] == ' ')){
        continue;
      }
      array[write++] = array[i];
    }
    //post processing: if the last element is empty space
    if (write > 0 && array[write-1] == ' '){
      write--;
    }
    return new String(array, 0, write);
  }
}
//Time:O(n)
//Space:O(m)

```