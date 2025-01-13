# [ATM](https://www.acmicpc.net/problem/11399)

<br>

## 시간복잡도 분석
- O(N log N)

## 코드
```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        int[] arr = new int[N];
        String[] input = br.readLine().split(" ");
        for(int i=0; i<N; i++) arr[i] = Integer.parseInt(input[i]);

        Arrays.sort(arr);
        int[] dp = new int[N];
        dp[0] = arr[0];
        for(int i=1; i<N; i++) dp[i] = arr[i] + dp[i-1];

        int[] answer = new int[N];
        answer[0] = dp[0];
        for(int i=1; i<N; i++) answer[i] = dp[i] + answer[i-1];

        System.out.println(answer[N-1]);

        br.close();
    }
}
```