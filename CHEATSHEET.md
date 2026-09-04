# Java 코테 치트시트

문법이 기억 안 날 때 여는 문서. 알고리즘이 아니라 **손이 굳어서 막히는 것**을 줄이는 용도다.

- [자료구조](#자료구조)
- [정렬](#정렬)
- [BFS / DFS](#bfs--dfs)
- [문자열·배열 변환](#문자열배열-변환)
- [표준 입력](#표준-입력)

---

## 자료구조

### HashMap — 개수 세기 (해시 문제 대부분)

```java
Map<String, Integer> map = new HashMap<>();

// 개수 누적: 없으면 0에서 시작
for (String s : arr) {
    map.put(s, map.getOrDefault(s, 0) + 1);
}

// 순회
for (Map.Entry<String, Integer> e : map.entrySet()) {
    String key = e.getKey();
    int cnt = e.getValue();
}

map.containsKey("a");   // 있는지
map.keySet();           // 키 전체
map.values();           // 값 전체
```

> **완주하지 못한 선수**, **의상**, **베스트앨범**이 전부 이 패턴이다.

### Queue — BFS용

```java
Queue<int[]> q = new ArrayDeque<>();
q.offer(new int[]{0, 0});      // 넣기

while (!q.isEmpty()) {
    int[] cur = q.poll();      // 빼기
    int x = cur[0], y = cur[1];
}
```

### Deque — 스택으로도 큐로도

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);      // 넣기
stack.pop();        // 빼기 (마지막에 넣은 것)
stack.peek();       // 보기만
stack.isEmpty();
```

### PriorityQueue — 힙

```java
// 작은 값 우선 (기본)
PriorityQueue<Integer> pq = new PriorityQueue<>();

// 큰 값 우선
PriorityQueue<Integer> maxPq = new PriorityQueue<>(Collections.reverseOrder());

pq.offer(5);
pq.poll();   // 가장 작은 값 꺼내면서 제거
pq.peek();   // 꺼내지 않고 보기
```

> **더 맵게**가 이것만 알면 풀린다.

---

## 정렬

```java
int[] arr = {3, 1, 2};
Arrays.sort(arr);                       // 오름차순

Integer[] boxed = {3, 1, 2};
Arrays.sort(boxed, Collections.reverseOrder());   // 내림차순 (int[]는 안 됨)

List<Integer> list = new ArrayList<>();
Collections.sort(list);
list.sort((a, b) -> b - a);             // 내림차순
```

### 2차원 배열 정렬 — 특정 열 기준

```java
int[][] arr = {{1, 5}, {2, 3}};
Arrays.sort(arr, (a, b) -> a[1] - b[1]);   // 1번 열 오름차순
```

### 문자열 이어붙여 큰 수 만들기

```java
String[] nums = {"3", "30", "34"};
Arrays.sort(nums, (a, b) -> (b + a).compareTo(a + b));
// "34" "3" "30"  →  "34330"
```

> **가장 큰 수** 문제의 핵심. 이 한 줄이 전부다.

---

## BFS / DFS

### BFS — 격자에서 최단거리

가장 자주 나온다. 통째로 외워두면 좋다.

```java
static int[] dx = {-1, 1, 0, 0};   // 상하좌우
static int[] dy = {0, 0, -1, 1};

int bfs(int[][] maps) {
    int n = maps.length, m = maps[0].length;
    int[][] dist = new int[n][m];

    Queue<int[]> q = new ArrayDeque<>();
    q.offer(new int[]{0, 0});
    dist[0][0] = 1;

    while (!q.isEmpty()) {
        int[] cur = q.poll();
        int x = cur[0], y = cur[1];

        for (int d = 0; d < 4; d++) {
            int nx = x + dx[d], ny = y + dy[d];

            if (nx < 0 || ny < 0 || nx >= n || ny >= m) continue;  // 범위 밖
            if (maps[nx][ny] == 0) continue;                        // 벽
            if (dist[nx][ny] != 0) continue;                        // 이미 방문

            dist[nx][ny] = dist[x][y] + 1;
            q.offer(new int[]{nx, ny});
        }
    }
    return dist[n - 1][m - 1] == 0 ? -1 : dist[n - 1][m - 1];
}
```

**핵심 3가지**
1. `dist` 배열이 방문 표시와 거리 계산을 동시에 한다. 따로 `visited`를 안 만들어도 된다.
2. 큐에 **넣을 때** 거리를 기록한다. 뺄 때 하면 중복으로 들어간다.
3. 범위 검사를 먼저 하지 않으면 `ArrayIndexOutOfBounds`가 난다.

> **게임 맵 최단거리**가 이 템플릿 그대로다.

### DFS — 재귀

```java
static int answer = 0;

void dfs(int[] numbers, int idx, int sum, int target) {
    if (idx == numbers.length) {          // 끝까지 왔으면
        if (sum == target) answer++;
        return;
    }
    dfs(numbers, idx + 1, sum + numbers[idx], target);   // 더하는 경우
    dfs(numbers, idx + 1, sum - numbers[idx], target);   // 빼는 경우
}
```

> **타겟 넘버**가 이 형태다. 종료 조건을 먼저 쓰고 시작하면 헷갈리지 않는다.

### 언제 뭘 쓰나

| 상황 | 선택 |
|---|---|
| **최단거리**를 묻는다 | BFS |
| 모든 경우의 수를 센다 | DFS |
| 덩어리 개수를 센다 (섬, 네트워크) | 둘 다 가능 |

---

## 문자열·배열 변환

여기서 시간을 많이 버린다. 자주 보게 될 것들만 모았다.

```java
// String → char 배열
char[] c = s.toCharArray();

// char → 숫자
int n = c[0] - '0';

// String → 숫자
int n = Integer.parseInt("123");

// 숫자 → String
String s = String.valueOf(123);

// String 뒤집기
String rev = new StringBuilder(s).reverse().toString();

// 자르기
s.substring(2);        // 2번째부터 끝까지
s.substring(1, 4);     // 1 이상 4 미만

// 쪼개기
String[] parts = s.split(" ");

// List → int[]
int[] arr = list.stream().mapToInt(i -> i).toArray();

// int[] → List
List<Integer> list = Arrays.stream(arr).boxed().collect(Collectors.toList());

// 배열 채우기
int[] arr = new int[10];
Arrays.fill(arr, -1);

// 2차원 배열 복사
int[][] copy = new int[n][];
for (int i = 0; i < n; i++) copy[i] = original[i].clone();
```

---

## 표준 입력

프로그래머스는 함수만 채우면 되므로 필요 없다.
**구름LEVEL, SWEA, 그리고 일부 기업 코테**에서 쓴다.

`Scanner`를 쓰면 입력이 많을 때 **알고리즘이 맞아도 시간 초과로 틀린다.**

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine().trim());

        // 한 줄에 여러 숫자
        StringTokenizer st = new StringTokenizer(br.readLine());
        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());

        // 출력은 모아서 한 번에
        for (int i = 0; i < n; i++) sb.append(i).append('\n');
        System.out.print(sb);
    }
}
```

> 반복문 안에서 `System.out.println`을 부르면 그것만으로 시간 초과가 날 수 있다.
