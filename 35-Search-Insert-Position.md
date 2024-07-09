# 35. Search Insert Position

## CH

这题说白了就是找第一个大于等于target的数。

先来左右边界检查，接着是二分搜索第一个GE的数。

Time complexity: O(logN)

Space complexity: O(1)

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
       if(nums == null || nums.length == 0){
           return -1;
       }
      int left = 0;
      int right = nums.length - 1;
      while (left < right){
        int mid = left + (right - left) / 2;
        if(nums[mid] < target){
            left = mid + 1;
        }
        else if(nums[mid] > target){
            right = mid - 1;
        }
        else{
            return mid;
        }
      }
      //corner one element
      if(nums.length == 1 && nums[0] == target){
          return left;
      }

      if(nums.length == 1 && nums[0] < target){
          return right + 1;
      }
        
      if(target <= nums[left]){
          return left;
      }
      else{
          return right + 1;
      }
    }
}
```

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <  right:
            mid = left + (right - left) // 2
            if nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
            else:
                return mid
        ## corner one element case
        if len(nums) == 1 and nums[0] == target:
            return left
        if len(nums) == 1 and nums[0] < target:
            return right + 1

        if nums[left] >= target:
            return left
        else:
            return right + 1
```

