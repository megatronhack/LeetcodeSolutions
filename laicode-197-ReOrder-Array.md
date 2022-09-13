# Laicode 197. ReOrder Array

对数组进行重新排列，{N1, N2, N3, ..., N2k} -> {N1, Nk+1, N2, Nk+2, N3, Nk+3, ..., Nk, N2k}，{N1, N2, N3, ..., N2k, N2k+1} -> {N1, Nk+1, N2, Nk+2, N3, Nk+3, ..., Nk, N2k, N2k+1}.

仔细看一下这个重排列其实就是`ABCD1234` -> `A1B2C3D4`。那么我们通过reverse以及递归的思路，就可以解决这个问题。reorder(array, l, r)意义是对给定array[l, r]进行重排列。

所以我们先把[2, 4)和[4, 6)各自reverse，变成`ABDC2134`。

然后再把[2, 6)整体reverse，变成`AB12CD34`。

那么其实我们就相当于是把`12`和`CD`平行对调一下，然后我们在对`AB12`和`CD34`继续做类似的操作，最后他俩就各自变成`A1B2`和`C3D4`，总体变成`A1B2C3D4`。

左中点，中点，右中点要靠len分别区1/4、1/2和3/4处的地方。

左边递归的区间:换完之后，是`[l, l + (lm - m) * 2)]`，因为对应着左边的`(lm - m) * 2`个元素。

右边递归的区间是:`[lm + (lm - m) * 2, r]`，表明剩下的元素归右边递归来重排。这样最后，整个数组就会被我们重排成我们需要的样子。

basecase:那么如果`[l, r]`长度不大于2的话，就没必要重排。

大于2的话，继续。算出左中点，中点和右中点，分别对应的index是2、4、6。

最上层调用的时候，分奇偶处理就好。

![Laicode 197. ReOrder Array](assets\images\Laicode 197. ReOrder Array.jpg)

Time complexity: O(nlogn)，因为有logn层递归树，每一层都要对一半的元素进行重排。

Space complexity: O(logn) because of n level call stacks.

```java
public class Solution {
  public int[] reorder(int[] array) {
    // Write your solution here\
    //is even
    if (array.length % 2 ==0){
     reorder(array,0,array.length-1);
    }
    else{//is odd
    reorder(array,0,array.length-2);
    };
    return array;
  }
  private void reorder(int[] array, int left, int right){
    int length = right - left + 1;
   //basecase
   if (length <= 2){
     return;
   }
   
   //body
    int mid = left + length/2;
    int lmid = left + length/4;
    int rmid = left + length*3/4;
    reverse(array, lmid, mid -1);
    reverse(array, mid, rmid -1);
    reverse(array, lmid, rmid -1);
    //half of the partitions's size 
    reorder(array, left, left + (lmid - left)*2 - 1);
    reorder(array,left + (lmid - left)*2, right);

  }
  private void reverse(int[] array, int left, int right){
    while (left <= right){
      int tmp = array[left];
      array[left] = array[right];
      array[right] = tmp;
      left++;
      right--;
    }
  }
}
```