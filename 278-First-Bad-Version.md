# 278. First Bad Version

## CH

说白了是找first occurrence。

循环不变量(loop invariant)是first bad version出现在[l, r]区间里。

Time complexity: O(logN)

Space complexity: O(1)

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while(left < right - 1){
            int mid = left + (right - left) / 2;
            if(isBadVersion(mid) != true){
                left = mid;
            }
            else{
                right = mid; 
            }
        }
        if(isBadVersion(left) == true){
            return left;
        }
        return right;
    }
}
```

```python
class Solution:
    def firstBadVersion(self, n: int) -> int:
        left = 1
        right = n
        while left < right - 1:
            mid = left + (right - left) // 2
            if isBadVersion(mid) == True:
                right = mid
            elif isBadVersion(mid) == False:
                left = mid
        if isBadVersion(left) == True:
            return left
        return right     
```

