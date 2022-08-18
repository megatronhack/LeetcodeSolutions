```
280. Sort With 2 Stacks
Given an array that is initially stored in one stack, sort it with one additional stacks (total 2 stacks).

After sorting the original stack should contain the sorted integers and from top to bottom the integers are sorted in ascending order.

Assumptions:
The given stack is not null.
There can be duplicated numbers in the give stack.

Requirements:
No additional memory, time complexity = O(n ^ 2).
```

给个unsorted的input stack，用另一个buffer stack，想办法把input stack变成sorted的。

1 和 2 stack， 记录最小值，1-2来回导。 2导1的时候，每次导的时候只到比当前状况localMin大的元素。 这样最后2的元素都会sorted。

思路是selection sort

（1）将input stack的元素loop一边，找最小元素，放到buffer stack。  Example: input 3 1 2 1 5 ， 最小是 1。   

（2）只把buffer stack里面比最小元素的大的元素放回input stack。  Example： buffer 5 1 2 1 3，放过去，input 变成 3  2  5

（3） loop，最后buffer里的元素将会是从小到大。 

 //selection sort like , select + sort
  //1: 2 stacks,  1 unsorted + 1 for buffer
  //2: record LocalMin when moving elemtns between 2 stacks
  //3: push only elements bigger than localMin back to input stack from buffer stack, leaving localMin at buffer
  //4: loop, everythime we are leaving localMin at buffers, until last moment, we push everything back to input stack(become sorted). 

Time complexity: O(N^2)

Space complexity: O(N). We need an extra stack.

```
public void sort(LinkedList<Integer> s1) {
    LinkedList<Integer> s2 = new LinkedList<Integer>();
    //  3 5 1  4 2----------------   1 2 3 4 5
    // Write your solution here.
    sort(s1,s2);
  }

  private void sort (Deque<Integer> input, Deque<Integer> buffer){
      while(!input.isEmpty()){
        int localMin = Integer.MAX_VALUE;
        int count = 0;
          //(1) record localMin
        while(!input.isEmpty()){
            int value = input.pollFirst();
            if ( value < localMin){
              localMin = value;
              count = 1;
            }
            else if (value == localMin){
              count++;
            }
            // push to buffer stack till input stack is empty;
            buffer.offerFirst(value);
        } 
         //(2) push back to input stack from buffer stack with elements bigger than localMin
         // only elements thats bigger than localMin
          while(!buffer.isEmpty() && buffer.peekFirst() >= localMin){
             int value = buffer.pollFirst();
             if (value != localMin){
               input.offerFirst(value);
             }
          }           
          //(3)  // push localMin to buffer, buffer need to have localMin everytime
          while(count-- > 0){
             buffer.offerFirst(localMin);
          }
    }
   // push everything back to input stack like 5 4 3 2 1 to  1 2 3 4 5 
   while(!buffer.isEmpty()){
         int value = buffer.pollFirst();
         input.offerFirst(value);
    }
  }
```

