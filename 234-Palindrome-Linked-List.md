```
Given a linked list, check whether it is a palindrome.

Examples:

Input:   1 -> 2 -> 3 -> 2 -> 1 -> null

output: true.

Input:   1 -> 2 -> 3 -> null  

output: false.

Requirements:

Space complexity must be O(1)
```

检查是否是前后的回文。

切两半，第二半倒转。  例子： 1-2-3-4- 4-2-1；  分成 1 2 3 4 和 4 - 2  -1， 第二半倒转成 1 - 2 -4

比较 1- 2 -3 -4 和 1 - 2 - 4。

如果发现有任何不一样的，return false；否则的话，return true;

  // cut the list from mid node into two list

  // reverse the second list

  // compare one by one of two lists

  // check if euqal, if we found anything that are different, we return false, which means its not palindrome;

 // otherise, we return true;

  // time On

  // space o1

```
public boolean isPalindrome(ListNode head) {
    // Write your solution here
    //corner case
    if (head == null || head.next == null){
      return true;
    }

    ListNode midNode = findMid(head); //find mid node
    ListNode sec = midNode.next;  // create the second list
    midNode.next = null; //delink first and second list
    ListNode reversedSec = reverse(sec); //reverse the second list
    return compare(head,reversedSec);
  }
  // check if euqal, if we found anything that are different, we return false, which means its not palindrome
  public boolean compare(ListNode one, ListNode two){
     while(one != null && two != null){
       if(one.value != two.value){
       return false;
       }
       one = one.next;
       two = two.next;
     }
    return true;
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
```

