# 50. Pow(x, n)

## Solution 1

经典的分治思想。

n是偶数的话，`x^n` 可以由 `x^(n/2) * x^(n/2)` 计算得出。`n` 是奇数的话，`x^n` 则由 `x^(n/2) * x^(n/2) * x` 所得。

Corner case:
+ n 是负数怎么办？转化为正数，最后被1除。
+ 注意 n 是 `-2147483648`，int的范围是 `-2147483648 ~ 2147483647`。

Time complexity: O(log(n)), because of log(n) level recursion.

Space complexity: O(log(n)), because of log(n) level recursion.

```java
class Solution {
    public double myPow(double x, int n) {
        if(n >= 0){
            return pow(x, n);
        }else{
            long longN = n;
            return 1 / pow(x, -longN);
        }
    }

    private double pow(double x, long n){
        if(n == 0){
            return 1.0;
        }
        double halfRes = pow(x, n / 2);
        if(n % 2 == 1){
            return halfRes * halfRes * x;
        }else{
            return halfRes * halfRes;
        }
    }
}
```



```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if(n == 0):
            return 1.0
        if n < 0:
            x = 1 / x
            n = -n
        halfResult = self.myPow(x,  n // 2)
        if n % 2 == 0:
            return halfResult * halfResult
        else:
            return halfResult * halfResult * x
        
```