# 133. Clone Graph

给定一个连通的无向图，把它deep copy一份出来。

## DFS Approach

这题也可以用深度优先搜索，dfs在过程中进行拷贝。

如果没有出现过，那就新建并且把映射关系确定。

但此时这个点并没有完全被复制好，我们还需要把它的邻居也复制好。

所以针对每个邻居，我们进行相同的方法调用，把邻居都复制好。

Time complexity: O(#). # of nodes + # of neighbors

Space complexity: O(#). # of nodes + # of neighbors

```java
public class Solution {
  public List<GraphNode> copy(List<GraphNode> graph) {
    // Write your solution here.
    // Use the DFS method to solve this question
    // Use the HashMap to store the graph ane the neighbors
    // Input is a list of graph node, and the output is the deep copy of the graph node
    //base case
    if (graph == null){
      return null;
    }
   HashMap<GraphNode, GraphNode> map = new HashMap<GraphNode, GraphNode>();
   for (GraphNode node : graph){
    if(!map.containsKey(node)){
       map.put(node, new GraphNode(node.key));
       DFS(node,map);
    }
   }
  //return
   return new ArrayList<GraphNode>(map.values());
  }
  //dfs
  private void DFS(GraphNode seed, HashMap<GraphNode, GraphNode> map){
    GraphNode copy = map.get(seed);
    for (GraphNode nei : seed.neighbors){
      if (!map.containsKey(nei)){
        map.put(nei,new GraphNode(nei.key));
        DFS(nei,map);
      }
      copy.neighbors.add(map.get(nei));
    }
  }
}
// O （ # of graph nodes + # of graph nodes neibors）
// O （ # of graph nodes + # of graph nodes neibors）
```

## BFS Approach

广度优先搜索方法，核心思想是利用广度优先搜索，在搜索的过程中对整张图进行复制。用队列来存放需要复制的节点，用`oldNewMap`来记录新老图里的节点对应关系，以及这个节点有没有被复制过。

每从队头拿出节点处理时，先得到它在新图里对应的节点。但是此时不一定所有的邻居都没被复制过，只有不在`oldNewMap`里的邻居没有被复制过，需要入队进行复制。所以说，如果一个邻居已经在`oldNewMap`里了，那么我们之前获取它在新图对应的节点加进来。否则，就进行复制加入`oldNewMap`，然后该邻居入队等待被复制。

Time complexity: O(N)

Space complexity: O(N)

```
class Solution {
  public Node cloneGraph(Node node) {
    if(node == null){
      return null;
    }
    Map<Node, Node> oldNewMap = new HashMap<>();
    Queue<Node> queue = new ArrayDeque<>();
    queue.offer(node);
    oldNewMap.put(node, new Node(node.val));
    while (!queue.isEmpty()) {
      Node curr = queue.poll();
      Node newCurr = oldNewMap.get(curr);
      for (Node nei : curr.neighbors) {
        if (!oldNewMap.containsKey(nei)) {
          oldNewMap.put(nei, new Node(nei.val));
          queue.offer(nei);
        }
        newCurr.neighbors.add(oldNewMap.get(nei));
      }
    }
    return oldNewMap.get(node);
  }
}
```

