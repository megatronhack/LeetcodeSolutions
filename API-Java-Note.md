## Array

```java
int[] array = new int[array.length];    // array length
int[] max = new int[]{Integer.MIN_VALUE}; // create an array with value  
int[] emptyArray = new int[]{};   // empty array  
Arrays.sort(array);  //void return
Arrays.equals(a, b); 
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
set<String> set = new HashSet<>();
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
List<GraphNode> result = new ArrayList<GraphNode>();
List<List<Integer>> result = new ArrayList<List<Integer>>();
List<String> result =  new ArrayList<String>();
list.isEmpty();
list.remove(index);
list.remove(Integer.valueOf(1));//remove by value
list.subList(size, cur.size()).clear(); // arrlist.subList(2, 4); [A, B, C, D, E] >> [C, D]
list.size()   // 大小
list.get(i)  //取数
list.add(array[i]);   //add在尾巴后
list.get(i).add(array[i])  // index 为i的位置，insert the element
List<ListNode>   // 有指针
list.add(new ArrayList<Integer>(cur));//add a list in the List<List<>>();
List<E> copy = new ArrayList<>(list);//Copy a list
ListNode dummy = new ListNode(0);
```



## HashMap

List,map,set的data structure都不能是primitive: boolean , byte , char , short , int , long , float and double 

{key:value}

```java
Map<Integer, List<Integer>> map = new HashMap<Integer,List<Integer>>();
HashMap.put(key,)    //key,value together. This method returns returns previous value associated with the key if present, else return -1.
HashMap.get()    //get value, primitive type double
        V value = map.getOrDefault(key, defaultValue);  
HashMap.getValue()   // get value, a Double object, like Integer wrapper type
HashMap.containsKey() ////return boolean
HashMap.keySet()  //  create a set out of the key elements
HashMap.values()  // return collections of values, like new ArrayList<E>(map.values())
    List<List<Integer>> result = new ArrayList<List<Intege>>(map.values());
HashMap.Entry() //return reference
HashMap.entrySet()  // returns a set view of the map
HashMap.Entry<String, Integer> entry : Hashmap.entrySet()
    //for (Map.Entry<String, String> entry : map.entrySet()) {
    //System.out.println(entry.getKey() + "/" + entry.getValue());
    //}
//On Java 10+:
for (var entry : map.entrySet()) {
    System.out.println(entry.getKey() + "/" + entry.getValue());
}
map.remove(key)//remove the element by using the key in map
graph.computeIfAbsent(a, val -> new ArrayList<Integer>()).add(b);
//For each vertex a, computeIfAbsent checks if a is already a key in graph.
//If a is not present, it initializes a with a new ArrayList (this happens only the first time a is //encountered).
//Then, it returns the list associated with a (whether newly created or already existing), and //the edge b is added to this list.

    
```

## HashSet

```java
Set<E> set = new HashSet<>();
```

```java
int count = HashMap.getOrDefault(key, 0);// mapped with specified key. If no value is mapped with the provided key then the default value is returned. // we "set" 0 to default value
HashMap.put(key, ++count);
```

```java
int count = HashMap.getOrDefault(key, 0);// mapped with specified key. If no value is mapped with the provided key then the default value is returned. // we "set" 0 to default value
HashMap.put(key, ++count);
set.remove(s.charAt(i));//remove an element fro
```



## Integer

```java
Integer.MIN_VALUE;
Integer.MAX_VALUE;
Integer.valueOf(str); //to Convert a String to an Integer
Integer.toString(number).toCharArray()//convert an integer to char array
int number = Integer.parseInt(string);//parseInt() The parseInt() function parses a string argument and returns an integer of the specified radix
int a = Integer.parseInt(str);//parse a str to an int
double digit2 = Double.parseDouble(rateStr[0]);//parse a str to double
```



## String 

