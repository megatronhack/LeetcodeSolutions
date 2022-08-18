# 225. Implement Stack using Queues

用queue来模拟stack的实现。

## One-Queue Approach

省点空间，用一个队列也可以直接模拟。那么这个队列就保持后进来的元素在队头，先进来的元素在队尾的性质就好了。

`push`的时候，先把`x`放入队尾，再把前面所有的元素弹出并重新入队。这样`x`作为后来的元素，成功的到了队头。时间复杂度是O(N)。

`pop`的时候，直接弹出队头的元素就好。

其他操作不变。

```java
class Solution {
    private Queue<Integer> queue;
    /** Initialize your data structure here. */
    public Solution() {
       queue = new ArrayDeque<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        queue.offer(x);
    }

    /** Removes the element on top of the stack and returns that element. */
    public Integer pop() {
        if (queue.isEmpty()){
          return null;
        }
        else{
          int size = queue.size();
          while(--size != 0){
            queue.offer(queue.poll());
          }
        }
        return queue.poll();
    }

    /** Get the top element. */
    public Integer top() {
        if (queue.isEmpty()){
          return null;
        }
        int top = pop();
        queue.offer(top);
        return top;
    }

    /** Returns whether the stack is empty. */
    public boolean isEmpty() {
       return queue.isEmpty();
    }
}
```



