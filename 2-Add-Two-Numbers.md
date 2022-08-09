```
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.  

Example

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8

```

2个list，反着给的，output也是反着的。

创建一个value，将list 1和list 2的值相加。

结尾的时候value/10变回原来的值，loop。

loop的条件value != 0 注意：在结尾val = val / val = 10后， 因为比如6 + 4的话结果是0， 需要再跑一遍，得出 0 - 1

 // Dummy List

 // adding list 1 and list 2 element value one by onethrough variable "value"

  //Time On 

  //sapce o1



```java
  public ListNode addTwoNumbers(ListNode one, ListNode two) {
    // Write your solution here
    
    ListNode dummy = new ListNode(0);
    ListNode cur = dummy;
    int val = 0;
    // while value != 0 is for, example two list 6 + 4 = 10 ; value = 10/10 = 1; 
    // run loop again; output would be   0 - 1 
    while(one != null || two != null || val != 0){
        if (one != null){
          val += one.value;
          one = one.next;
        }
        if(two != null){
          val += two.value;
          two = two.next;
        }
        cur.next = new ListNode(val % 10); //
        cur = cur.next;
        // for example, 5/10 = 0; 10 / 10 = 1;  12/10 = 1;  22/10 = 2; 
        val = val / 10;
    }
    return dummy.next;

  }
```

