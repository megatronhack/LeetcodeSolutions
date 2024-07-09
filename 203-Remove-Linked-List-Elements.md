```
Remove all elements from a linked list of integers that have value val.

Example
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5
```

 删元素。创建dummylist，做检查，连进去。

 有意思的是， 算法本身就包含了些corner case，比如只有1个元素的时候。

  //create dummy list

  //check one by one in the real list and connect qualified elements to the dummy list

  // interesting thing of this is, we don't need to pre-write corner case since its already covered in algorithm

  //on 

  //o1

```java
   if (head == null){
      return null;
    }
   
    ListNode dummy = new ListNode(0);
    ListNode cur = dummy;
    while(head != null){
      //then head value is not equal to the target value we letting the dummy list to connect them
      if (head.value != val){
         cur.next = head;
         cur = cur.next;
      }
      //if they are equal, we jumped this element
      else{
        cur.next = head.next;
      }
      // head elements moving forward
      head = head.next;
    }
  return dummy.next;
  }
```

