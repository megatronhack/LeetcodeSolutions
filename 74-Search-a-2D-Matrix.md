# 74. Search a 2D Matrix

Time complexity: O(log(m) + log(n))

Space complexity: O(1)

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        int len = rows * cols;
        int left = 0;
        int right = len - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(matrix[mid / cols][mid % cols] == target){
                return true;
            } else if(matrix[mid / cols][mid % cols] < target){
                left = mid + 1;
            } else{
                right = mid - 1;
            }
        }
        return false;
    }
}
```

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rows = len(matrix)
        cols = len(matrix[0])
        matrixLen = rows * cols
        left = 0
        right = matrixLen - 1
        while left <= right:
            mid = left + (right - left) //2
            if matrix[mid // cols][mid % cols] == target:
                return True
            elif matrix[mid // cols][mid % cols] < target:
                left = mid + 1
            else:
                right = mid - 1
        return False
```

