# 912. Sort An Array

这题随便用merge sort或者quick sort都行。
+ [Merge Sort](laicode-9-Merge-Sort.md)
+ [Quick Sort](laicode-10-Quick-Sort.md)

counterSort O(n+k)    ,  because collections.Counter(N) = o(N)

```python
class Solution:
    def sortArray(self, N: List[int]) -> List[int]:
        # Step 1: Create a counter for all elements in the list N
        C = collections.Counter(N)
        
        # Step 2: Find the minimum and maximum values in the list N
        m, M = min(N), max(N)
        
        # Step 3: Create an empty list to store the sorted result
        S = []
        
        # Step 4: Iterate over the range from min to max value (inclusive)
        for n in range(m, M + 1):
            # Extend the list S by the number n, repeated by its count in N
            S.extend([n] * C[n])
        
        return S
```

