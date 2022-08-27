## Array

```
int[] array = new int[array.length];    // array length
int[] max = new int[]{Integer.MIN_VALUE}; // create an array with value  
int[] emptyArray = new int[]{};   // empty array  
Arrays.sort(array);  
Arrays.asList(i,j)  // new array to list  
```



## Set 

List,map,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double 

```
set.contains()  
set.add()  
Set<Integer> set = new HashSet<Integer>();  
set.toCharArray();  // string set                 
Set<String> set = new HashSet<>();     
set.contains();  
set.remove(); 
```



## KnaryTreeNode



## List

List,map,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double 

```
List<GraphNode>
List<List<Integer>> result = new ArrayList<List<Integer>>();
List<String> result =  new ArrayList<String>();
list.isEmpty();
list.remove(index);
list.subList(size, cur.size()).clear(); //题目404
list.size()   // 大小
list.get(i)  //取数
list.add(array[i]);   //add在尾巴后
list.get(i).add(array[i])  // index 为i的位置，insert the element
List<ListNode>   // 有指针
ListNode dummy = new ListNode(0);
```



## HashMap

List,map,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double 

```
Map<Integer, List<Integer>> map = new HashMap<Integer,List<Integer>>();
HashMap.put()    //key,value together
HashMap.get()    //get value
HashMap.values()     return collections of values
HashMap.containsKey()
HashMap.keySet()  //  create a set out of the key elements
```



## Integer

```
Integer.MIN_VALUE;
Integer.MAX_VALUE;
```



## String 

```
String s = new String("word");
String s = "hello";   //double quote is string, single is chart
char[] arraySet = s.toCharArray();  // string to char array
s.equals();  // checking actual value
s.indexOf('0'); //return first occurrence index of '0' in the string. 

int matchIndex = s.indexOf("0", fromIndex); ////returns the position of the first occurrence of a 
//value starting "fromIndex" in a string, returns -1 if the value is not found.

s.toCharArray(); 
String str = String.valueOf(arr);//The method valueOf() will convert the entire char array into a string.
//这里的String. 本身就是内置API

s.length();
s.substring(start,end)  // not include end index  

int matchIndex = input.indexOf(s, fromIndex); //Check if there exists a substring same as s in the substring of input starting at fromIndex.


StringBuilder sb = new StringBuilder();
sb.toString();
sb.length();
sb.deleteCharAt();
sb.deleteCharAt(cur.length() - 1);
sb.append(); 
```



## Char

```
Character.isLetterOrDigit(ch)//return boolean, check whether the char is a digit or character('0'-'9', 'a'-'z', 'A'-'Z')
Character.toLowerCase(ch)//change the char to lower case
```



## Deque stack 单向 LIFO

```
Deque<Character> stack = new LinkedList<Character>();
Deque<Character> stack = new ArrayDeque<Character>();
stack.push();   // to left side add, = offerFirst();
stack.pop();    // the left side pop = pollFirst();
stack.offerFirst();
stack.pollFirst()
stack.offerLast();
stack.pollLast()
stack.add; // addlast
```



## Queue:FIFO

```
Queue<Integer> queue = new ArrayDeque<Integer>();
queue.offer() // add element at the end; like offerLast. 1 2 3, offer 4, becoming 1 2 3 4
queue.remove() //return and remove the first element when queue is empty, raise exception
queue.poll() // return and remove the first element.  when queue is empty, returns null.   1 2 3, return 2 3, head is 1
queue.peek() // return value but not remove
```



## Final API:

```
private static final char[] PS = new char[]{'(',')','<','>','{','}'};
```



## HEAP Or Comparator interface

```
2 methods:

(1)compare  (2)equals

(1)compare
  static class MyComparator implements Comparator<Entry>{
     @Override
     public int compare(Entry e1, Entry r2) {
          if (e1.value == e2.value){
             return 0;
          }
     return e1.value < e2.value ? -1 : 1;       
     }
  }

Comparable interface
1 method:(1)compareTo
```

```
//use a maxheap to store the k smallest elements
PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(k, new Comparator<Integer>(){
  @Override
  public int compare(Integer a, Integer b){
    if (a.equals(b)){
      return 0;
    } 
    return a > b ? -1 : 1;
    }
});
```

## Priority Queue

```
maxHeap.peek();  //peekFirst
maxHeap.offer();  //depending on your comparator, maxheap is ..
maxHeap.poll();  //pollFirst
```



## OTHERS

```java
Collections.reverse(mylist) ;// Reversing an ArrayList, Reversing a LinkedList, Reversing an array.  1 2 3 4 > 4 3 2 1
boolean[][] visited = new boolean[rows][collumn]; //default boolean false
```

