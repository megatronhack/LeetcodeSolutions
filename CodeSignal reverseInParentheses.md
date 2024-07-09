把括号里面的字符反转，遇到“（”记录start index， 遇到“）”记录end index，然后把这部分replace成反转后的结果。注意index的boundary， 需要remove掉“（” &“）”。

str.replace(start, end + 1, new StringBuilder(str.substring(start+1, end)).reverse().toString());

    foo(bar(baz))blim -> foo(barzab)blim -> foobazrabblim

Write a function that reverses characters in (possibly nested) parentheses in the input string.

Input strings will always be well-formed with matching `()`s.

Example

- For `inputString = "(bar)"`, the output should be
  `solution(inputString) = "rab"`;
- For `inputString = "foo(bar)baz"`, the output should be
  `solution(inputString) = "foorabbaz"`;
- For `inputString = "foo(bar)baz(blim)"`, the output should be
  `solution(inputString) = "foorabbazmilb"`;
- For `inputString = "foo(bar(baz))blim"`, the output should be
  `solution(inputString) = "foobazrabblim"`.
  Because `"foo(bar(baz))blim"` becomes `"foo(barzab)blim"` and then `"foobazrabblim"`.

Input/Output

- **[execution time limit] 3 seconds (java)**

- **[input] string inputString**

  A string consisting of lowercase English letters and the characters `(` and `)`. It is guaranteed that all parentheses in `inputString` form a [regular bracket sequence](keyword://regular-bracket-sequence).

  *Guaranteed constraints:*
  `0 ≤ inputString.length ≤ 50`.

- **[output] string**

  Return `inputString`, with all the characters that were in parentheses reversed.

```java
String solution(String inputString) {

  StringBuilder str = new StringBuilder(inputString);

  int start, end;

  while(str.indexOf("(") != -1){
    start = str.lastIndexOf("(");//return the last index of "(", return -1 if not found
    end = str.indexOf(")", start);
    str.replace(start, end + 1, new StringBuilder(str.substring(start+1, end)).reverse().toString());
    //1 round: foo(bar(baz))blim -> foo(barzab)blim
    //2 round: foo(barzab)blim -> foobazrabblim
  }
  return str.toString();
}
```

