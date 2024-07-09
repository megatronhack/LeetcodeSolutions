# 1429. First Unique Number

和[laicode 288. First Non-Repeating Character In Stream](laicode-288-First-Non-Repeating-Character-In-Stream.md)一样的，只不过这题是先有一些初始化的数据，所以在constructor里先`add`就好。

通过一个hashmap去记录这个integer出现的次数，当出现次数大于1的时候，这个interger就不是unique的，就需要把它poll掉。

```java
class FirstUnique {

  private Deque<Integer> uniqueDeque = new ArrayDeque<>();
  private Map<Integer, Integer> countMap = new HashMap<>();

  public FirstUnique(int[] nums) {
    for (int num : nums) {
        add(num);
    }
  }

  public int showFirstUnique() {
    return uniqueDeque.isEmpty() ? -1 : uniqueDeque.peekFirst();
  }

  public void add(int value) {
    int count = countMap.getOrDefault(value, 0);
    countMap.put(value, ++count);
    if (count == 1) {
      uniqueDeque.offerLast(value);
    } else {
      while (!uniqueDeque.isEmpty() && countMap.get(uniqueDeque.peekFirst()) > 1) {
        uniqueDeque.pollFirst();
      }
    }
  }
}
```

Example:

Input: 
["FirstUnique","showFirstUnique","add","showFirstUnique","add","showFirstUnique","add","showFirstUnique"]
[[[2,3,5]],[],[5],[],[2],[],[3],[]]