# 84. Largest Rectangle in Histogram

给定一个柱状图，求出里面最大的矩形面积。

直观上来说，为了求出这个柱状图里最大的矩形面积，我们需要遍历每一个柱形然后向左向右找到比自己矮的柱形作为边界来求出面积。这样子，我们最后需要O(n^2)的复杂度可以求出其中最大的矩形。

有没有更好的思路呢？想想看，我们在向左向右寻找比自己矮的柱形时，这个步骤可以被优化一下。我们用一个栈来存储横轴坐标，然后从左向右遍历横轴坐标，每次都要把当前的坐标压栈。但是呢，我们要维护一个性质，栈内自栈底到栈顶的所有坐标对应的柱形是呈严格升序的，没有重复高度。这样做有什么好处呢？这样子，每当被较矮的柱形截断时，我们可以及时计算好之前部分里面的最大矩形。

如何计算之前部分里最大矩形？不断地取栈顶坐标和当前坐标比。如果当前柱形不比栈顶坐标对应的柱形高的话，那么我们就需要弹出栈顶坐标并且计算以这个柱形为“中心”的最大矩形面积。我给“中心”打上引号，因为这个柱形并不一定真的是它对应矩形的正中间。该矩形左边界在哪儿？弹出后新的栈顶坐标就是左边界，因为栈顶坐标对应的柱形肯定比它矮。右边界在哪儿？右边界就是当前柱形，因为当前柱形也不比这个柱形高。所以以这个柱形为“中心”的最大矩形的宽就可以通过`i - stack.peek() - 1`计算出来了。

那如果当前柱形等于栈顶柱形咋办？宽度不就少算了么？不担心，当前坐标入栈之后，以后肯定还会把它弹出来然后计算以它为中心的最大矩形面积的，到时候不就算出来了。

栈内先放个-1来初始化左边界。需要注意的是，遍历完柱形图之后如果栈里面还有多余元素的话，我们还要接着重复弹出并计算的过程。

Time complexity: O(n) because each index only get pushed and poped once.

Space complexity: O(n).

```java
public class Solution {
  public int largest(int[] array) {
    // Assumptions: array is not null, array.length >= 1,
    // all the values in the array are non-negative.
    int result = 0;
    Deque<Integer> stack = new LinkedList<>();
    for (int i = 0; i <= array.length; i++) {
      int cur = i == array.length ? 0 : array[i];
      while (!stack.isEmpty() && array[stack.peekFirst()] >= cur) {
        int height = array[stack.pollFirst()];
        // determine the left boundary of the largest rectangle
        // with height array[i].       
        int left = stack.isEmpty() ? 0 : stack.peekFirst() + 1;
        // determine the right boundary of the largest rectangle
        // with height of the popped element.
        result = Math.max(result, height * (i - left));        
      }
      stack.offerFirst(i);
    }
    return result;
  }
}

//tc: O(n)
//sc: O(n)

```

- { 2, 1, **3, 3, 4** }, the largest rectangle area is 3 * 3 = 9(starting from index 2 and ending at index 4)