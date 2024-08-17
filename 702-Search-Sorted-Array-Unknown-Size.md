```

```

# 702. Search in a Sorted Array of Unknown Size

这题主要是array长度未知，所以我们要先确定二分搜索的左右边界。

先确定左右边界为0和1，不断地对对范围进行double来确定target是否在[l, r]之中。

敲定了target所在的范围之后，对这个范围进行二分搜索。

二分搜索的循环不变量是，target始终在[l, r]这个区间里。如果能找得到，那么一定会在循环结束之前找到并返回。如果循环顺利结束，l > r，说明没找到。

```java
/**
 * // This is ArrayReader's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface ArrayReader {
 *     public int get(int index) {}
 * }
 */

class Solution {
    public int search(ArrayReader reader, int target) {
        //use the ArrayReader and its function to get the search range
        //then use binary search method to find the target
        //tc:o(logn) sc:o(1)
        int left = 0; 
        int right = 2 * left + 1;
        while(reader.get(right) < target){
            left = right;
            right = 2 * left + 1;
        }
        return getIndex(reader, left, right, target);

    }

    public int getIndex(ArrayReader reader, int left, int right, int target){
        while (left <= right){
            int mid = left + (right - left)/2;
            if (reader.get(mid) == target){
                return mid;
            } else if(reader.get(mid) < target){
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
        }
}
```

```python
# """
# This is ArrayReader's API interface.
# You should not implement it, or speculate about its implementation
# """
#class ArrayReader:
#    def get(self, index: int) -> int:

class Solution:
    def search(self, reader: 'ArrayReader', target: int) -> int:
        left = 0
        right = left * 2 + 1
        while reader.get(right) < target:
            left = right
            right = left * 2 + 1
        return self.BST(left, right, reader, target)

    def BST(self, left: int, right: int, reader: 'ArrayReader', target: int) -> int:
        while left <= right:
            mid = left + (right - left) // 2
            if reader.get(mid) == target:
                return mid
            elif reader.get(mid) < target:
                left = mid + 1
            else:
                right = mid - 1
        return -1
```

