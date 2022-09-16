# Laicode 117. Array Deduplication III

和前面两题差不多，只不过这次是不保留任何重复元素。

这次我们需要重新审视一下这题，`[0, slow)`依然存放去重之后的元素。但是这题不能像前两题一样实现了，这题我们需要跳过整段的重复元素。所以快指针在往后走的时候需要用一个begin来记录起始位置，然后跳过所有是重复的元素。只有遇见非重复元素时候，才加入`[0, slow)`。

Time complexity: O(N)

Space complexity: O(N)

```java
public class Solution {
  public int[] dedup(int[] array) {
    if (array == null || array.length <= 1) {
      return array;
    }
    int slow = 0;
    char[] array = input.toCharArray();
    for(int i = 0; i < array.length; i++){
       if(i == 0  || array[i] != array[i - 1]){
         array[slow++] =array[i];
       }
       else{
         continue;
       }
    }
    return new String(array, 0, slow);
  }
}
```

或者通过flag来判断，创建一个新的array

On和O1

```
public class Solution {
  public int[] dedup(int[] array) {
    if (array == null || array.length <= 1) {
      return array;
    }
    int end = 0;
    //use flag to see if there is any duplicates of array[end]
    boolean flag = false;
    for (int i = 1; i < array.length; i++) {
      if (array[i] == array[end]) {
        flag = true;
      } else if (flag == true) {
        array[end] = array[i];
        flag = false;
      } else {
        array[++end] = array[i];
      }
    }
    return Arrays.copyOf(array, flag ? end : end + 1);
  }
}
//tc: O(n)
//sc: O(1)

```

