# 149. Max Points on a Line

给出一堆点的坐标，求出最大共线的点数。

这题我只能想到用暴力的枚举方法了，双重for循环遍历每个点和其他点的搭配。但是呢，给定的点里会有一些特殊情况比如重复，或者横坐标相等，这些都需要考虑好。

所以给定一个点，遍历剩余点的时候要记录好重复点数，横坐标相同点数以及斜线上不同斜率对应的点数。因为斜率不一定是正数，double可能会丢失精度，所以我们用字符串记录斜率的分数形式来表示斜率。这就要求该分数一定得是不可再分，不然`1/1`和`2/2`本质上是同一个斜率但会被纳入不同的斜率。把横坐标差和纵坐标差除以他们的最大公约数就可以约分得到最简分数。（艹，我竟然还记得约分和最简分数这些概念。。。）

内层循环结束之后，我们就可以得到与当前点重复的点数，同x轴的点数，正常斜率的直线里最多的共线点数。他们三个里面取最大值加一，就是这个点对应的最大共线点数。用他来试图更新答案即可。

需要注意的是，当题目给定的点数不足3个时，我们直接返回给的点数就行了。

Time complexity: O(n^2)

Space complexity: O(n) because of the hash map.

```java
public class Solution {
  public int most(Point[] points) {
    // Assumptions: points is not null, and points.length >= 2.
    // record the maximum number of points on the same line.
    int result = 0;
    // we use each pair of points to form a line.
    for (int i = 0; i < points.length; i++) {
      Point seed = points[i];
      // any line can be represented by a point and a slope.
      // we take the point as seed and try to find all possible slopes.
      int same = 1;// record the points with same <x,y>.
      int sameX = 0; // record the points with same x, for the special case of infinite slope.
      int most = 0;
      // record the maximum number of points on the same line
      // crossing the seed point.      
      HashMap<Double, Integer> cnt = new HashMap<Double, Integer>();
      //a map with all possible slopes
      for (int j = 0; j < points.length; j++) {
        if (i == j) {
          continue;
        }
        Point tmp = points[j];
        if (tmp.x == seed.x && tmp.y == seed.y) {
          same++;
          //handle the points with same <x, y>
        } else if (tmp.x == seed.x) {
          sameX++;
          //handle the points with same x
        } else {
          //otherwise just calculate the slope and increment the counter for the calculated clope
          double slope = ((tmp.y - seed.y) + 0.0) / (tmp.x - seed.x);
          if (!cnt.containsKey(slope)) {
            cnt.put(slope, 1);
          } else {
            cnt.put(slope, cnt.get(slope) + 1);
          }
          most = Math.max(most, cnt.get(slope));
        }
      }
      most = Math.max(most, sameX) + same;
      result = Math.max(result, most);
    }
    return result;
  }
}
//tc: O(n^2)
//sc: O(n)
```

**Examples**

- <0, 0>, <1, 1>, <2, 3>, <3, 3>, the maximum number of points on a line is 3(<0, 0>, <1, 1>, <3, 3> are on the same line)