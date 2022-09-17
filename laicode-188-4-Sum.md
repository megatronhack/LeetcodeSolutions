# Laicode 188. 4 Sum

给定一个数组，判断里面是否存在和为`target`的四元组。

首先我们把数组进行排序，方便操作。我们用一个`TwoSumPair`来表示一个双元组他们的和对应某个值，我们遍历一次数组得到所有可能的two sum对应的双元组(i1, j1)的Map，每一个和对应的双元组要选取首次出现的地方。



Time complexity: O(N^2)

Space complexity: O(N)

```java
public class Solution {
  public boolean exist(int[] array, int target) {
    //assume array is not null and with length >= 4
    Map<Integer, Pair> map = new HashMap<>();
    for (int i = 1; i < array.length; i++) {
      for (int j = 0; j < i; j++) {//we should gurantee that we can always loot at the pair with
      //the smallest right index
        int pairSum = array[j] + array[i];
        if (map.containsKey(target - pairSum) && map.get(target - pairSum).right < j) {
        //we need to gurantee there exists another pair with right index smaller than the current pair's
        //left index
        return true;
      }
      if (!map.containsKey(pairSum)) {
        map.put(pairSum, new Pair(j, i));
      }
    }
   }
   return false;
  }

  static class Pair {
    int left; 
    int right;
    Pair(int left, int right) {
      this.left = left;
      this.right = right;
    }
  }
}
//tc: O(n^2)
//sc: O(n)
```