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

    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        while(cur != null){
            ListNode next = cur.next; // recording next element
            cur.next = prev;  //change direction
            prev = cur; // update prev to cur for next time direction change use
            cur = next; //cur move to newst place
        }
    return prev; // prev will be at the last element
    }

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

