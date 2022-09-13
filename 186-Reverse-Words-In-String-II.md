# 186. Reverse Words in a String II

给定一个句子，把整个句子的单词反转过来。比如`the sky is blue`变成`blue is sky the`。

Clarification:
+ 有无leading/trailing zero？没有
+ 单词之间只有一个空格？是

问清楚具体的条件之后，思路很简单了。既然是单词对调，那么我们就先把整个字符串反转，然后再把每个单词自身再反转一下就好了。比如`the sky is blue`->`eulb si yks eht`->`blue is sky the`。

具体过程就是先把字符串反转，然后遍历。`Start`记录当前单词的开始位置，当`i + 1`是空格时说明当前是一个单词的结束，直接反转本单词。空格后肯定是下一个单词，所以再更新一下Start为空格的后一个位置就好。

不过需要注意的是由于没有leading/trailing zero，所以我们单独处理`i == array.length - 1`的情况。

Time complexity: O(N)

Space:O(n)

```java
public class Solution {
  public String reverseWords(String input) {
    // turn the string input to an array 
    // reverse the array
    //find the start and end index of each word, then reverse the word one by one
    //return the reversed array back to string

    char[] array = input.toCharArray();
    reverse(array, 0, array.length - 1);
    //reverse each word
    int start = 0;
    //find start and end index for this array
    for (int i = 0; i < array.length; i++){

      if (array[i] != ' ' && (i == 0 || array[i-1] == ' ')){
       start = i;
      }
      //the end of the index
      if (array[i] != ' ' && (i + 1) == array.length || array[i + 1] == ' '){
       reverse(array, start, i);
      }
    }
    return new String(array);
  }

  private void reverse(char[] array, int left, int right){
    while (left <= right){
      swap(array, left, right);
      left++;
      right--;
    }
  }

  private void swap (char[] array, int left, int right){
    char tmp = array[left];
    array[left] = array[right];
    array[right] = tmp;
  }
}

```