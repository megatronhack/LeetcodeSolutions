## Array

```java
int[] array = new int[array.length];    // array length
int[] max = new int[]{Integer.MIN_VALUE}; // create an array with value  
int[] emptyArray = new int[]{};   // empty array  
Arrays.sort(array);  
Arrays.asList(i,j)  // new array to list  
Arrays.copyOf(myArray,end)// copy an array from index 0 to index end - 1;
    
int[] array = new ArrayList<GraphNode>(map.values()); // create (array with map.values api)
```



## Set 

List,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double 

String[] s ，或者所有array都***不可以***放到Set<String> set = new HashSet<>(s)进行转换。（得用for loop用set一个一个add）

List<String> s **可以**放到Set<String> set = new HashSet<>(s)进行转换

List<TreeNode> nodes **可以**放到  Set<TreeNode> set = new HashSet<TreeNode>(nodes);

```java
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

List,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double . 

list: [1,2,3,4,5]

```java
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

List,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double 

{key:value}

```java
Map<Integer, List<Integer>> map = new HashMap<Integer,List<Integer>>();
HashMap.put()    //key,value together
HashMap.get()    //get value, primitive type double
HashMap.values()     return collections of values
HashMap.containsKey()
HashMap.keySet()  //  create a set out of the key elements
HashMap.getValue()   // get value, a Double object, like Integer wrapper type
HashMap.Entry() //return reference
HashMap.entrySet()  // returns a set view of the map
HashMap.Entry<String, Integer> entry : Hashmap.entrySet()
```



## Integer

```java
Integer.MIN_VALUE;
Integer.MAX_VALUE;
```



## String 

"string"

```java
String s = new String("word");
String s = "hello";   //double quote is string, single is chart
char[] arraySet = s.toCharArray();  // string to char array
s.equals();  // checking actual value
s.indexOf('0'); //return first occurrence index of '0' in the string. 
s.charAt(i)// getting element
s.length();
int matchIndex = s.indexOf("abc", fromIndex); ////returns the position of the first occurrence of "abc" starting "fromIndex" in a string(our case is "s"), returns -1 if the value is not found.

s.toCharArray(); 
String str = String.valueOf(arr);//The method valueOf() will convert the entire char array into a string.//这里的String. 本身就是内置API

s.substring(start,end)  // not include end index  

new String(sourceArray,0,slow) // new a string from source array, start form index 0 to slow-1
```

## Char

```java
char[] array = string.toCharArray();
char[] arrya = new char[];
Character.isLetterOrDigit(ch)//return boolean, check whether the char is a digit or character('0'-'9', 'a'-'z', 'A'-'Z')
Character.toLowerCase(ch)//change the char to lower case
```



## StringBuilder

```java
StringBuilder sb = new StringBuilder();
sb.toString();
sb.length();
sb.deleteCharAt();
sb.deleteCharAt(cur.length() - 1);
sb.append(); 
```



## Deque stack 单向 LIFO

```java
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

```java
Queue<Integer> queue = new ArrayDeque<Integer>();
queue.offer() // add element at the end; like offerLast. 1 2 3, offer 4, becoming 1 2 3 4 // == offerLast
queue.remove() //return and remove the first element when queue is empty, raise exception // == pollFirst
queue.poll() // return and remove the first element.  when queue is empty, returns null.   1 2 3, return 2 3, head is 1 //  = pollFirst
queue.peek() // return value but not remove //peak first
```



## Final API:

```java
private static final char[] PS = new char[]{'(',')','<','>','{','}'};
```



## HEAP or Comparator interface

```java
3 methods:

(1)compare  // compare value of 2 objects  >> belong to comparator/comparable interface
(2)equals //will take any Object as a parameter
(3)compareTo  // compare value of 2 string objects, compareTo will only take Strings. >> belong to comparable interfance
    
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

```

## Priority Queue and Heap

Class比较，比如Integer，用a.equals(b); Value比较，比如int, 用 a == b

```java
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

```java
maxHeap.peek();  //peekFirst
maxHeap.offer();  //depending on your comparator, maxheap is ..  nlogn 
maxHeap.poll();  //pollFirst, nlongn  >>  You can build your heap in O(n), heapSort. Then you pop elements off, one at a time, each taking O(log n) time. This takes O(n log n) time total.
```

```java
//Minheap
PriorityQueue<Map.Entry<String, Integer>> minHeap = new PriorityQueue<>(k, new Comparator<Map.Entry<String, Integer>>(){
 @Override
 public int compare(Map.Entry<String, Integer> e1, Map.Entry<String, Integer> e2){
   return e1.getValue().compareTo(e2.getValue());
 }
});
```



## OTHERS

```java
Collections.reverse(mylist) ;// Reversing an ArrayList, Reversing a LinkedList, Reversing an array.  1 2 3 4 > 4 3 2 1
boolean[][] visited = new boolean[rows][collumn]; //default boolean false
int count = array[i] - '0'; // getting number. exa: int 5 = '5' - '0'  
```

