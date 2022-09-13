Laicode 175. Decompress String II

建议用method2string builder，简单点

**Method 1:**

给定压缩后的字符串，对其进行解压。比如`a1c0b2c4`变成`abbcccc`。

Clarification:
+ 输入是否可能为null？不
+ 字符串的字符范围？仅小写字母
+ 数字范围？0-9

那么这里我们依然两步走，第一步先解压所有数字小于等于2的，第二步解压大于2的。因为数字小于等于2的话，解压出来最多和压缩之后等长，而不会超过，所以可以在原数组上进行解压。因此就把`a1c0b2c4`变成`abbc4`。那么我们可以从前向后，每次遍历两位。先看数字是否在0~2以内，如果是的话就解压。不是的话，就拷贝。这样我们就可以初步得到解压所有0~2之后的字符串长度。

紧接着，第二部我们解压所有数字大于2的。那么我们先要得到解压后新字符串的长度，依次遍历所有剩余的数字，拿上一步得到的长度加上每个数字减2，就是解压缩之后的新长度。双指针，i从初步解压缩的最后一位向前，j从新字符数组的最后一位向前。每当i遇到一个数字`y`，就把它前面的字符拷贝`y`份到以j为结尾的地方。i要跳过前面的字符，j要跳过`y`个长度向前。如果i遇到字母，那就简单的拷贝i给j。

这样最后整个字符串就被我们成功解压缩了。

Time complexity: O(n)，三轮遍历。

```java
public class Solution {
  public String decompress(String input) {
 // Method 1: "in place".
  // When we say in place, it usually means the input is a long enough
  // char array, and the original string only occupies part of the array
  // starting from index 0, and usually the length to represent the
  // original string is given.
    if (input.isEmpty()) {
      return input;
    }
    char[] array = input.toCharArray();
    // We need to handle the
    // "a0", "a1", "a2" case (the decoded string is shorter) and
    // "a3", "a4" ... case (the decoded string is longer)
    // in two pass to avoid conflict, since the encoding of the two cases
    // require different directions.
    return decodeLong(array, decodeShort(array));
  }

  // return the length of he decoded string,
  // only cares about "a0", "a1", "a2", A.K.A
  // the decoded string is shorter.
  private int decodeShort(char[] input) {
    // since the decoded string is shorter, we should
    // do the decoding work from left to right direction.
    int end = 0;
    for (int i = 0; i < input.length; i += 2) {
      int digit = getDigit(input[i + 1]);
      if (digit >= 0 && digit <= 2) {
        for (int j = 0; j < digit; j++) {
          input[end++] = input[i];
        }
      } else {
        // we don't handle the longer decoded string here.
        input[end++] = input[i];
        input[end++] = input[i + 1];
      }
    }
    return end;
  }
  // take care of "a3", "a4", "a5",....
  // the decoded string is longer.
  // length: the length of the valid partition starting from index 0.
  private String decodeLong(char[] input, int length) {
    // we need to calculate the new required length.
    int newLength = length;
    for (int i = 0; i < length; i++) {
      int digit = getDigit(input[i]);
      if (digit > 2 && digit <= 9) {
        newLength += digit - 2;
      }
    }
    // Notice: if it is required to do this in place, usually the input
    // array is a sufficient large one, you will not need to
    // allocate a new array. This solution is only for demonstration.
    char[] result = new char[newLength];
    int end = newLength - 1;
    for (int i = length - 1; i >= 0; i--) {
      int digit = getDigit(input[i]);
      if (digit > 2 && digit <= 9) {
        i--;
        for (int j = 0; j < digit; j++) {
          result[end--] = input[i];
        }
      } else {
        // we already take care the shorter cases, "a1" in previous pass.
        // we can leave as it is. e.g. the input could be "abc2".
        result[end--] = input[i];
      }
    }
    return new String(result);
  }

  private int getDigit(char digit) {
    return digit - '0';
  }
 // Time Complexity: O(n)
 // Space Complexity: O(1)
}

```

**Method2: String builder**

Time On

Space On

```
public class Solution {
  public String decompress(String input) {
    // Write your solution here
    char[] array = input.toCharArray();
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < array.length; i++){
      char ch = array[i++];
      int count = array[i] - '0';
      for (int c = 0; c < count; c++){
        sb.append(ch);
      }
    }
    return sb.toString();
  }
}

```

