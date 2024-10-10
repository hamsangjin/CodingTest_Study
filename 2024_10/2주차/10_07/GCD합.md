# [GCD합](https://www.acmicpc.net/problem/9613)

<br>

## 시간복잡도 분석

- 배열 초기화: 𝑂 ( 𝑛 ) O(n) 
- 이중 반복문을 통한 모든 쌍의 최대공약수 계산: 𝑂 ( 𝑛^2 ) O(n^2 ), 각 쌍마다 𝑂 ( log ⁡ 𝑀 ) O(logM)의 최대공약수 계산이 포함됨.
- 따라서, 각 테스트 케이스의 시간 복잡도는  𝑂 ( 𝑛^2 log ⁡ 𝑀 ) O(n^2 logM)입니다.
- 전체 프로그램의 시간 복잡도: 테스트 케이스가 𝑡 t개 주어지므로, 전체 시간 복잡도는  𝑂 ( 𝑡 ⋅ 𝑛^2 log ⁡ 𝑀 ) O(t⋅n^2 logM)입니다.

<br>

## 코드

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class GCD의합 {
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());
        for(int i = 0 ; i < t; i++){
            //배열에 입력
            StringTokenizer st = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(st.nextToken());
            int[] arr = new int[n];

            for(int  j = 0 ; j < n; j++){
                arr[j] = Integer.parseInt(st.nextToken());
            }

            //커질수 있으므로 long 타입으로 선언
            long sum = 0;

            //더하기
            for(int k = 0 ; k < arr.length - 1;k++){
                for(int l = k+1; l < arr.length; l++ ){
                    sum += gcd(arr[k],arr[l]);
                }
            }

            System.out.println(sum);
        }

    }

    public static int gcd(int a,int b){ //gcd
        while(b != 0){
            int temp = b ;
            b = a % b;
            a = temp;
        }
        return a;
    }
}
```
