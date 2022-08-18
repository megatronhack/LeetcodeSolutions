# 155. Min Stack

```
Enhance the stack implementation to support min() operation. min() should return the current minimum value in the stack. If the stack is empty, min() should return -1.

push(int element) - push the element to top
pop() - return the top element and remove it, if the stack is empty, return -1
top() - return the top element without remove it, if the stack is empty, return -1
min() - return the current min value in the stack.
```

用2个stack。一个正常的stack，一个minStack用来记录最小值。

## Two Stack Approach

```java
public class Solution {
  ArrayDeque<Integer> stack;
  ArrayDeque<Integer> minStack;
  public Solution() {
    // write your solution here
    stack = new ArrayDeque<>();
    minStack = new ArrayDeque<>();
  }
  public void push(int element) {
    stack.offerFirst(element);
    //when value <= currentMin value in stack need to push the value to minstack
    if (minStack.isEmpty() || element <= minStack.peekFirst()){
      minStack.offerFirst(element);
    }
  }
  public int min(){
     if (minStack.isEmpty()){
       return -1;
     }
     return minStack.peekFirst();
   }

  public int pop() {
    //corner case
    if (stack.isEmpty()){
      return - 1;
    }
    else{
      Integer result =  stack.pollFirst();
      //when the popped value is the same as top value of minStack, 
      //the value need to be popped from minStack as well
      if (minStack.peekFirst().equals(result)){
        minStack.pollFirst();
      }
    return result;
    }
  }
  public int top() {
    if (stack.isEmpty()){
         return -1;
    }
    return stack.peekFirst();
  }
}
```



