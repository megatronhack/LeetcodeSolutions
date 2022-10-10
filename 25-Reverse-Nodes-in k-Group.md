

通过一个指针去记录当前traverse了多少个node， count=k的时候就把当前的nodes反转，同时需要把head.next接上。（通过recursion方式接上）

通过一个helper function去反转当前k个nodes。

Hard

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return *the modified list*.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.



```Java
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

```Java
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

 * ```Java
   /**
   
    * Definition for singly-linked list.
   
    * public class ListNode {
   
    * int val;
   
    * ListNode next;
   
    * ListNode() {}
   
    * ListNode(int val) { this.val = val; }
   
    * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
   
    * }
      */
      class Solution {
      public ListNode reverseKGroup(ListNode head, int k) {
          //Need to reverse k nodes, and combine the newhead to the former last node
          int count = 0;
          ListNode prev = head;
          while (count < k && prev != null) {
              prev = prev.next;
              count++;
          }
          
   
          if (count == k) {
              ListNode reverseHead = reverseNode(head, k);
              head.next = reverseKGroup(prev, k);//link the former head node with the new head
   //what to return 
              return reverseHead;
          }
   //what if there are not k nodes for the last recursion
          return head;
   
      }
      public ListNode reverseNode(ListNode head, int k) {
          ListNode prev = null;
          while(k > 0) {
              ListNode next = head.next;
              head.next = prev;
              prev = head;
              head = next;
              k--;
          }
          return prev;
      }
      }
   ```
   
   