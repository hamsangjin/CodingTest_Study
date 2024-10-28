# [N과 M(9)](https://www.acmicpc.net/problem/15663)

<br>

## 시간복잡도 분석

- N개 중에서 m개를 선택하는 순열의 개수를 뜻하기 때문에 시간 복잡도는 O(nP(m))입니다.

<br>

## 코드

```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M;
    static int[] arr;
    static boolean[] visited;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] input = br.readLine().split(" ");
        N = Integer.parseInt(input[0]);
        M = Integer.parseInt(input[1]);

        String[] nums = br.readLine().split(" ");
        arr = new int[N];
        for(int i=0; i<N; i++) arr[i] = Integer.parseInt(nums[i]);
        Arrays.sort(arr);

        int[] result = new int[M];
        visited = new boolean[N];

        dfs(result, 0);
        System.out.println(sb);

        br.close();
    }

    public static void dfs(int[] result, int depth) {
        // 깊이가 M에 도달하면 출력
        if (depth == M) {
            for (int num: result) {
                sb.append(num).append(" ");
            }
            sb.append("\n");
            return;
        }

        int prev = -1;  // 중복된 값 체크
        for (int i=0; i<arr.length; i++) {
            if(!visited[i] && arr[i] != prev) {
                visited[i] = true;
                result[depth] = arr[i];
                dfs(result, depth+1);
                visited[i] = false;

                prev = arr[i];  // 현재 값을 이전 값으로 저장하여 중복 방지
            }
        }
    }
}
```