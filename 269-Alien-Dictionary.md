# 269. Alien Dictionary

给定一个按照字典序排序的外星字符数组，求出它字典序。

这题还是拓扑的思路。新建`Vertex`类来记录每个字符以及有多少字符排在它前面`inDegree`，以及哪些字符在它后面`outVertexes`。建立`Map<Character, Vertex> alphabet`来建立字符到对应`Vertex`的映射。

通过对字符串数组遍历来寻找潜在的字典序关系。具体来说就是相邻两个字符串找到首个不同的字符，那么前一个字符串这个位置的字符肯定在字典序上就比后一个字符串这个位置的字符要小，后一个字符的`inDegree`就得+1，前一个字符的`outVertexes`就把后一个字符的vertex加进去。余下的部分的就不用再看了。

接着，我们从所有的字符vertex里找出`inDegree`为0的入队，他们是字典序最小的一批。可能有多个`inDegree`为0的字符，他们之间的顺序我们不一定清楚，但是他们都是有可能的。只有明显的自相矛盾才会导致没有答案，比如`["a", "b", "a"]`。

用一个`cnt`来记录处理多少个字符了，用`ordering`来构建字典序。从队列取出一个字符，加入`ordering`，然后cnt自增。把所有在当前字符的`outVertexes`里的字符节点的`inDegree`全部自减，如果自减之后有0的话就入队。重复该过程知道队列为空。如果`cnt`等于字符总数，也就是`alphabet`的大小，那么就返回`ordering`。否则，就代表没处理完则返回空串。

```java
class Solution {
  public String alienOrder(String[] words) {
    // Step 0: Create data structures and find all unique letters.
    Map<Character, List<Character>> adjList = new HashMap<>();
    Map<Character, Integer> counts = new HashMap<>();
    for (String word : words) {
        for (char c : word.toCharArray()) {
            counts.put(c, 0);
            adjList.put(c, new ArrayList<>());
        }
    }
    
    // Step 1: Find all edges.
    for (int i = 0; i < words.length - 1; i++) {
        String word1 = words[i];
        String word2 = words[i + 1];
        // Check that word2 is not a prefix of word1.
        if (word1.length() > word2.length() && word1.startsWith(word2)) {
            return "";
        }
        // Find the first non match and insert the corresponding relation.
        for (int j = 0; j < Math.min(word1.length(), word2.length()); j++) {
            if (word1.charAt(j) != word2.charAt(j)) {
                adjList.get(word1.charAt(j)).add(word2.charAt(j));
                counts.put(word2.charAt(j), counts.get(word2.charAt(j)) + 1);
                break;
            }
        }
    }
    
    // Step 2: Breadth-first search.
    StringBuilder sb = new StringBuilder();
    Queue<Character> queue = new LinkedList<>();
    for (Character c : counts.keySet()) {
        if (counts.get(c).equals(0)) {
            queue.add(c);
        }
    }
    while (!queue.isEmpty()) {
        Character c = queue.remove();
        sb.append(c);
        for (Character next : adjList.get(c)) {
            counts.put(next, counts.get(next) - 1);
            if (counts.get(next).equals(0)) {
                queue.add(next);
            }
        }
    }
    
    if (sb.length() < counts.size()) {
        return "";
    }
    return sb.toString();
}
}

```