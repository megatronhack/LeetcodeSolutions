# Laicode 191. Largest Product Of Length

给定一个数组的字符串，找出长度乘积最大的没有相同字符的两个字符串。

Clarification:
1. 字符串只有小写字母
2. 数组不为null且长度至少为2
3. 没有答案的话返回0

直观的来说，这题我们可以通过双重for循环来枚举，枚举所有字符串组合，全局记录答案。当两个字符串没有重合字符的时候，就试图更新答案。如果我们是通过另外一个双重for循环来判定两个字符串是否有相同字符的话，这题的复杂度大概是O(N^2)，不过N是这题所有字符串的长度和。因为其实每个字符串里的每个字符都要和其他所有字符串的每一个字符进行一次对比，可能会有部分剪枝，但是总体来说复杂度就是这个量级。

那么这题可以优化么？当然，两个方面可以优化。一个是提前找到，二个是优化判定字符串是否有相同字符。我们可以把数组按照字符串长度排序一下，然后从最长的组合开始枚举，以期待提前找到答案并break掉。二来，两个字符串是否有相同字符我们可以通过位运算来优化。因为题目说了字符串只有小写字母，所以我们可以把26个小写字母映射到`int`的0~25位。只要一个字母出现了，对应的位就置为1，我们就可以得到一个字符串的字母组成数。两个字符串对应的数进行按位与操作，如果答案为0就表示两个字符串没有相同字符，反之则有。我们可以提前计算好每个字符串对应的数存在Map里，这样我们判断操作可以优化到平均O(1)的复杂度。

那么优化之后的时间复杂度是多少呢？O(N + nlogn + n^2), N是所有字符串的长度和，而n是字符个数。 N来自于建立每个字符串到对应组成数的Map，nlogn来源于对数组排序，n^2来源于主体算法过程。所以看情况，到底是N更大，还是n^2更大。空间复杂度则是O(n)，因为要存Map。


```java
public class Solution {
  public int largestProduct(String[] dict) {
   // Assumptions: dict is not null and has length >= 2,
    // there is no null String in the dict.
    // The words in the dict only use characters 'a' - 'z'.
    // Get the bit mask for each of the word in the dict,
    // the bit mask is represented by the lowest 26 bits of an integer.
    // each of the bit represents one of the characters in 'a' - 'z'.

   // Time: O(n^2 + |sum of all words’ length|)
   // Space: O(n)

   HashMap<String, Integer> bitMasks = getBitMasks(dict);
   //sor the dict by length of the words in descending order
   Arrays.sort(dict, new Comparator<String>(){
     @Override 
     public int compare(String s0, String s1) {
       if (s0.length() == s1.length()) {
         return 0;
       }
       return s0.length() < s1.length() ? 1 : -1;
     }
   });
   int largest = 0;
    // note the order of constructing all the pairs,
    // we make our best to try largest product.
   for (int i = 1; i < dict.length; i++) {
     for (int j = 0; j < i; j++) {
        // early break if the product is already smaller than
        // the current largest one.
        int prod = dict[i].length() * dict[j].length();
        if (prod <= largest) {
          break;
        }  
        int jMask = bitMasks.get(dict[i]);
        int iMask = bitMasks.get(dict[j]);
        // if two words do not share any common characters,
        // the bit masks "and" result should be 0 since
        // there is not any position such that in the two bit masks
        // they are all 1.
        if ((iMask & jMask) == 0) {
          largest = prod;
        }        
     }
   }
   return largest;
  }

  //get the bit mask for each of the words
  private HashMap<String, Integer> getBitMasks(String[] dict) {
    HashMap<String, Integer> map = new HashMap<String, Integer>();
    for (String str : dict) {
      int bitMask = 0;
      for (int i = 0; i < str.length(); i++) {
        // the 26 characters 'a'-'z' are mapped to 0 - 25th bit.
        // to determine which bit it is for a character x,
        // use (x - 'a') since their values are in a consecutive range.
        // if character x exists in the word, we set the bit at
        // corresponding index to 1.
        bitMask |= 1 << (str.charAt(i) - 'a');
      }
      map.put(str, bitMask);
    }
    return map;
  }
}

```