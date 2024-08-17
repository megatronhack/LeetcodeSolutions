# Laicode 10. Quick Sort

快排实现。

快排的基本思想也是分治。从数组里随机挑一个点作为pivot把数组一分为二，对数组进行分割。分割的同时也要对数组进行一系列调整，目标是经过分割之后pivot左边所有数都小于它，右边所有数都大于等于它。这样我们再对左右子数组进行相同的操作，直到子数组不可拆分为止，最后整个数组都有序了。

这里分治原理很简单，和merge sort一样，主要是难在`partition`。我们来详细解析一下这个方法。

我们先从[left, right]中随机挑一个数作为`pivot`，然后把它和`right`交换。剩下来就是把[left, right - 1]区间给变成连续的一部分小于pivot，剩下的部分大于等于pivot。最后再把pivot放回两个部分的交界处就好了。

`partition` 维持着一个循环不变量，[left, l)区间元素均小于`pivot`，(r, right-1]区间元素均大于等于`pivot`，他们俩相当于是两个挡板。无论是每一轮循环开始前，还是每一轮循环结束后，该循环不变量都成立。

所以，如果我们要让两个区间顺利汇合从而使他们合并成为连贯的[left, right - 1]区间的话，那么`l`最后`r`必然要大于`r`才行。所以循环条件是`while(l <= r)`。

刚开始时候，`[left, l)`和`(r, right-1]`都是空区间，空区间当然是符合我们的循环不变量的。当`array[l] < pivot`的时候，那么`l++`来维护循环不变量。当`array[r] >= pivot`的时候，`r--`来维护循环不变量。到else进行交换的时候，l是停在一个大于等于pivot的位置，而r是停在一个小于pivot的位置。交换过后，l和r各自自增和自减以维护循环不变量。

循环退出时，`l == r + 1`是必然的，不可能出现其他情况。如果`l == r + 2`，那么意味着之前有一次交换的时候，l和r是同一个数，但是同一个数不可能同时满足`if` 和 `else if`的两个条件，所以不可能出现该情况。

由于我们不断地维护循环不变量，循环结束之后[left, l)均小于`pivot`依然成立，(r, right - 1]也依然成立。只不过，可以改写为[left, l) < pivot，[l, right - 1] >= pivot。由于我们之前把pivot换到right位置了，所以现在把pivot换回到当前`l`的位置就可以实现——pivot左边都小于等于它，pivot右边都大于等于它。

Time complexity: O(NlogN) in average, O(N^2) in worst case

Space complexity: O(logN) in average, O(N) in worst case

```java
class Solution {
    public int[] sortArray(int[] nums) {
        //quick sort
        //choose a povot and sort the remainings, then put the pivot back to its position
        //keep on partioning on left to pivot -1, pivot + 1 and right until left >= right

        //tc:O(nlogn) sc: O(logn)
        if (nums == null || nums.length <= 1) return nums;
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }

    public void quickSort(int[] nums, int left, int right){
        //base case
        if (left >= right){
            return;
        }
        int pivotIndex = partition(nums, left, right);
        quickSort(nums, left, pivotIndex - 1);
        quickSort(nums, pivotIndex + 1, right);
    }

    public int partition(int[] nums, int left, int right){
        //sub problem: choose a pivot and sort
        int pivot = randomIndex(left, right);
        int target = nums[pivot];
        swap(nums, pivot, right);
        //-1, 2, 4, 3, 2(pivot)
        int leftBound = left;
        int rightBound = right - 1;
        while (leftBound <= rightBound){
            if (nums[leftBound] <= target){
                leftBound++;
            } else if (nums[rightBound] > target){
                rightBound--;
            } else {
                swap(nums, leftBound, rightBound);
                leftBound++;
                rightBound--;
            }
        }
        swap(nums, leftBound, right);
        return leftBound;
    }

    public void swap(int[] nums, int left, int right){
        if (nums == null || nums.length <= 1) return;
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }

    public int randomIndex(int left, int right){
    int pivot = left + (int)(Math.random()* (right - left + 1));
    return pivot;
    }
}
```

```python
import random
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        if nums is None or len(nums) <= 1:
            return nums
        self.quickSort(nums, 0, len(nums) - 1)
        return nums
    
    def partition(self, nums, left, right):
        pivot = random.randint(left, right)
        target = nums[pivot]
        nums[pivot], nums[right] = nums[right], nums[pivot]
        leftBound = left
        rightBound = right - 1

        while leftBound <= rightBound:
            if nums[leftBound] <= target:
                leftBound += 1
            elif nums[rightBound] > target:
                rightBound -= 1
            else:
                nums[leftBound], nums[rightBound] = nums[rightBound], nums[leftBound]
                leftBound += 1
                rightBound -= 1

        nums[leftBound], nums[right] = nums[right], nums[leftBound]
        return leftBound

    def quickSort(self, nums, left, right):
        if left >= right:
            return
        pivotIndex = self.partition(nums, left, right)
        self.quickSort(nums, left, pivotIndex - 1)
        self.quickSort(nums, pivotIndex + 1, right)
```

