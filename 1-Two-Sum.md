# 1. Two Sum

Two Sum没必要解释

Method 1:

// time O(n)  
// space o(n)

```java
public class Solution {
  public boolean existSum(int[] array, int target) {
    // Write your solution here
    Set<Integer> set = new HashSet<Integer>();
    for (int num : array){
       if (set.contains(target - num)){
         return true;
       }
       set.add(num);
    }
    return false;
  }
}
// time On  
// space oN
```

Method 2:

/Time:O(n^2)
Space:O(1)

```Java
public class Solution {
  public boolean existSum(int[] array, int target) {
    // Write your solution here
    for (int i = 0; i < array.length -1; i++) {
      for (int j = i + 1; j < array.length; j++) {
        if (array[i] + array[j] == target) {
          return true;
        }
      }
    }
    return false;
  }
}
//Time:O(n^2)
//Space:O(1)
```

Method 3:

Time: O(nlogn)   Array Sort time 
Space: O(1)

```java
public class Solution {
  public boolean existSum(int[] array, int target) {
    // Write your solution here
    int left = 0;
    int right = array.length - 1;
    Arrays.sort(array);
    while (left < right){
      int sum = array[left] + array[right];
      if (sum == target){
        return true;
      }
      else if( sum < target) {
       left++;
      }
      else{
      right--;
      }
    }
    return false;
  }
}
// time nlogn
// space o1
```

**Examples**

- A = {1, 2, 3, 4}, target = 5, return true (1 + 4 = 5)
- A = {2, 4, 2, 1}, target = 4, return true (2 + 2 = 4)
- A = {2, 4, 1}, target = 4, return false