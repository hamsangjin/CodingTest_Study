# [Two Dots](https://www.acmicpc.net/problem/16929)

<br>

## 시간복잡도 분석
- DFS 호출에서 최대 N * M번, 각 DFS에서 최대 N * M번의 탐색이 가능하므로
- 시간 복잡도는 O((N×M)^2).

## 코드
```java
package baekjoon.silver;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class TwoDots {
    static int n, m;
    static char[][] board;
    static boolean[][] visited;
    static int[] dc = {-1, 0, 1, 0};
    static int[] dr = {0, 1, 0, -1};
    static boolean hasCycle = false;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        board = new char[n][m];
        visited = new boolean[n][m];

        for (int i = 0; i < n; i++) {
            String str = br.readLine();
            for (int j = 0; j < m; j++) {
                board[i][j] = str.charAt(j);
            }
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (!visited[i][j]) {
                    dfs(i, j, i, j, 1);
                }
            }
        }

        System.out.println(hasCycle ? "Yes" : "No");
    }

    public static void dfs(int x, int y, int startX, int startY, int count) {
        visited[x][y] = true;

        for (int i = 0; i < 4; i++) {
            int nx = x + dr[i];
            int ny = y + dc[i];

            if (nx >= 0 && nx < n && ny >= 0 && ny < m) {
                if (!visited[nx][ny] && board[nx][ny] == board[x][y]) { // 미방문이고 이전과 색이 같을 경우
                    dfs(nx, ny, startX, startY, count + 1);
                } else if (nx == startX && ny == startY && count >= 4) { // 시작점으로 돌아오고 경로 길이가 4 이상이면 사이클
                    hasCycle = true;
                    return;
                }
            }
        }

        visited[x][y] = false;
    }
}

```