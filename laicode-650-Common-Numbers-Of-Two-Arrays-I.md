# Laicode 650. Common Numbers Of Two Arrays I(Array version)

和[laicode 652. Common Numbers Of Two Sorted Arrays](laicode-652-Common-Numbers-Of-Two-Sorted-Arrays.md)一样，只不过给定的数组没有排好序。那就排好序再用同样的双指针方法来做。

Time complexity: O(nlogn) because of the sorting process.

Space complexity: Depends on the sorting algorithm. Quick sort takes O(logn) in average, and O(n) in worst case. Merge sort takes O(n) all the time.

```java
public class Solution {
  public List<Integer> common(int[] a, int[] b) {
    // Write your solution here
    //corner
    if (a == null || b == null){
      return null;
    }
    Arrays.sort(a);
    Arrays.sort(b);
    List<Integer> result = new ArrayList<>();
    Set<Integer> set = new HashSet<>();
    // adding first array elements to set with no duplicates; 
     for (int i = 0; i < a.length; i++){
        set.add(a[i]);
     }
   // compare first array and second array
     for (int i = 0; i < b.length; i++){
        if (set.contains(b[i])){
          result.add(b[i]);
        }
     }

    return result;
  }
}
//time nlogn
//space on
```