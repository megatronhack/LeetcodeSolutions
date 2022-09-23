# 254. Factor Combinations

给定一个数n，返回所有可能的因数分解结果。

经典的DFS题目。我们先得到`n`所有的因数，然后每个因数为一层进行dfs。base case是所有因数均遍历完了。如果正好分解结束，就把当前的因数分解组合加入答案。不管是否分解完，因数遍历完了都需要返回。

对于每一层的因数来说，我们先针对不用该因数的情况进行深搜，再对用这个因数的情况进行深搜。用这个因数又分用几次，遍历每一种情况进行深搜直到不可分为止。返回前，记得恢复状态。![254. Factor Combinations](assets\images\254. Factor Combinations.jpg)

Time complexity: hard to say.

Space complexity: depends on how many factors does n have.


```java
public class Solution {
  public List<List<Integer>> combinations(int target) {
    // Need to get all the factors and then use dfs to solve this question
    // Traverse all the factors, decide how may factors we can choose at current level
    // if the final target == 1 afters dividing the factors, 
    // then the combination of theses factors is one of the solution
    //tc: O(n^n) assume that n is the number of factors
    //sc: O(n)
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    if (target <= 1) {
      return result;
    }
    List<Integer> cur = new ArrayList<>();
    List<Integer> factors = getFactor(target);
    helper(target, factors, 0, cur, result);
    return result;
  }

  private List<Integer> getFactor(int target) {
    List<Integer> factors = new ArrayList<>();
    for (int i = 2; i <= target / 2; i++) {
      if (target % i == 0) {
        factors.add(i);
      }
    }
    return factors;
  }
  
  private void helper(int target, List<Integer> factors, int index, List<Integer> cur, List<List<Integer>> result) {
    //base case
    if (factors.size() == index) {
      if (target == 1){
        result.add(new ArrayList(cur));
      }
      return;
    }
    //choose to divide current factor or not
    helper(target, factors, index + 1, cur, result);
    //if the current target can divide the factor and the remainder is 0 then we can choose the current factor
    //use the while loop to decide the number of current factors we can divide 
    int factor = factors.get(index);
    int size = cur.size();
    while (target % factor == 0) {
      target /= factor;
      cur.add(factor);
      helper(target, factors, index + 1, cur, result);
    }
    cur.subList(size, cur.size()).clear();
  }
}

```

**Example**

Give A = 24

since 24 = 2 x 2 x 2 x 3

​       = 2 x 2 x 6

​       = 2 x 3 x 4

​       = 2 x 12

​       = 3 x 8

​       = 4 x 6

your solution should return

{ { 2, 2, 2, 3 }, { 2, 2, 6 }, { 2, 3, 4 }, { 2, 12 }, { 3, 8 }, { 4, 6 } }

**note:** duplicate combination is not allowed.