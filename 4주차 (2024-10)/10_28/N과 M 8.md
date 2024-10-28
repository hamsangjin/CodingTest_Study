# [N과 M(8)](https://www.acmicpc.net/problem/15657)

<br>

## 시간복잡도 분석

- N개 중에서 m개를 선택하는 순열의 개수를 뜻하기 때문에 시간 복잡도는 O(nP(m))입니다.

<br>

## 코드

```java
package baekjoon.silver;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class N과M_8 {
    static StringBuilder sb = new StringBuilder();  // 출력 결과를 저장할 StringBuilder
    static int n, m;  // n: 최대 숫자, m: 고를 숫자의 개수
    static boolean[] visit;  // 방문 여부를 체크할 배열
    static int[] arr;  // 선택한 숫자를 저장할 배열
    static int[] nums;  // 입력받은 숫자들을 저장할 배열

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());  // N 값
        m = Integer.parseInt(st.nextToken());  // M 값

        // 배열 초기화
        nums = new int[n];  // N개의 숫자를 저장할 배열
        arr = new int[m];  // M개의 선택된 숫자를 저장할 배열
        visit = new boolean[n];  // 방문 여부를 체크할 배열


        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }


        Arrays.sort(nums);


        dfs(0,0);
        System.out.print(sb);
    }

    private static void dfs(int depth,int start) {
        // M개의 숫자를 모두 선택한 경우
        if (depth == m) {
            for (int i = 0; i < m; i++) {
                sb.append(arr[i]).append(" ");
            }
            sb.append("\n");
            return;
        }


        for (int i = start; i < n; i++) {
            arr[depth] = nums[i];  // 선택한 숫자를 현재 깊이에 저장
            dfs(depth + 1,i);  // 다음 깊이로 이동
        }
    }
}
```