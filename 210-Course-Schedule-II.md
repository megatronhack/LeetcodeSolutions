# 210. Course Schedule II

和[207. Course Schedule](207-Course-Schedule.md)类似，但是这里如果可以完成的话要给出具体的完成顺序。

Clarification:
+ 不能上完就返回空数组
+ 不存在自依赖
+ 给的依赖关系都是合理的，不存在超出`numCourses`情况

其实区别不大，我们只要用一个额外的数组`ordering`记录下顺序就好。`taken`每次自增之前，先把当前的课程写入`ordering`对应的位置。最后如果上完了的话，就返回`ordering`，没上完就返回空数组。

```java
public class Solution {
  public int[] findOrder(int numCourses, int[][] prerequisites) {
// the adjacency list representation of prerequisites
  List<List<Integer>> graph = new ArrayList<>(numCourses);
  for (int i = 0; i < numCourses; i++) {
    graph.add(new ArrayList<>());
  }
  for (int[] dependency : prerequisites) {
    int x = dependency[0];
    int y = dependency[1];
    graph.get(y).add(x);  //[[1, 2], [3], [3], []]
  }
  return topologicalSort(graph);
  }

  private int[] topologicalSort(List<List<Integer>> graph) {
    int numCourses = graph.size();
    int[] topologicalOrder = new int[numCourses];
    int[] incomingEdges = new int[numCourses];
    // how many edges are pointing to itself
    for (int x = 0; x < numCourses; x++) {
      for (int y : graph.get(x)) {
        incomingEdges[y]++;
      }//[0, 1, 1, 2]
    }
    //nodes with no incoming edges
    Queue<Integer> queue = new ArrayDeque<>();
    for (int x = 0; x < numCourses; x++) {
      if (incomingEdges[x] == 0) {
        queue.offer(x);
      }
    }
    int numExpanded = 0;
    while (!queue.isEmpty()) {
      int x = queue.poll();
      topologicalOrder[numExpanded++] = x;
      for (int y : graph.get(x)) {
        if (--incomingEdges[y] == 0) {
          queue.offer(y);
        }
      }
    }
    return numExpanded == numCourses ? topologicalOrder : new int[]{};
  }
}
//time:O(v+e)
//space: O(v+e)

```

For example:

```
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is `[0,1]`

```
4, [[1,0],[2,0],[3,1],[3,2]]
```

There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is `[0,1,2,3]`. Another correct ordering is`[0,2,1,3]`.