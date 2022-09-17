# 138. <u>Copy</u> List with Random Pointer

给定一个带有`next`和`random`指针的链表，对它进行deep copy。<u>注：deep copy出来的reference不指向原来的，但value一样。shallow copy出来的是指向原来的reference的。</u>`random`指针可以指向链表内部任意一个节点，包括自己或者空。

用一个Map来记录新老链表之间节点的对应关系。从原来的表头出发，一直到最后。

每轮循环定下当前节点的`next`和`random`元素，然后往后走一直到最后。

我们首先检查Map里有没有相应的新节点。有的话，直接用，没有的话再创建。

再看当前节点的`random`是否为空，不为空我们也接着处理`random`。检查Map里有没有对应的节点在新链表里，有的话直接用，没有的话创建然后用。

这样，最后我们就可以把整个链表的给deep copy一下了。

Time complexity: O(N)

Space complexity: O(N)

```java
/**
 * class RandomListNode {
 *   public int value;
 *   public RandomListNode next;
 *   public RandomListNode random;
 *   public RandomListNode(int value) {
 *     this.value = value;
 *   }
 * }
 */
public class Solution {
  public RandomListNode copy(RandomListNode head) {
    // Use the hashmap to aviod copy multiple times for the same node
    if (head == null) {
      return null;
    }
    RandomListNode dummy = new RandomListNode(0);
    RandomListNode cur = dummy;
    //maintain the mapping between the node in the original list and the corresponding node in the new list
    Map<RandomListNode, RandomListNode> map = new HashMap<>();
    while (head != null) {
      if (!map.containsKey(head)) {
        map.put(head, new RandomListNode(head.value));
      }
      //connect the copied node to the deep copy list
      cur.next = map.get(head);
      //copy the random node if necessary
      if (head.random != null) {
        if (!map.containsKey(head.random)) {
          map.put(head.random, new RandomListNode(head.random.value));
        }
        //connect the copied node to the random pointer
        cur.next.random = map.get(head.random);
      }
      head = head.next;
      cur = cur.next;
    }
    return dummy.next;
  }
}
//tc: o(n)
//sc: o(n)
```

A deep copy of an object is **a copy whose properties do not share the same references (point to the same underlying values) as those of the source object from which the copy was made**.