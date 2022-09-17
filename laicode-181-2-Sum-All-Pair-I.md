# Laicode 181. 2 Sum All Pair I

还是two sum，不过答案不唯一，要找出所有答案。

因为题目不保证没有重复元素，所以如果**有重复元素**满足答案的话，肯定需要都记录下来。

每轮循环先看看`index Map`里有没有`target - array[i]`，有的话得到所有对应的下标和当前的`i`加入答案。然后记录`array[i]`出现在`i`下标再结束本轮循环。

Time complexity: O(N)

Space complexity: O(N)

```java
public class Solution {
  public List<List<Integer>> allPairs(int[] array, int target) {
    // Write your solution here
    List<List<Integer>> result = new ArrayList<>();
    Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
    // key is number, its value is all possible indices
    for (int i = 0; i < array.length; i++){
       List<Integer> indices = map.get(target - array[i]);
    // if target - array[i] is in the map
    //we can get all the paris(j,i), well i is current index
       if (indices != null){
         for (int j : indices){
           result.add(Arrays.asList(j,i));
         }
       }
    // add current index array[i]  value with all possible indices to the map 
     if (!map.containsKey(array[i])){
       map.put(array[i], new ArrayList<Integer>());
     }  
     map.get(array[i]).add(i);
    }
    return result;
  }
}
// time average on  wrose case on^2 because we dont have manby indices for for loop
// space On

```

**Examples**

- A = {1, 3, 2, 4}, target = 5, return [[0, 3], [1, 2]]
- A = {1, 2, 2, 4}, target = 6, return [[1, 3], [2, 3]]