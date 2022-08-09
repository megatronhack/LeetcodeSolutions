```
Reorder the given singly-linked list N1 -> N2 -> N3 -> N4 -> … -> Nn -> null to be N1- > Nn -> N2 -> Nn-1 -> N3 -> Nn-2 -> … -> null

Examples

L = null, is reordered to null
L = 1 -> null, is reordered to 1 -> null
L = 1 -> 2 -> 3 -> 4 -> null, is reordered to 1 -> 4 -> 2 -> 3 -> null
L = 1 -> 2 -> 3 -> null, is reordred to 1 -> 3 -> 2 -> null
```

###### 给与一个sorted或者非sorted的linkedlist，顺序其实无所谓。随意例子，比如1-2-3-4，变成1-4-2-3。思路找midNode切两半，第二段反转下，创个dummy然后一个一个接回去。

// Find the mid node of the linked list.  Example: 1 - 2 - 3 - 4 - null, where 2 is the mid node

// Break from mid node to 2 linked list.  Example: 1 - 2 - null,     3 - 4 - null

 // Reverse the second list. For example:  Example: 4 - 3 - null

 // Merge two list into one list one node by one node.  Example: 1 - 4 - 2 - 3 - null 

 // Time On  

 // Space O1

```java
  public ListNode reorder(ListNode head){
      //corner case
      if (head == null || head.next == null){
        return head;
      }
      // Find midNode
      ListNode midNode = findMid(head);
      // Break into 2 lists
      ListNode one = head;
      ListNode sec = midNode.next;
      midNode.next = null; // Disconnect two lists
      //merge one and the reversed the second list
      return merge(one, reverse(sec));
  }

  public ListNode findMid(ListNode head){
    ListNode slow = head;
    ListNode fast = head;
    while(fast.next != null && fast.next.next != null){
      slow = slow.next;
      fast = fast.next.next;
    } 
    return slow;
  }

  public ListNode reverse(ListNode head){
       //base case
       if (head == null || head.next == null){
         return head;
       } 

      ListNode newHead = reverse(head.next);
      head.next.next = head;
      head.next = null;

      return newHead;
  }
  
  public ListNode merge(ListNode one,ListNode two){
    ListNode dummy = new ListNode(0);
    ListNode cur = dummy;
    
    while(one != null && two != null){  //
    //connect dummy to one
    cur.next = one;
    //moving forward one
    one = one.next;
    //moving forward cur
    cur = cur.next;
    
    //connect to two
    cur.next = two;
    //moving forward two
    two = two.next;
    //moving forward two
    cur = cur.next;
  }

  //post precessing of leftovers
  if(one != null){
    cur.next = one;
  }

  if(two != null){
    cur.next = two;
  }

  return dummy.next;  

  }
```

