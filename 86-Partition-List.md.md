```
Given a linked list and a target value T, partition it such that all nodes less than T are listed before the nodes larger than or equal to target value T. The original relative order of the nodes in each of the two partitions should be preserved.

Examples

L = 2 -> 4 -> 3 -> 5 -> 1 -> null, T = 3, is partitioned to 2 -> 1 -> 4 -> 3 -> 5 -> null
```

###### 给一个非sorted的linked list和target value，小的在target左边，大的在target右边。

###### 思路创建2个dummy List, 小的list放小的元素，大的放大的元素，然后接上。

// Create two dummy list, one list is for smaller elements than target, the other list is bigger elements than target

// connect two list 

 // Time On

// Space O1 

```java
    public ListNode partition(ListNode head, int target) {
    // Write your solution here
    //corner case
    if (head == null || head.next == null){
        return head;
    }
    //setting small list dummy and big list dummy
    ListNode small = new ListNode(0);
    ListNode smallCur = small;
    ListNode big = new ListNode(0);
    ListNode bigCur = big;
    while(head != null){
      // if head value is smaller than the target value
      if(head.val < target){
        smallCur.next = head;
        smallCur = smallCur.next;
      }
      //  if head value is biggerthan or equal to the target value
      else{
        bigCur.next = head;
        bigCur = bigCur.next;
      }
      //moving head
      head = head.next;
    }
    
    //connect smallCur list and big list,  since smallCur is at the newst place
    smallCur.next = big.next;   
    
    // de-link the nodes after bigCur, since the big Cur is at the newest place
    bigCur.next = null;
        
        
    return small.next; 
  }
```

