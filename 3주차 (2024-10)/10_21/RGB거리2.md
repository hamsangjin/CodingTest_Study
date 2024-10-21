# [RGB거리2](https://www.acmicpc.net/problem/17404)

<br>

## 시간복잡도 분석
- 외부 루프는 3번 반복되고 내부 루프는 n번 실행되므로
- 전체 시간복잡도는 O(3 * n) = O(n)임.

<br>

## 코드
```java
import java.io.*;
import java.util.*;

public class RGB거리2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        int[][] arr = new int[n][3]; // 각 집의 비용을 저장할 배열
        int[][] dp = new int[n][3];

        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine(), " ");
            arr[i][0] = Integer.parseInt(st.nextToken()); // 빨강
            arr[i][1] = Integer.parseInt(st.nextToken()); // 초록
            arr[i][2] = Integer.parseInt(st.nextToken()); // 파랑
        }

        int answer = Integer.MAX_VALUE;
        for(int first = 0; first < 3; first++) { // 0번째 집을 3가지 색으로 칠하는 경우를 고정시키기

            // 첫번째 집 색 고정
            for(int i = 0; i < 3; i++) {
                if(i == first) {
                    dp[0][i] = arr[0][i];
                } else dp[0][i] = 1000 * 1000 + 1; // 이외의 색은 불가능한 큰값으로 설정
            }

            for (int i = 1; i < n; i++) {
                dp[i][0] = arr[i][0] + Math.min(dp[i - 1][1], dp[i - 1][2]); // 현재 집을 빨강으로 칠할 경우
                dp[i][1] = arr[i][1] + Math.min(dp[i - 1][0], dp[i - 1][2]); // 현재 집을 초록으로 칠할 경우
                dp[i][2] = arr[i][2] + Math.min(dp[i - 1][0], dp[i - 1][1]); // 현재 집을 파랑으로 칠할 경우
            }

            // 마지막 집에서 첫 번째 집과 같은 색을 제외하고 최솟값 찾기
            for(int last = 0; last < 3; last++) {
                if(last != first) { // 첫 번째 집과 마지막 집의 색이 달라야 함
                    answer = Math.min(answer, dp[n - 1][last]);
                }
            }

        }
        System.out.println(answer);
    }
}
```