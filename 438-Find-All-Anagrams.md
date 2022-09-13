# 438. Find All Anagrams in a String

给定两个字符串`s`和`pl，在`s`中找出所有与`l`异构的子串，并输出所有的子串起始的下标。

examples: l = "abcbac", s = "ab", return [0, 3] since the substring with length 2 starting from index 0/3 are all anagrams of "ab" ("ab", "ba").

Clarification:
+ 字符范围？小写字母
+ s和l的长度？只保证p的长度不为0

sliding window经典题。 通过hashmap记录short string的char和出现次数。

 public class Solution {  public boolean match(String input, String pattern) {    //Iterative way    //case 1: if the char is a character compare whether they are equal    //case 2: if the char is a digit, move the pointer in string input by count positions    //Having traverse all the elements, then compare whether the two pointers reached the end of the input and pattern    int si = 0; //    int ti = 0;    while (si < input.length() && ti < pattern.length()){      if (pattern.charAt(ti) < '0' || pattern.charAt(ti) > '9') {        if (input.charAt(si) != pattern.charAt(ti)) {          return false;        }        si++;        ti++;      } else {        int count = 0;        while (ti < pattern.length() && pattern.charAt(ti) >= '0' && pattern.charAt(ti) <= '9') {          count = count * 10 + (pattern.charAt(ti) - '0');          ti++;        }        si += count;      }    }    return si == input.length() && ti == pattern.length();  }}//Time:O(n)//Space:O(1)​java

通过滑动窗口

//Time: O(n)

//Space: O(n) where n is the number of characters in input string alphabet

```java
public class Solution {
  public List<Integer> allAnagrams(String sh, String lo) {
    //Assumptions: sh and lo are not null, sh is not empty
    List<Integer> result = new ArrayList<Integer>();
    if (lo.length() == 0){
      return result;
    }
    //when short string is longer than long string, no way of short string is anagram of long string.
    if (sh.length() > lo.length()){
      return result;
    }
    Map<Character, Integer> map = countMap(sh);
    //when we get an instance of 'a' in 1, we let count of 'a' decremented by 1
    //and only when the count is from 1 to 0, we have 'a' totally matched
    int match = 0;
    //when move the sliding window by one step from left to right,what we only need to change is
     //1. remove the leftmost character at the previous sliding window
     //2. add the rightmost character at the current sliding window
    for (int i = 0; i < lo.length(); i++){
        //handle the new added character(rightmost) at current sliding window
      char tmp = lo.charAt(i);
      Integer count = map.get(tmp);
      if (count != null){
        //the number of needed count should be --.
        //and only when the count is from 1 to 0, we find an additional
        //match of distinct character
        map.put(tmp, count - 1);
        if (count == 1){
          match++;
        }
      }
      //handle the leftmost character at the previous sliding window
      if (i >= sh.length()) {
        tmp = lo.charAt(i - sh.length());
        count = map.get(tmp);
        if (count != null){
        //the number of needed count should be ++.
        //and only when the count is from 0 to 1, we are short for one
        //match of distinct character
          map.put(tmp, count + 1);
          if (count == 0){
            match--;
          }
        }
      }
      //for the current sliding window, if all the disctinct characters are matched, the count are all zero
      //we find the anagram 
      if (match == map.size()){
        result.add(i - sh.length() + 1);
      }
    }
    return result;

  }

  private Map<Character, Integer> countMap(String sh){
    Map<Character, Integer> map = new HashMap<Character, Integer>();
    for (char ch : sh.toCharArray()){
      Integer count = map.get(ch);
      if (count == null){
        map.put(ch,1);
      } else {
        map.put(ch, count + 1);
      }
    }
    return map;
  }
}
//Time: O(n)
//Space: O(d) where d is the number of characters in input string alphabet
```