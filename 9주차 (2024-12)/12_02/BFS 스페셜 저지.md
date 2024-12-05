# [BFS 스페셜 저지](https://www.acmicpc.net/problem/16940)

<br>

## 시간복잡도 분석
- 그래프 생성 O(n)
- 정렬 O(nlogn)
- BFS O(n)
- 최종 시간 복잡도 O(nlogn)

## 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.io.*;
import java.util.*;

public class Bfs스페셜저지 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine()); // 노드의 개수
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }

        // 그래프 입력
        for (int i = 0; i < n - 1; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            graph.get(u).add(v);
            graph.get(v).add(u);
        }


        st = new StringTokenizer(br.readLine());
        int[] order = new int[n];
        int[] position = new int[n + 1];
        for (int i = 0; i < n; i++) {
            order[i] = Integer.parseInt(st.nextToken());
            position[order[i]] = i;
        }


        for (int i = 1; i <= n; i++) {
            graph.get(i).sort(Comparator.comparingInt(a -> position[a]));
        }


        if (isBFSValid(graph, order, n)) {
            System.out.println(1);
        } else {
            System.out.println(0);
        }
    }

    private static boolean isBFSValid(List<List<Integer>> graph, int[] bfsOrder, int n) {
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n + 1];

        int index = 0;
        queue.add(1);
        visited[1] = true;

        while (!queue.isEmpty()) {
            int current = queue.poll();


            if (bfsOrder[index++] != current) {
                return false;
            }


            for (int neighbor : graph.get(current)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }

        return index == n;
    }
}
```