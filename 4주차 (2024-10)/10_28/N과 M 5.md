# [N과 M(5)](https://www.acmicpc.net/problem/15654)

<br>

## 시간복잡도 분석

- 모든 재귀 호출을 통해 m개의 요소를 선택하는 모든 순열을 생성하기 때문에 시간 복잡도는 O(nPm)임.


<br>

## 코드

```java
package baekjoon.silver;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class N과M_5 {

    public static int n;
    public static int m;
    public static int[] arr; // 입력 저장할 배열
    public static int[] p; // 출력 담을 배열
    public static boolean[] visited;
    public static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        arr = new int[n];
        p = new int[m];
        visited = new boolean[n];

        st = new StringTokenizer(br.readLine(), " ");
        for(int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(arr);

        dfs(0);
        System.out.println(sb);
    }

    public static void dfs(int d) {
        if(d == m) {
            for(int i : p) {
                sb.append(i).append(" ");
            }
            sb.append("\n");
            return;
        }

        for(int i = 0; i < n; i++) {
            if(visited[i]) continue;
            visited[i] = true;
            p[d] = arr[i]; // 현재 깊이 d에 arr[i] 값 넣기
            dfs(d + 1); // 다음 깊이로 재귀 호출
            visited[i] = false;
        }
    }
}

```