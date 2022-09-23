# Laicode 651. Common Numbers Of Two Arrays II(Array version)

这题还是和[laicode 652. Common Numbers Of Two Sorted Arrays](laicode-652-Common-Numbers-Of-Two-Sorted-Arrays.md)差不多，只不过是无序。先排序，后用双指针。

Time complexity: O(nlogn) because of the sorting.

Space complexity: Depends on the sorting algorithm.

```java
public class Solution {
  public List<Integer> common(int[] A, int[] B) {
    // Write your solution here
    if (A == null || B == null){
      return null;
    }
    HashMap<Integer, Integer> hashMap = new HashMap<>();
    List<Integer> result = new ArrayList<>();     
    //sort
    Arrays.sort(A);
    Arrays.sort(B);
    //putting elements and its appearances into hashMap
    for (int i = 0; i < A.length; i++) {
      Integer count = hashMap.get(A[i]);
      if (count == null) {
        hashMap.put(A[i], 1);
      } else {
        hashMap.put(A[i], count + 1);
      }
    }
    //check common
    for(int i = 0; i < B.length; i++){
      if (!hashMap.containsKey(B[i])){
        continue;
      }
      else{
      int count = hashMap.get(B[i]);
       if (hashMap.get(B[i]) >= 1){
        result.add(B[i]);
        hashMap.put(B[i], count - 1 );
       }
      }
    } 
     return result; 
  }
}
//on
//on
```