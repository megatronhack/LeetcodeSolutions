# 75. Sort Colors

利用快排中的挡板思想。只不过这里有三个挡板，`i`、`j`和`k`。

Time complexity: O(N)

Space complexity: O(1)

```java
class Solution {
    public void sortColors(int[] array) {
        int i = 0, j = 0, k = array.length - 1;
        while(j <= k){
            if(array[j] == 0){
                swap(array,i,j);
                i++;
                j++;
            }
            else if(array[j] == 1){
                j++;
            }
            else{
                swap(array,j,k);
                k--;
            }
        }
    }
    public void swap(int[] array, int left, int right){
        int temp = array[left];
        array[left] = array[right];
        array[right] = temp;
    }
}
```

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        i = 0
        j = 0
        k = len(nums) - 1
        while j <= k:
            if nums[j] == 0:
                self.swap(nums, i, j)
                i = i + 1
                j = j + 1
            elif nums[j] == 1:
                j = j + 1
            else:
                self.swap(nums, j, k)
                k = k - 1

    def swap(self, array, left, right):
        temp = array[left]
        array[left] = array[right]
        array[right] = temp
```

