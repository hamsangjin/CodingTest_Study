# [BaseConversion](https://www.acmicpc.net/problem/11576)

<br>

## 시간복잡도 분석
- A진법에서 10진법으로 변환하는 과정은 for문이 반복하는 만큼인 O(m)정도 걸리고
- 10진법에서 B진법으로 변환하는 과정은 10진법으로 되어있는 값을 B로 계속 나누는 것이므로 O(log_B(ans))정도 소요된다.
- 따라서 전체 시간 복잡도는 O(m * log_B(ans))입니다.

<br>

## 코드
```java
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        // 입력
        String[] ab = br.readLine().split(" ");
        int a = Integer.parseInt(ab[0]);
        int b = Integer.parseInt(ab[1]);
        int m = Integer.parseInt(br.readLine());
        String[] nums = br.readLine().split(" ");

        // A진법을 10진법으로 변환
        int ans = 0;
        int temp = 1;       // a^0부터 시작
        for (int i = m - 1; i >= 0; i--) {
            ans += Integer.parseInt(nums[i]) * temp;
            temp *= a;
        }

        // 10진법으로 변환한 값을 B진법으로 변환
        List<String> list = new ArrayList();
        while(ans != 0) {
            list.add(Integer.toString(ans%b));
            ans /= b;
        }

        // list.reversed();는 백준에서 못 씀 ㅜ
        Collections.reverse(list);
        System.out.println(String.join(" ", list));
    }
}
```