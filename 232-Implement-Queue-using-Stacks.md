用栈来模拟实现一个队列。

这里我们需要两个栈，一个in，一个out。`in`专门用来存放新进来的元素，`out`专门存放准备出去的元素。

当`push`的时候，新进来的元素直接压入`in`栈。当`pop`的时候，要出去的元素从`out`弹出。但是如果`out`为空的话，那么就把`in`的所有元素依次弹出并压入`out`。那么原来在`in`栈顶的，现在就到了`out`的栈底，正好符合了队列先入先出的性质。再把`out`弹出元素，就实现了`pop`操作。

`peek`操作也就是看`out`的栈顶，如果`out`为空的话，继续把`in`的元素挪过来。`empty`的话就看是不是两个栈都是空。

```
public class Solution {
  Deque<Integer> in;
  Deque<Integer> out;
  public Solution() {
    // Write your solution here.
    in = new LinkedList<Integer>();
    out = new LinkedList<Integer>();
  }
  
  public Integer poll() {
    move();
    if (out.isEmpty()){
      return null;
    } else {
      return out.pollFirst();
    }
  
  }
  
  public void offer(int element) {
    in.offerFirst(element);
    
  }
  
  public Integer peek() {
    move();
    if (out.isEmpty()){
      return null;
    } else {
      return out.peekFirst();
    }
  }
  
  public int size() {
   return in.size() + out.size();
  }
  
  public boolean isEmpty() {
    return in.size() == 0 && out.size() == 0;
  }

  public void move(){
    if (out.isEmpty()){
      while (!in.isEmpty()){
        out.offerFirst(in.pollFirst());
      }
    }
  }

}
```

