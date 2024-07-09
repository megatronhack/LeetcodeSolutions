# Laicode 208. Majority Number III

这题就是更加通用的情况了，给定一个数组，Majority Number定义为出现超过`1/k`次就好。

那么我们这题用一个`Map<Integer, Integer> counter`来记录每个candidiate出现过多少次。遍历数组的时候，首先检查当前数字是否在`counter`里。如果在的话，把对应的次数加一。如果不在的话，还得看`counter`里的候选数字数量是否有`k-1`个。如果不足的话，就把它当成新的候选数字加入。如果已经满`k-1`个，那就所有的候选数字对应的count都要减一。不过这里要注意，如果减一之后变成0的话，就可以直接从counter里删除掉了。然后在实现的时候，一定注意在keySet基础上新建一个ArrayList再访问，不然会有`ConcurrentModificationException`。

Time complexity: O(N) in average. Even if we have to iterate over the map to subtract the frequency, the total number of remove operation is less than the total number of put operation. So it's O(N).

Spaec complexity: O(k) because of the map.

```java
public class Solution {
  public List<Integer> majority(int[] array, int k) {
    // Traverse the array and use a hashmap to keep records of the number and the occurence
    // Use a set to record the numbers with occurence more than array.length / k
    // Add the elements from the set to a list and return as the result
    // TC: O(n) SC: O(n)
    HashMap<Integer, Integer> map = new HashMap<>();
    Set<Integer> set = new HashSet<>();
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < array.length; i++) {
      if (map.containsKey(array[i])) {
        int count = map.get(array[i]);
        map.put(array[i], count + 1);
      } else {
        map.put(array[i], 1);
      }
      if (map.get(array[i]) > array.length / k) {
        set.add(array[i]);
      }
    } 
    for (int num : set) {
      result.add(num);
    }
    return result;
  }
}
```

