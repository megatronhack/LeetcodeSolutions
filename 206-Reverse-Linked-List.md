```
206. Reverse Linked List
Given the head of a singly linked list, reverse the list, and return the reversed list.

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

//method1 iterative: 

记录前面的element，换方向 

// keep changing direction of newst element to previously elements

//Time On;  Space O1;

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        //Traverse the node by using three pointers
        ListNode prev = null;
        ListNode cur = head;
        if (head == null || head.next == null) return head;
        ListNode next = head.next;
        while(cur != null) {
            next = cur.next;
            cur.next = prev;
            prev = cur;

            cur = next;

        }
        return prev;
    }
}
```

//Method 2: recusion

basecase会让newHead在5停下，就不会继续run下去。然后返回上个function当head是4的时候，才会跑下面的body

// for example 1 -2 -3 -4 - 5

// base case will make newHead stop at 5, but it won't run body. 

//Then return to last recursive function where head is 4 and run the body since;

```
public ListNode reverseList(ListNode head) {
//recursion
//basecase, newhead should be stopped at the last element
if (head == null || head.next == null){
    return head;
}
//Body    
ListNode newHead = reverseList(head.next); 
head.next.next = head; //change direction
head.next = null; //delink

return newHead;
}
```

Python version:

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        cur = head
        while cur is not None:
            next = cur.next
            cur.next = prev
            prev = cur
            cur = next
        return prev
```

