需要找到能避开array里面所有num的一个Jump步数，这个步数是固定的single value。需要两个pointer：1.int jump记录步数 2. boolean 记录当前步数是否有效。

设置一个Jump步数，初始值为1，然后traverse array， 看里面的值是否整除步数为0，如果为0，则Jump会碰到这个obstacle，这个步数无效。继续递增步数直到找到一个有效的Jump步数。

You are given an array of integers representing coordinates of obstacles situated on a straight line.

Assume that you are jumping from the point with coordinate `0` to the right. You are allowed only to make jumps of the same length represented by some integer.

Find the minimal length of the jump enough to avoid all the obstacles.

Example

For `inputArray = [5, 3, 6, 7, 9]`, the output should be
`solution(inputArray) = 4`.

Check out the image below for better understanding:

![img](https://codesignal.s3.amazonaws.com/tasks/avoidObstacles/img/example.png?_tm=1624426122561)

```Java
int solution(int[] inputArray) {
    int jump = 1;
    boolean fail = true;
    
    while(fail) {//if the curret step not valid, need to increase jump and reset the value of fail
        jump++;
        fail = false;
        for(int i=0; i<inputArray.length; i++)
            if(inputArray[i]%jump==0) {
                fail = true;
                break;
            }
    }
    return jump;
}

```

