# Laicode 73. Combinations Of Coins

和[leetcode 39](39-Combination-Sum.md)差不多，只是答案的表现性质稍有区别。我们这里用一个和`coins`等长的List来表明每个面额需要多少个才能组成`target`，所以每个答案的长度都是和coins等长的。

![Laicode 73. Combinations Of Coins](assets\images\Laicode 73. Combinations Of Coins.jpg)

Time complexity: O(N * (T/M)^N).  99^N  N is the number of denominations, T is target value and M is the min value among the denominations.

Space complexity: O(N), n level call stack and n size combination. Result space is not counted.

```java
public class Solution {
 // each combination is represented as a List<Integer> cur,
 //and cur.get[i] = the number of coins of coins[i]
 //all the combinations are stored in the result as a list of List<Integer> in result
  public List<List<Integer>> combinations(int target, int[] coins) {
    // Write your solution here
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    List<Integer> cur = new ArrayList<>();
    dfs(result,cur,coins,target,0);
    return result;
    
  }

  public void dfs(List<List<Integer>> result, List<Integer> cur, int[] coins, int target, int index){
    if(index == coins.length - 1){
      if(target % coins[coins.length - 1] == 0){
       cur.add(target / coins[coins.length - 1]);
       result.add(new ArrayList<Integer>(cur));
       cur.remove(cur.size() - 1);
      }
    return; 
    }
  //for coins[index], we can pick 0,1,2,...target / coins[index] coins  
   int max = target / coins[index];
   for(int i = 0; i <= max; i++ ){
      cur.add(i);
      //remember to modify the remaining cents for the next level
      dfs(result,cur,coins,target - i * coins[index], index + 1);
      cur.remove(cur.size() - 1);
   }
  }
}

```