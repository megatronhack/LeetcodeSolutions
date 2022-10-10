# 23. Merge k Sorted Lists

给定k个有序链表，把他们合并为一个有序链表。

不是很懂，这也能算hard题？是我所在的层数太低了么？难道我在第一层而这题在第五层？

新建一个dummy表头用来存放答案。用小顶堆存放所有链表的表头然后开始做以下两件事：
+ 从小顶堆里取出当前最小的节点加入答案。
+ 如果当前这个节点的next不为空的话，那就把它放入小顶堆。

重复上述两件事情直到堆为空，最后我们就得到了一个有序的链表。

Time complexity: O(N * logk) where k is the number of lists and N is the total number of nodes of all k lists.

Space complexity: O(k). Min heap will have k elements most of the time.

```java
public class Solution {
  public ListNode merge(List<ListNode> listOfLists) {
    // Write your solution here/.
    PriorityQueue<ListNode> minHeap = new PriorityQueue<ListNode>(11, new MyComparator());
    ListNode dummy = new ListNode(0);
    ListNode cur = dummy;
    for (ListNode node : listOfLists){
        if(node != null){
          minHeap.offer(node);
        }
    }
    while(!minHeap.isEmpty()){
        cur.next = minHeap.poll();
        if (cur.next.next != null){
          minHeap.offer(cur.next.next);
        }
        cur = cur.next;
    } 
    return dummy.next;
  }   
    
    static class MyComparator implements Comparator<ListNode>{
        @Override
        public int compare(ListNode o1, ListNode o2) {
          if(o1.value == o2.value){
              return 0;
          }
        return o1.value < o2.value ?  -1 : 1;
        }   
    }
}

//time n * logk
//space k
```