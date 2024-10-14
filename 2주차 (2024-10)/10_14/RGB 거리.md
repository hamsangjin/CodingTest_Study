# [RGB 거리](https://www.acmicpc.net/problem/1149)

<br>

## 시간복잡도 분석

- 입력 받는 횟수와 dp를 채우는 횟수가 전부 O(n)으로 전체 시간 복잡도는 O(n)이다.

<br>

## 코드

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        int[][] RGB = new int[n][3];
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            RGB[i][0] = Integer.parseInt(st.nextToken());
            RGB[i][1] = Integer.parseInt(st.nextToken());
            RGB[i][2] = Integer.parseInt(st.nextToken());
        }

        for (int i = 1; i < n; i++) {
            // 현재 집을 빨간색으로 칠할 때, 이전 집을 초록색(RGB[i-1][1]) 또는 파란색(RGB[i-1][2])으로 칠한 최소 비용을 더해주기
            RGB[i][0] += Math.min(RGB[i-1][1], RGB[i-1][2]);
            // 현재 집을 초록색으로 칠할 때, 이전 집을 빨간색(RGB[i-1][0]) 또는 파란색(RGB[i-1][2])으로 칠한 최소 비용을 더해주기
            RGB[i][1] += Math.min(RGB[i-1][0], RGB[i-1][2]);
            // 현재 집을 파란색으로 칠할 때, 이전 집을 빨간색(RGB[i-1][0]) 또는 초록색(RGB[i-1][1])으로 칠한 최소 비용을 더해주기
            RGB[i][2] += Math.min(RGB[i-1][0], RGB[i-1][1]);
        }

        // 다 칠했을 때의 최소비용 출력
        int result = Math.min(RGB[n-1][0], Math.min(RGB[n-1][1], RGB[n-1][2]));
        System.out.println(result);
    }
}
```