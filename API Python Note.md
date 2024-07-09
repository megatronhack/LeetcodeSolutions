## Array

```python
len(array)    ##  array length  ps:如果local var定义了个len,会和Built in len冲突
array = [1,2,3] ##  create an array with value  
array = []     ## empty array  
array.append(1) ##  add
array.sort(array);  
array.copf(myArray,end)##  copy an array from index 0 to index end - 1;
    
list(array) ## Create an array from the values of a
```



## Set 

```py
my_set = set() ## my_set  = {}  # This creates an empty dictionary, not a set
my_set = {1, 2, 3}  ## my_set with element 1 2 3
my_set.add(4
my_set.remove(4)       
print("a" in my_string_set)  # Output: True ## Check if a set contains an element (Same as above).
      
string_set = {"hello", "world"}       
Example 1: Converting each string to a list of characters   
char_array = [char for word in string_set for char in word] # Convert each string in the set to a list of characters         
Example 2: Concatenating all strings and then converting to a list of characters
concatenated_string = "".join(string_set) # Concatenate all strings in the set into a single string
char_array = list(concatenated_string)  # Convert the concatenated string to a list of characters          
print(char_array)  # Output: ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
```



## KnaryTreeNode



## List

```python
my_list = [1, 2, 3, 4, 5]
is_empty = len(my_list) == 0
print(is_empty)  # Output: False
 
my_list.append(6)  ## add   
del my_list[index] ## delete
del my_list[2:]  ## like java sublist. here delete from index to end
len(my_list) ## length, size
mylist.reverse() ## [5,4,3,2,1]
my_list[i] ## same as java list.get(i)


mylist[::-1] ## [5,4,3,2,1] slicing, sequence[start:stop:step], : means you want the whole list. The -1 is the step size, which means you want to step backwards through the list, effectively reversing it.
```



## HashMap

{key:value}

```python
key = 1
value = [1, 2, 3]  or {'key1': 'value1', 'key2': 2, 3: 'value3'}
map[key] = value
print(map)  # Output: {1: [1, 2, 3]} or {'key1': 'value1', 'key2': 2, 3: 'value3'}

map.get(key) ## get value
map.values() ## return collections of values
if 'key' in map: ## hashMap.containsKey()
    
map.keys()  ## HashMap.keySet()   create a set out of the key elements
print(map.keys()) ## a view object here output :dict_keys(['key1', 'key2', 3]), can be accessed with for key in map.keys().   but easier to conver to List as: list(map.keys())

for k, v in map.items(): ## HashMap.Entry() iterating over items
map.items() # HashMap.entrySet() returns a set view of the map. map.items() returns a view object that displays a list of (key, value) tuples.  output: print(my_dict.items()):  dict_items([('key1', 'value1'), ('key2', 2), (3, 'value3')])
```



## Integer

```java
Integer.MIN_VALUE;
Integer.MAX_VALUE;
```



## String 

"string"

```python
s = "hello"
array = list(s)  ## string to char array  # Output: ['h', 'e', 'l', 'l', 'o']
string 1 == string 2;  // ## checking actual value
s.find('o'); ## ## Output: 4
s[i] ## s.charAt(i) getting element
len(s)  ## same as java s.length()
match_index = s.find("abc", from_index) ## returns the position of the first occurrence of "llo", returns -1 if the value is not found.

charArray = list(s) ## java s.toCharArray();  # Output: ['h', 'e', 'l', 'l', 'o']
str_value = ''.join(charArray)  ## Output: "hello"  .  similar to String str = String.valueOf(arr); //The method valueOf() will convert the entire char array into a string.//这里的String. 本身就是内置API

start = 1   end = 4   substring = s[start:end]   print(substring)  # Output: "ell" . java s.substring(start,end) not include end index  

source_array = ['h', 'e', 'l', 'l', 'o']
length = 3
new_string = ''.join(source_array[:length])
#  print(new_string)  # Output: "hel".  in java  new String(sourceArray,0,slow) // new a string from source array, start form index 0 to slow-1
```

## Char

```python
ch = 'a'
ch.isalnum() ## java Character.isLetterOrDigit(ch)//return boolean, check whether the char is a digit or character('0'-'9', 'a'-'z', 'A'-'Z')
ch.lower() ## java Character.toLowerCase(ch)//change the char to lower case
ch.upper()
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
// if only using a list, similar but not that many apis
stack = []
stack.appened();   // to left side add, = offerFirst();
stack.pop();    // the left side pop = pollFirst();

// deque stack
from collections import deque
stack = deque()   
stack.appendleft(4)  // java stack.offerFirst();
stack.append(4) // append right
    
stack.popleft()  // # Remove from the left side
stack.pop()   // remove right
```



## Queue:FIFO

```java

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

```python
array = ['5', '3', '2']
i = 0
count = int(array[i]) - int('0')
print(count)  # Output: 5
```

