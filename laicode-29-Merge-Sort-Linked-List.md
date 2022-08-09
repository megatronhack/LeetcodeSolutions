```
Given a singly-linked list, where each node contains an integer value, sort it in ascending order. The merge sort algorithm should be used to solve this problem.

Examples

null, is sorted to null
1 -> null, is sorted to 1 -> null
1 -> 2 -> 3 -> null, is sorted to 1 -> 2 -> 3 -> null
4 -> 2 -> 6 -> -3 -> 5 -> null, is sorted to -3 -> 2 -> 4 -> 5 -> 6
```

###### 用merge sort algorithm去解决一个not sorted的linked list的问题。

###### 找中点，切两半。不停的这样recursion，到basecase的时候一个一个merge回去。

// The given linked list is not sorted. Using mersort algorithm

// Find the mid node of the linked list.  Example: 1 - 3 - 4 - 3- null, where 2 is the mid node

// Break from mid node to 2 linked list.  Example: 1 - 3 - null,     4 - 3 - null

//recursion till base case

//Merge two list into one list one recursively

//Time O n * logn
//Spce O logn

```java
public ListNode mergeSort(ListNode head) {
    // Write your solution here
    //base case
    if(head == null || head.next == null){
      return head;
    }

    ListNode midNode = findMid(head); // find mid node
    ListNode two = midNode.next;   // create second linked list 
    midNode.next = null;  // delink
    
    ListNode left = mergeSort(head);
    ListNode right = mergeSort(two);   
    return merge(left,right);
  }
  
  // find mid node
  public ListNode findMid(ListNode head){
      ListNode slow = head;
      ListNode fast = head;
      while(fast.next != null && fast.next.next != null){
          slow = slow.next;
          fast = fast.next.next;
      }
      return slow;
  }
  
  //merge two linked list
  public ListNode merge(ListNode one, ListNode two){
     ListNode dummy = new ListNode(0);
     ListNode cur = dummy;
     while(one != null && two != null){
         if (one.value < two.value){
            cur.next = one;
            one = one.next;
         }
         else{
            cur.next = two;
            two = two.next;
         }
         cur = cur.next;
     }
  //post processing of leftover elements
    if (one != null){
      cur.next = one;
    }
    if(two != null){
      cur.next = two;
    }
  return dummy.next;
  }
}

```