```java
String s = new String("word");
String s = "hello";   //double quote is string, single is chart
char[] arraySet = s.toCharArray();  // string to char array

s.equals();  // checking actual value
s.indexOf('0'); //return first occurrence index of '0' in the string. returns -1 if the value is not found. 
s.charAt(i)// getting element
s.length();
int matchIndex = s.indexOf("abc", fromIndex); ////returns the position of the first occurrence of "abc" starting "fromIndex" in a string(our case is "s"), returns -1 if the value is not found.
start = str.lastIndexOf("(");//return the last index of "(", return -1 if not found
String str = String.valueOf(arr);//The method valueOf() will convert the entire char array into a string.//这里的String. 本身就是内置API

char[] array = String.valueOf(n).toCharArray();//convert an int to char array
String string = String.valueOf(charArray);
//When you want to convert a character array to a String, you should always use String.valueOf(charArray) or the String constructor like new String(charArray). If you mistakenly use charArray.toString(), you will not get the content of the array as a string, but a string that represents the array object's reference in memory.
s.substring(start,end)  // not include end index  
s.substring(startIndex)  // from startindex to end  
new String(sourceArray,0,slow) // new a string from source array, start form index 0 to slow-1
s+= Integer.toString(root.key)//how to append in the string
s.replaceAll(".", "*")//Replace all symbol with *. The dot symbol can take place of any other symbol, that is why it is called the wildcard character.
s.split("[.]")//split the string with "." and return as an array
Integer.valueOf(s);//Convert a String to an Integer
String(inputString.chars().map(x -> (x - 'a' + 1) % 26 + 'a').toArray(), 0, inputString.length());
//1. str.chsrs():In Java 8, there is a new method String.chars() which returns a stream of ints (IntStream) that represent the character codes.
//2. toArray() :toArray() method of Chars Class is used to convert the char values, passed as the parameter to this method, into a Char Array.
String result = String.join("-", "2024", "06", "06");
String result = String.join(", ", list/array);//You can also use the join() method with a List or any other Iterable of CharSequence 

```

## Char

```java
char[] array = string.toCharArray();
char[] arrya = new char[];
char[] array = set.toCharArray(); //String set也可以
Character.isLetterOrDigit(ch)//return boolean, check whether the char is a digit or character('0'-'9', 'a'-'z', 'A'-'Z')
Character.toLowerCase(ch)//change the char to lower case
```



## StringBuilder

```java
StringBuilder sb = new StringBuilder();
sb.toString();
sb.length();
sb.deleteCharAt();
sb.setCharAt(index, value);
sb.deleteCharAt(cur.length() - 1);
sb.append(); 
sb.reverse().toString();//reverse the sb, then turn it into a string
sb.inser(int position, target)//position is the index in string where we need to insert.
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

By default, the priority queue in Java is **min Priority queue with natural ordering**. To make it max, we have to use a custom comparator so that head of the queue returns the greatest element in the queue.

```Java
PriorityQueue<Integer> minHeap = new PriorityQueue<>(); 

Java15: MaxHeap
PriorityQueue<Integer> pq = new PriorityQueue(Collections.reverseOrder());

PriorityQueue<Integer> maxHeap= new PriorityQueue<Integer>(k, new Comparator<Integer>() {   
    @Override   
    public int compare(Integer i, Integer j){    
        if (i.equals(j)){     
            return 0;    
        }    
        return i < j ? 1 : -1;   
    }  
});
```

```java
Comparator interface: 2 methods:(1)compare  (2)equals
(1)compare  // compare value of 2 objects  >> belong to comparator/comparable interface

  static class MyComparator implements Comparator<Entry>{
     @Override
     public int compare(Entry e1, Entry r2) {
          if (e1.value == e2.value){
             return 0;
          }
     return e1.value < e2.value ? -1 : 1;       
     }
  }

(2)equals //will take any Object as a parameter

Comparable interface: 1 method:(1)compareTo

(1) compareTo  // compare value of 2 string objects, compareTo will only take Strings. >> belong to comparable interfance

```

compare 和 compareTo的用法

```java
int cmp = Integer.compare(l1.get(i), l2.get(j)); //return 0 or -1 or 1
int compare = a.get(i).compareTo(b.get(j)); //return 0 or -1 or 1
```

## Priority Queue and HEAP

Class比较，比如Integer，用a.equals(b); 

Value比较，比如int, 用 a == b

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

**MaxHeap**

```java
maxHeap.peek();  //peekFirst
maxHeap.offer();  //depending on your comparator, maxheap is ..  nlogn 
maxHeap.poll();  //pollFirst, nlongn  >>  You can build your heap in O(n), heapSort. Then you pop elements off, one at a time, each taking O(log n) time. This takes O(n log n) time total.
```

**MinHeap**

```java

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
