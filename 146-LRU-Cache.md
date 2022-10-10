# 146. LRU Cache

实现一个LRU cache。

LRU, least recent used， is a cache replacement policy. 当缓存空间不够的时候，挑出最久没有被访问的缓存项丢弃。

这里我们需要一个双端队列来存放缓存数据，还需要一个Map来快速获取缓存项，`cnt`来记录目前有多少缓存项，以及`capacity`记录缓存的大小。`get`的时候，先检查对应的缓存是否存在。不存在的话，直接按照题意返回`-1`。存在的话，在返回缓存项的值之前，先把缓存项放到队列的头部，表示这个最近刚被访问过过。

`put`的时候，先通过Map来判断给定的`key`是否存在。存在的话，就直接修改对应缓存项的值，并且把缓存项放到队列头部表示刚被访问过。不存在的话，就新建节点然后放入队列头部和Map。如果放入之后，缓存项的数量超过了上限，那么就要从队列尾部弹出一个缓存项丢弃掉，并且从Map里也删去这个缓存项的键值对。

这里双端队列的实现，我们也是手动实现的，因为把队列中的某个元素放到队列头部这个操作需要我们先删掉它，然后把它重新放入头部。java自带的ArrayDeque和LinkedList都会先遍历一遍队列找到对应的元素，会有性能上的损失。我们这里自己实现一个`remove(DLinkedListNode node)`来快速删除。


```java
public class Solution<K, V> {
  // each node contains the key, value pair,
  // and it is also a double linked list node.
  static class Node<K,V> {
    Node<K, V> next;
    Node<K, V> prev;
    K key;
    V value;

   Node(K key, V value) {
    this.key = key;
    this.value = value;
  }
   void update(K key, V value) {
    this.key = key;
    this.value = value;
  }
}

  // make it final for the pre-defined size limit of the cache.
private final int limit;
  // record all the time the head and tail of the double linked list.
private Node<K, V> head;
private Node<K, V> tail;
  // maintains the relationship of key and its corresponding node
  // in the double linked list.
private Map<K, Node<K, V>> map;

  public Solution(int limit) {
    this.limit = limit;
    this.map = new HashMap<K, Node<K, V>>();
  }
  
  public void set(K key, V value) {
    Node<K, V> node = null;
    // 1. if the key already in the cache, we need to update its value
    // and move it to head(most recent position).  
    if (map.containsKey(key)) {
      node = map.get(key);
      node.value = value;
      remove (node);
    }  else if (map.size() < limit) {
     // 2. if the key is not in the cache and we still have space,
     // we can add append a new node to head. 
     node = new Node<K, V>(key, value);    
    } else {
      // 3. if the key is not in the cache and we don't have space,
      // we need to evict the tail and reuse the node let it maintain
      // the new key,value and put it to head.      
      node = tail;
      remove(node);
      node.update(key, value);
    }
    append(node);
  }
  
  public V get(K key) {
    Node<K, V> node = map.get(key);
    if (node == null) {
      return null;
    }
    // even it is a read operation, it is still a write operation to
    // the double linked list, and we need to move the node to head.
    remove(node);
    append(node);
    return node.value;    
  }

  private Node<K, V> remove(Node<K, V> node) {
    map.remove(node.key);
    if (node.prev != null) {
      node.prev.next = node.next;
    }
    if (node.next != null) {
      node.next.prev = node.prev;
    }
    if (node == head) {
      head = head.next;
    }
    if (node == tail) {
      tail = tail.prev;
    }
    node.next = node.prev = null;
    return node;
  }

  private Node<K, V> append(Node<K, V> node) {
    map.put(node.key, node);
    if (head == null) {
      head = tail = node;
    } else {
      node.next = head;
      head.prev = node;
      head = node;
    }
    return node;
  }
}

//tc: O(1) for all operations
```