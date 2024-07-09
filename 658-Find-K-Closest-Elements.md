# 658. Find K Closest Elements

这题依然是二分搜索找到第一个大于等于`x`的的元素，以它为原点向前取k个元素，

Time complexity: O(logN + k), N is array length.

Space complexity: O(k), because we have to return list.

```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int target) {
        //find the closest equal or smaller element's index
        //use the the index and index + 1 to compare the value with target
        //tc:O(logn)+O(klogk) sc:O(k)
        //corner case 
        List<Integer> res = new ArrayList<>();
        if (arr == null || arr.length == 0){
            return res;
        }
        int left = findClose(arr, target);
        int right = left + 1;
        while(k > 0){
            if(right >= arr.length || left >= 0 && target - arr[left] <= arr[right] - target){
                res.add(arr[left]);
                left--;
            } else {
                res.add(arr[right]);
                right++;
            }
            k--;
        }
        Collections.sort(res);
        return res;
    }

    public int findClose(int[] arr, int target){
        int left = 0;
        int right = arr.length - 1;
        while(left < right - 1){
            int mid = left +(right - left)/2;
            if (arr[mid] == target){
                return mid;
            }else if (arr[mid] > target){
                right = mid;
            } else {
                left = mid;
            }
        }
        //if all elements bigger than target, would return 0, ok
        //if all smaller than target, would return the last second one, then compare this one with last one, ok
        return left;
    }
}
```

```python
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        res = []
        if not arr:
            return res
        left = self.BST(arr, x)
        right = left + 1
        while k > 0:
            if right >= len(arr) or (left >= 0 and x - arr[left] <= arr[right] - x):
                res.append(arr[left])
                left -= 1
            else:
                res.append(arr[right])
                right += 1
            k -= 1
        res.sort()
        return res

    def BST(self, array: List[int], target: int) -> int:
        left = 0
        right = len(array) - 1
        
        while left < right - 1:
            mid = left + (right - left) // 2
            if array[mid] == target:
                return mid
            elif array[mid] < target:
                left = mid
            else:
                right = mid
        return left

```

