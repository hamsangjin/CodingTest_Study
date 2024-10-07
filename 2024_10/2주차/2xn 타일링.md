# [2xn 타일링](https://www.acmicpc.net/problem/11726)

<br>

## 시간복잡도 분석
n에 크기에 비례하므로 시간복잡도는 O(n)

<br>

## 코드

```java
import java.io.*;

public class Main {
  static long[] arr = new long[1001];

  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    int n = Integer.parseInt(br.readLine());

    // 1부터 6까지
    // 1 2 3 5 8 13 -> 피보나치 수열
    arr[1] = 1;
    arr[2] = 2;

    for(int i=3; i<arr.length; i++)
      arr[i] = (arr[i-1] + arr[i-2]) % 10007;

    System.out.println(arr[n]);

    br.close();
  }
}
```
