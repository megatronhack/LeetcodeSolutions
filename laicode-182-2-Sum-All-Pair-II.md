# Laicode 182. 2 Sum All Pair II

还是two sum，但是不返回下标组合而是返回所有的元素组合，并且不能有重复。

这题和之前的two sum不太一样，返回元素组合不说，还兼具去重。那么我们就不能用元素到下标的映射了，而是元素到出现次数的映射。分情况讨论，
+ 当前元素 * 2 正好是`target`，那么只要当前元素之前出现过一次，那么这就是个组合。
+ 当前元素* 2 不是`target`，只要`target - array[i]`出现过并且当前`array[i]`没有出现过，那么我们就可以保证这个组合没有用过。加入答案。

结束时记得更新`array[i]`出现的次数。

Time complexity: O(N)

Space complexity: O(N)

```java
public class Solution {
  public List<List<Integer>> allPairs(int[] array, int target) {
    // Find all distinct pairs and return as a list
    // Use a hashmap to record the num and the count of the num in the array
    //case 0: if num * 2 = target, the current count for the num is 1 then add it in the result
    //case 1: if hahmap contains a num whilch is target - num then add it to the result
    //Update the hashmap for current num: 
    //if the count is null, add current num in the hashmap otherwise count of the num + 1
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    HashMap<Integer, Integer> map = new HashMap<>();
    //key: num in the array 
    //value: count of the num
    for (int num : array) {
      Integer count = map.get(num);
      if (num * 2 == target && count != null && count == 1) {
        result.add(Arrays.asList(num, num));
      }
      if (map.containsKey(target - num) && count == null) {
        result.add(Arrays.asList(target - num, num));
      }
      if (count == null) {
        map.put(num, 1);
      } else {
     map.put(num, count + 1);
      }
    }
    return result;
  }
}
//TC: O(n)
//SC: O(n)

```

**Examples**

- A = {2, 1, 3, 2, 4, 3, 4, 2}, target = 6, return [[2, 4], [3, 3]]