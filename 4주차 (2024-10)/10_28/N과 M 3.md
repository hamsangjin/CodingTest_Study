# [N과 M(3)](https://www.acmicpc.net/problem/15651)

<br>

## 시간복잡도 분석

- 선택할 수 있는 자연수는 N개이고, 수열의 길이가 M이므로 M번 만큼의 선택을 반복하기에 시간 복잡도는 O(N^M)

<br>

## 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    static int N, M;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        backtrack(0, new int[M]);

        System.out.print(sb.toString());
    }

    public static void backtrack(int depth, int[] sequence) {
        if (depth == M) {
            for (int i = 0; i < M; i++) {
                sb.append(sequence[i]).append(" ");
            }
            sb.append("\n");
            return;
        }

        // 1부터 N까지의 숫자를 선택
        for (int i = 1; i <= N; i++) {
            sequence[depth] = i; // 현재 위치에 숫자 i 저장
            backtrack(depth + 1, sequence); // 다음 위치 선택
        }
    }
}
```
