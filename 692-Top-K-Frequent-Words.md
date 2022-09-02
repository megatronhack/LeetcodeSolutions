# 692. Top K Frequent Words

给定一个数组的字符串，输出出现频率最高的k个字符串。

这题用Hash表配合小顶堆来解决。首先，我们要先得到每个单词出现的频率。得到频率的哈希表之后，我们把哈希表的每一个元素放入小顶堆，小顶堆的比较条件是
+ 如果两个单词频率不一样，那就比较频率
+ 如果两个单词频率一样，那就字典序大的反而小，因为频率一样的话，字典序小的要排在前面。

当小顶堆不足k个元素时，持续加入哈希表的元素。当小顶堆已经有了k个元素，而且当前元素的频率大于等于堆顶的元素频率时，先放入堆中，再弹出堆顶。这样我们就可以时刻保持堆里是目前为止频率最高的k个单词，频率相同的字典序小的会尽量被留在堆里。

最后，我们依次弹出堆顶元素到列表里，并把列表反转一下，就是从高到低的top k了。

Time complexity: O(n + nlogk), n for get frequency map, poll and offer operation is logk.

Space complexity: O(n + k), n for hash map and k for heap.

```java
public class Solution {
  public String[] topKFrequent(String[] combo, int k) {
   //corner case
   if (combo.length == 0){
     return new String[0];
   }
   //get all distinct strings as keys and their frenquencies as value
   Map<String, Integer> freqMap = getFreqMap(combo);
   //minheap on the frenquencirs of the strings
   //Notice: using Map.Entry as element type directly so that all the operations are mostly efficient
   PriorityQueue<Map.Entry<String, Integer>> minHeap = new PriorityQueue<>(k, new Comparator<Map.Entry<String, Integer>>(){
     @Override
     public int compare(Map.Entry<String, Integer> e1, Map.Entry<String, Integer> e2){
       return e1.getValue().compareTo(e2.getValue());
     }
   });

   for (Map.Entry<String, Integer> entry : freqMap.entrySet()){
     if (minHeap.size() < k){
       minHeap.offer(entry);
     }else if(entry.getValue() > minHeap.peek().getValue()){
       minHeap.poll();
       minHeap.offer(entry);
     }
   }
   //because the return is an array and requires the strings sorted by frenquencies, use helper method
   return freqArray(minHeap);
  }

  private Map<String, Integer> getFreqMap(String[] combo){
    Map<String, Integer> freqMap = new HashMap<>();
    for  (String s : combo){
      Integer freq = freqMap.get(s);
      if (freq == null){
        freqMap.put(s, 1);
      }else{
        freqMap.put(s, freq + 1);
      }
    }
    return freqMap;
  }

  private String[] freqArray(PriorityQueue<Map.Entry<String, Integer>> minHeap){
    String[] result = new String[minHeap.size()];
    for (int i = minHeap.size() - 1; i >= 0; i--){
      result[i] = minHeap.poll().getKey();
    }
    return result;
  }
}
//Time: put in hashmap O(n), use minheap O(nlogk), pop result from heap O(klogk)
//Space: O(n)

```