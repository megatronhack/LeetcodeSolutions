需要检查是否size== 4， 每个string里面的char是否都是digit，string在0-255区间， 如果leading char是‘0’后面不能有别的数字否则提前返回false

注意Corner case 比较多

An IP address is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication. There are two versions of the Internet protocol, and thus two versions of addresses. One of them is the [IPv4 address](keyword://ipv4-address).

Given a string, find out if it satisfies the IPv4 address naming rules.

Example

- For `inputString = "172.16.254.1"`, the output should be
  `solution(inputString) = true`;

- For `inputString = "172.316.254.1"`, the output should be
  `solution(inputString) = false`.

  `316` is not in range `[0, 255]`.

- For `inputString = ".254.255.0"`, the output should be
  `solution(inputString) = false`.

  There is no first number.

```java
boolean solution(String inputString) {
    //check if the size == 4 and integer <= 255
    String[] array = inputString.split("[.]");
    if (array.length != 4) return false;
    for (String cur : array) {
        if (cur.isEmpty()) return false;
        if (!cur.matches("[0-9]{1,3}")){
            return false;
        }
        int num = 0;
        for (int i = 0; i < cur.length(); i++) {
            if(num == 0 && i != 0) return false;
            num = 10 * num + (cur.charAt(i) - '0');
        }
        if (num > 255) return false;
    }
    return true;
}
```

