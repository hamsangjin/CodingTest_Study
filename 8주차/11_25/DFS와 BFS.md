# [DFS와 BFS](https://www.acmicpc.net/problem/1260)

<br>

## 시간복잡도 분석
- DFS: N+M, BFS: N+M
- 시간 복잡도: O(N+M)

## 코드
```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M, V;
    static List<Integer>[] graph;
    static boolean[] ch;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        V = Integer.parseInt(st.nextToken());

        graph = new List[N+1];
        for(int i = 1; i <= N; i++) graph[i] = new ArrayList<>();

        for(int i = 0; i < M; i++){
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            graph[a].add(b);
            graph[b].add(a);
        }

        // 정점 번호가 작은 것을 먼저 방문하도록 정렬
        for (int i = 1; i <= N; i++)    Collections.sort(graph[i]);

        // DFS
        ch = new boolean[N+1];
        dfs(V);
        sb.append("\n");

        // BFS
        ch = new boolean[N+1];
        bfs(V);

        // 전체 결과 출력
        System.out.println(sb.toString());
    }

    static void dfs(int v) {
        ch[v] = true;
        sb.append(v).append(" ");
        for (int nv : graph[v]) {
            if (!ch[nv])    dfs(nv);
        }
    }

    static void bfs(int start) {
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        ch[start] = true;
        sb.append(start).append(" ");

        while (!q.isEmpty()) {
            int v = q.poll();
            for (int nv : graph[v]) {
                if (!ch[nv]) {
                    q.add(nv);
                    ch[nv] = true;
                    sb.append(nv).append(" ");
                }
            }
        }
    }
}
```