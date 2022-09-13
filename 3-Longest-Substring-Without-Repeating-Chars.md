# 3. Longest Substring Without Repeating Characters

给定一个有重复字符的字符串，找到最长的无重复字符的子串，并输出其长度。

the longest substring without repeating letters for "bcdfbd" is "bcdf. , we should return 4 in this case.

这题是sliding window的经典题型。

为了在每一轮结束之前维护这一性质，

Time complexity: O(N), we only access every character once.

Space complexity: O(N), constant space is needed.

```java
public class Solution {
  public int longest(String input) {
    // Need a HashSet to check the duplicate
    // Need two pointers to keep track of the unduplicate char in the string
    // Need a int to update the longest 

    int slow = 0;
    int fast = 0;
    int longest = 0;
    char[] array = input.toCharArray();
    Set<Character> set = new HashSet<Character>();
    //Treverse the input 
    while (fast < array.length){
      if (set.contains(array[fast])){
        set.remove(array[slow]);
        slow++;
      } else {
        set.add(array[fast++]);
        longest = Math.max(longest, fast - slow);
      }
    }
    return longest;
  }
}

```