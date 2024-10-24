# [N과 M(1)](https://www.acmicpc.net/problem/15649)

<br>

## 시간복잡도 분석

- N개 중에서 m개를 선택하는 순열의 개수를 뜻하기 때문에 시간 복잡도는 O(nP(m))입니다.

<br>

## 코드

```java
import java.io.*;
import java.util.*;

public class Main {
    static boolean[] ch;
    static int n, m;
    static List<Integer> list;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        ch = new boolean[n+1];

        list = new ArrayList<>();
        dfs();
    }

    public static void dfs(){
        if(list.size() == m){
            for(int num : list)     System.out.print(num + " ");
            System.out.println();
        } else{
            for(int i = 1; i <= n; i++) {
                if(!ch[i]){
                    ch[i] = true;
                    list.add(i);
                    dfs();
                    ch[i] = false;
                    list.removeLast();
                }
            }
        }
    }
}
```