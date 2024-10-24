# [N과 M(2)](https://www.acmicpc.net/problem/15650)

<br>

## 시간복잡도 분석

- 각 재귀 호출에서 중복 없이 숫자를 선택하고, 깊이는 m 이므로 탐색의 경우의 수는 nCm임.
- 각 경우마다 m개의 숫자를 출력하므로 전체 시간 복잡도는 O(nCm \* m) 임.

<br>

## 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class N과M_2 {

    public static int n; // 1부터 n 까지
    public static int m; // 깊이
    public static int[] arr; // 출력 담을 배열
    public static boolean[] v; // 방문한 노드 체크할 배열
    public static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        arr = new int[m];
        v = new boolean[n];

        dfs(0, 0);
        System.out.println(sb);
    }

    private static void dfs(int d, int s) {
        if(d == m) { // 재귀 탈출 조건
            for(int i : arr) {
                sb.append(i).append(" ");
            }
            sb.append("\n");
            return;
        }

        for(int i = s; i < n; i++) {
            if(v[i]) continue; // 이미 방문한 노드는 넘어가기
            v[i] = true; // 방문한 노드 true 로 설정
            arr[d] = i + 1; // 깊이마다 1씩 더해서 arr 에 저장
            dfs(d + 1, i + 1); // 자식 노드 방문, s+1부터 arr가 채워지도록
            v[i] = false; // 방문 상태 되돌리기
        }
    }
}
```
