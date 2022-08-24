# Laicode 25. K Smallest In Unsorted Array

## Max Heap Approach

这题可以采用大顶堆的方法。当大顶堆内元素不足k个的时候持续放入，当大顶堆内元素已经大于k个了就弹出堆顶最大的那个，这样我们就可以保持堆内始终放着最小的k个元素。不过这也要求我们大顶堆建立的时候`maxSize = k + 1`来让我们能放`k+1`个元素进去，来获得比较的余地。

当然了，这题需要用到大顶堆。一般我们是用Java的`PriorityQueue`类，但是呢这里我们要深入理解堆操作的原理，所以自己实现一个大顶堆。大顶堆放入新元素的时间复杂度是O(logN)，弹出堆顶时间复杂度也是O(logN)，这里的N是堆的大小。所以整个流程下来，时间复杂度是O(Nlogk)，空间复杂度是O(k)，这里的N是输入数组的大小。

Time complexity: O(Nlogk)

Space complexity: O(k)

```java
public class Solution {
  public int[] kSmallest(int[] array, int k) {
    // Write your solution here
    int[] result = new int[k];
    if(array.length == 0 || k == 0){
      return new int[0];
    }
  //use a maxheap to store the k smallest elements
  PriorityQueue<Integer> maxHeap = new PriorityQueue<>(k, new Comparator<Integer>(){
     @Override
     public int compare(Integer a, Integer b){
       if(a.equals(b)){
         return 0;
       }
       return a > b ? -1 : 1;
     }
  });
    
    for(int i = 0; i < array.length; i++){
        if(i < k){
          maxHeap.offer(array[i]);
        }
        else{
          if(array[i] < maxHeap.peek()){
            maxHeap.poll();// pollFrist
            maxHeap.offer(array[i]); 
          }
        }
    }
    //write elements back to the array
    for (int i = k - 1; i >= 0; i--){
      result[i] = maxHeap.poll();
    }
    return result;
  }
}

```